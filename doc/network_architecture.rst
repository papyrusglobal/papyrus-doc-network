Governance
===========================

There are many issues with governance paradigms used in other blockchain solutions, which lead to unacceptable level of centralization. For instance, EOS network is governed by Constitution and 21 Block Producers, which execute EOS protocol and are elected using dPoS mechanism. But voting thresholds to become elected BPs are low due to absence of quorum requirements, and power is consolidated in the hands of few people with significant token holdings and influence over BP decisions. Political systems, where power is consolidated in the hands of richest, are called plutocracy. In another dPoS network - TRON - situation is even worse, as not only BPs are elected by elite token holders with large stakes, but BPs are allowed to buy votes from token holders, and they spend their mining rewards to attract votes, instead of investments in better service and infrastructure. On the opposite, PoW networks have an issue with consolidation of power in large mining pools, controlling a significant percentage of network’s hashpower and effectively controlling the network itself. 

Our design goal in Papyrus Network was to construct governance protocol, which is aligned with Proof-of-Authority consensus for network scalability reasons, in a way to maintain greater level of decentralization and incentivize benefit of everyone: token holders, miners (authority nodes) and network customers (application developers and users). To achieve this goal we implemented flexible governance protocol, which somewhat reflects how corporations are managed in the modern world by shareholders and the board of directors. We believe that this is the best construction to be used as the network evolves to stimulate its growth.

Papyrus Network User Agreement
------------

Definitions
-----------

Papyrus Network User Agreement: This document (PNUA)

Chain ID: 32328

BIOS Contract: An Papyrus Network smart contract with a dynamic permissions structure, which defines network governance procedures.

User: Any person or organization of persons who maintain(s) direct or indirect ownership of an Papyrus Network address, or property connected to an Papyrus Network address.

Ownership: Direct or indirect access to an Papyrus Network address through one or more valid permissions checks. Ownership may be partially shared between Users through the use of multi-signature permissions.

Authority Nodes: Users who have created new blocks in Papyrus Network.

On-Chain: Any transaction, smart contract, or Ricardian contract which is located within a block that is irreversible and appended to the Papyrus Network.

Papyrus Network-based Property: Anything that requires a valid permission in order to directly manipulate, alter, transfer, influence, or otherwise effect on the Papyrus Network

Call: To submit an action to the Papyrus Network.

Authorizations & Permissions: Permissions are arbitrary names used to define the requirements for a transaction sent on behalf of that permission. Permissions can be assigned for authority over specific contract actions.

Article I -  User Acknowledgement of Risks
If User loses access to their Papyrus Network address on chain_id and has not taken appropriate measures to secure access to their Papyrus Network address by other means, the User acknowledges and agrees that that Papyrus Network address will become inaccessible. Users acknowledge that the User has an adequate understanding of the risks, usage and intricacies of cryptographic tokens and blockchain-based software. The User acknowledges and agrees that the User is using the Papyrus Network at their sole risk.

Article II - Consent of the PNUA
The nature of the Papyrus Network User Agreement is such that it serves as a description of the current Papyrus Network Mainnet governance functions that are in place. These functions, enforced by code, do not require the consent of Users as these functions are inherent and systemic to the Papyrus Network Mainnet itself.

Article III - Governing Documents
Current version of PNUA is referred by its SHA256 hash in Papyrus Network BIOS Contract and modifications to the PNUA may be made using BIOS Contract.

Article IV - Native Unit of Value
The native unit of value on Papyrus Network chain_id shall be the PPR token as defined by Papyrus Network software.

Article V - Maintaining the Papyrus Network 
Papyrus Network code is published in open GitHub repositories and open source developers community is supposed to maintain the active blockchain codebase which includes, but is not limited to, the implementation of all modifications of all features, optimizations, and upgrades: present and future.

Article VI - No Fiduciary
No User shall have a fiduciary purpose to support the value of the PPR token. No User can authorize anyone to hold assets, borrow, speak, contract on behalf of other Papyrus Network Users or the Papyrus Network chain_id collectively. Papyrus Network shall have no owners, managers, or fiduciaries.

Article VII - User Security
All items pertaining to personal account security, including but not limited to the safekeeping of private keys, is solely the responsibility of the User to secure.

Article VIII - Authority Nodes Limited Liability
The User acknowledges and agrees that, to the fullest extent permitted by any applicable law, this disclaimer of liability applies to any and all damages or injury whatsoever caused by or related to risks of, use of, or inability to use, the PPR token or the Papyrus Network under any cause of action whatsoever of any kind in any jurisdiction, including, without limitation, actions for breach of warranty, breach of contract or tort (including negligence) and that Authority Nodes shall not be liable for any indirect, incidental, special, exemplary or consequential damages, including for loss of profits, goodwill or data.

Adding new Authority Node
-------------------------

Any Authority Node can make proposal on adding new Authority Node to the network, which follows the approval process.
Any Authority Node can vote for proposed Authority Node candidate, if it is not blacklisted in either authority nodes blacklist or stakeholders blacklist. In total each Authority Node can vote for a maximum of 7 other Authority Nodes or candidates. Authority Node can move their votes from one Node to another at any time. 
Candidate Node becomes Authority Node if it keeps minimum 3 votes and holds in the top 47 Candidate and Authority Nodes by received votes number for continuous 7 days. Only votes from Authority Nodes are counted.    

Authority Nodes Management
--------------------------

1. Election
-----------

New Authority Nodes are elected by existing Authority Nodes. 

Authority Node candidate can be proposed by any of existing Authority Nodes.
After Authority Node candidate is proposed, voting for the Authority Node candidate begins and last 14 days.

Any Authority Nodes is able to vote for other Authority Nodes and Authority Node candidates. 
The following contraints are applied in network BIOS contract:

- Authority Node have maximum of 7 votes to be casted for different Authority Nodes

- Authority Node can't cast more than 1 vote for the same Node

- Authority Node can cast one vote for itself

- Authority Node can withdraw a vote from any node with immediate effect

- Withdrawed votes can be casted again only after 14 days vote cooldown period

After 14 days of voting for a new candidate Authority Node, decision is made based on received votes.
If by the end of voting period candidate received minimum of 3 votes from Authority Nodes AND is not added to the blacklist (see below), than candidate becomes Authority Node. 

*Additional rule to be implemented by upgrading BIOS contract in the near time:* 

If by the end of voting period candidate fits with ALL of the following:

- received minimum of 3 votes from Authority Nodes

- is not added to the blacklist (see below)

- current number of Authorty Nodes < 47 OR there is an Authority Node, which have less received votes than candidate node

Than candidate is promoted to Authority Node. 
If number of Authority Nodes = 47, than simulatneously existing Authority Node with lowest amount of received votes is excluded from Authority Nodes. 
This logic ensures that maximum number of Authority Nodes is limited with 47. 

***

Otherwise, candidate node is rejected and not promoted to Authority Node.

2. Blacklist
------------

Authority Node and candidate for Authority Node can be blacklisted by existing Authority Nodes. 

To add candidate or Authority Node to the blacklist, any Authority Node can create blacklist proposal and initiate proposal voting.
Voting period for blacklist proposal is 5 days, which enables ability of blacklisting for Authority Node candidates before candidate voting period of 14 days ends. 
Only Authority Nodes can cast votes in the blacklist voting.
Each Authority Node can cast 1 vote for the proposal.

After 5 days of blacklist proposal voting, proposal is deemed successful, if: 

- amount of votes for proposal is > 50% of Authority Nodes count 

Otherwise, proposal is rejected. 

If proposal is successful, Authority Node or Authority Node candidate is added to the blacklist.
Any node inlcuded into the blacklist can't be Authority Node. 

*Community blacklist to be implemented by upgrading BIOS contract in the near time:* 

Authority Node and candidate for Authority Node can be blacklisted by owners of PPR token stakes. 
Blacklist formed based on PPR token stake holders voting is called community blacklist. 

To add candidate or Authority Node to the blacklist, any owner of PPR token stake can create community blacklist proposal and initiate proposal voting by staking minimum amount of PPR tokens towards the proposal (minimum is to be determined). 

Voting period for community blacklist proposal is 5 days, which enables ability of blacklisting for Authority Node candidates before candidate voting period of 14 days ends. 
Only owners of PPR token stakes can cast votes in the community blacklist voting.
Each owner of PPR token stake can cast vote proportional to their token stake.
In case of voting for blacklist proposal stake withdrawal period for stake owner is increased to 5 days starting at the time of voting, so he can never vote twice in the same voting using the same stake. 
Each vote for community blacklist can be either positive (for) or negative (against). 

After 5 days of blacklist proposal voting, proposal is deemed successful, if: 
- amount of positive votes is bigger, than amount of negative votes
- total amount of votes is > 10% of total token stake owner votes possible in the network based on existing network-wide amount of token stakes (quorum)

If proposal is successful, Authority Node or Authority Node candidate is added to the community blacklist.
Any node inlcuded into the community blacklist can't be Authority Node. 

***

Changing BIOS contract parameters
------------------------------------------------------

BIOS contract refers to Papyrus Network User Agreement using its SHA-256 hash code, linking network operations with the agreement.

Parameters such as maximum amount of Authority Nodes or mining rewards are configured in BIOS contract as well.

Upon network launch Papyrus have ownership rights on BIOS contract and can override / reconfigure it in case of network issues. In the future Papyrus will surrender ownership of BIOS contract so that no party will be controlling it. 

To achieve decentralised governance, BIOS contract may be upgraded by supermajority decision of Authority Nodes, which is not objected by voting of the community of token stake owners. 

Implementation of this voting will be deployed to BIOS contract in the near time. 
 
Authority Nodes token reward recommendation
-------------------------------------------
 
To incentivize Authority Nodes participation, they shall receive token rewards for each block, which they include in the blockchain. With 1 seconds block interval it is recommended to set block reward at 1.5*K PPR tokens per block, where *K = {AMOUNT OF AUTHORITY NODES}/47*. It will keep annual inflation of PPR token supply under 5% for the network with 47 Authority Nodes, and it will avoid Authority Node reward dilution due to new nodes joining the network. As rewards aren’t diluted, Authority Nodes will be incentivized to propose new nodes inclusion to increase trust and adoption of the network, influencing token value. 

Governance attack considerations
--------------------------------

Network governance and resistance to attacks is considered sufficient, assuming that >50% of Authority Nodes are controlled by honest owners at all times.  
When amount of Authority Nodes in the network is between 5 and 47, three or more nodes can collude to include more their allies as nodes into the network with the idea of eventually getting control over 50%+ Authority Nodes and performing network attack. Assuming that honest Nodes represent at least 50% of the Authority Nodes at the moment of attack preparation suspicion, they shall blacklist proposed node candidates to tolerate potential attack.
In case of very unlikely situation, where network attack such as double spending is made by attackers, which manged to get control over more than 50% of Authority Nodes, token stake owners together with honest Authority Nodes can make hard fork of the blockchain and use media to distribute incident information and guides on necessary updates for network customers. 


