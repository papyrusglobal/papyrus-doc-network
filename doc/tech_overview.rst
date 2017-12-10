Technology overview
===================

Basic concept
-------------


The base of Papyrus technology is the scalability layer. This layer allows processing large amounts of data (operational logs of the bidding process, ad tracking, inputs from the data processing vendors) while keeping blockchain guarantees. Papyrus uses map-reduce approach to aggregate data from multiple sources into compact lists of output transactions which are posted to the base blockchain. This is somewhat similar to plasma.io approach. But our solution is much simpler because we do not try to build public universal blockchain.

The scalability layer is a combination of: 

* State channel nodes responsible for accumulating data and placing it into the distributed storage.
* Distributed offchain storage based on IPFS.
* Validator nodes responsible for aggregating,and processing validating data (though logically distinct, this functionality will be implemented as part of channel nodes).
* Base chain: in the prototype - ethereum blockchain. In production mode - consortium blockchain shared among ecosystem participants (like https://github.com/tendermint/ethermint or bitshares).
* Token exchange protocol between the base chain and public chains like Ethereum or Bitcoin (two-way peg).

Papyrus node
------------

.. image:: images/tech_overview.webp

Papyrus node is a complete set of required software for blockchain and IPFS communication. It consists of business logic, state channel node and validator node.


Channel blocks
--------------

State channel's message log may grow at a rate of thousands messages per second and needs to be compacted before settling to the base blockchain. For this reason messages in each state channel are grouped into blocks. Blocks may have thousands of messages. So we have a hierarchy: base chain→state channel→block→message. We update the base chain on a per-block basis so that blockchain interaction is limited. Only block headers go to the base chain. Block data is stored in the offchain block storage, and retained for a limited period of time.

Messages which need to be processed together (e.g. messages for the same impressionId) must be assembled into the same block and hence need to be assigned the same block number. Participants must agree in advance on how block numbers are generated. For example SSP may generate block number incremented every hour and pass it to other participants during RTB. Each message must include signature, target channel id and block number.

Lifecycle of each channel block has the following stages:

* Collection. Each participant produces messages and sends them to its channel node. Channel node temporarily stores messages in apache kafka for persistence. 

* Collation. When collection period is finished (no new messages may be added to the block) each participant:

  * assembles all block messages into a single blob - "block part" (block part is different for each participant, so each block may have up to N block parts, where N - is number of participants);
  * writes the block part to block storage;
  * computes hash of the block part and store to base chain.

* Processing. After each participant have posted its block part, all block parts are merged and processed by validators. As a result of processing validators generate block output. This part is described in Validators section below.

* Settlement. Block output transactions are settled to the base chain.

Notes:

* Different blocks are processed independently. Processing of the next block may be completed earlier than that of the previous. To ensure that all participants have enough time to write their data there is a timeout before the block is considered final. It must account for all possible delays such as the maximum period needed for verifying impressions by the appointed auditor(s).
* To avoid DoS attacks there are limits on the number of messages per block and the message size.
* Data written to the block storage is encrypted with the keys known only to the particular channel participants.
* When assembling their block parts participants may include both messages created by themselves and messages created by other participants. Generally speaking participants are expected to include those messages they are incentivised to store (and most likely skip all other messages), i.e. all the messages that being excluded make the participant risk losing money.



Validators
----------

Block data processing is performed offchain by validator nodes. Validation algorithm is deterministic so each non-faulty validator given the same input data must return the same result. To make validation process scalable Papyrus uses only a few validator nodes for each block, and only if no consensus can be reached additional validators can be involved for dispute resolution.

Validator nodes act on request from participants. To process the block they need to

* download all the block parts from the storage
* merge block parts - duplicate messages are removed and messages are sorted deterministically 
* process result block data using specific algorithm which also may use data from the state channel contract
* as a result of processing a list of output transactions is constructed

Block processing has the following steps:

* Each participant chooses which validators it will delegate block validation to and sends them a signed request containing channel id, block number and block encryption key. Validators use provided information to process block data and post hashed results to the blockchain.
* If all choosen validators produce the same result (normal situation) then processing completes.
* If at least two validators have returned different results then block challenge period is extended and dispute process is used to resolve conflicts.

Participants may use different strategies for choosing validators:

* By running trusted validator node. Install trusted validator node on their own servers and use it for each new block.
* By running coordinator node which selects external validators. One or several randomly choosen validators are used for each new block. Participant still need to run coordinator node to choose and communicate with validators.
* In normal situation the number of validators is equal to the number of participants. But in case of faulty or malicious behaviour of validators the dispute process is used to ensure correctness and additional validators may be used.

Event sequence
--------------

An important part of the process is how events are recorded. In the prototype ecosystem Papyrus suggests two types of records:

1. Win records. These records are generated by SSP after determining a winner and by DSP after receiving a win notification.
2. Auditor check records. These records are generated by auditor after receiving tracking events from the browser/app.

The placement of record generation is illustrated on the following sequence diagram.

.. image:: images/sequence.png
