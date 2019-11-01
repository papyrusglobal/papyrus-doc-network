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

Removal of Authority Node
-------------------------
Authority Node or candidate Node is removed and added to the authority nodes blacklist if other Authority Node proposes blacklisting of the Node and:

- a) quorum of >50% of Authority Nodes votes for the proposal keeps for 3 continuous days. 
- b) at least 50% of Authority Nodes vote in favor of blacklisting the Node for the same 3 continuous days.

Blacklisted nodes cannot become Authority Nodes again until they are removed from the authority nodes blacklist. Removal from the authority nodes blacklist may be performed by using the same approval process as for adding to the authority nodes blacklist.
Authority Node or candidate Node is removed and added to the stakeholders blacklist if token stakeholder propose blacklisting of the Node and: 

- a) quorum of >10% of staked token votes for the proposal keeps for 3 continuous days
- b) at least 50% of token votes are in favor of blacklisting the Node for the same 3 continuous days.

Blacklisted nodes cannot become Authority Nodes again until they are removed from the stakeholders blacklist. Removal from the stakeholders blacklist may be performed by using the same approval process as for adding to the stakeholders blacklist.
Authority Node is removed if

- a) current amount of Authority nodes is 47
- b) new Authority Node is being added
- c) the Node had the lowest average amount of votes for past 7 days period among Authority Nodes, where only votes from other Authority Nodes are counted.

Changing the maximum number of allowed Authority Nodes
------------------------------------------------------
Initial number of allowed Authority Nodes is 47. This number is used as parameter in the process of decision making for adding new Authority Node or removal of existing Authority Node. Token stakeholder can propose amending this number and it will be amended if

- a) quorum of >10% of staked token votes for the proposal keeps for 7 continuous days within 30 days period
- b) no fewer than 10% more Yes than No votes sustain for the same 7 continuous days within 30 days period. 

Changing token rewards for Authority Nodes. 
Token reward rules for Authority Nodes are defined within the protocol implemented at the launch of Papyrus Network. Token stakeholder can propose amending these rules and they will be amended if

- a) quorum of >10% of staked token votes for the proposal keeps for 7 continuous days within 30 days period
- b) no fewer than 10% more Yes than No votes sustain for the same 7 continuous days within 30 days period. 

Authority Nodes approval recommendation
---------------------------------------
 
It is recommended that Authority Node vote for other Authority Node approval only if it verified the following. 
Node is owned by specific registered business identity. Proof of ownership is provided in a form of information disclosure on the authorized website of business identity. For example, Node network address may be published on the website of business identity. Ownership of the website shall be verified as well using internet domain registry or other means. 
Owner of the node have proven good reputation in the business society. 
Node is compliant with technical requirements 
It is also recommended that Authority Node make a proposal and vote for proposal to blacklist other Authority Nodes or candidates as soon as it gets information that the Node violates recommended requirements.
 
Authority Nodes token reward recommendation
-------------------------------------------
 
To incentivize Authority Nodes participation, they shall receive token rewards for each block, which they include in the blockchain. With 1 seconds block interval it is recommended to set block reward at 1.5*K PPR tokens per block, where *K = {AMOUNT OF AUTHORITY NODES}/47*. It will keep annual inflation of PPR token supply under 5% for the network with 47 Authority Nodes, and it will avoid Authority Node reward dilution due to new nodes joining the network. As rewards aren’t diluted, Authority Nodes will be incentivized to propose new nodes inclusion to increase trust and adoption of the network, influencing token value. 
As network usage grow token holders may amend block reward amount by facilitation decision process, established by the Constitution.

Attack considerations
---------------------

Network governance and resistance to attacks is considered sufficient, assuming that >50% of Authority Nodes are controlled by honest owners at all times.  
When amount of Authority Nodes in the network is between 5 and 47, three or more nodes can collude to include more their allies as nodes into the network with the idea of eventually getting control over 50%+ Authority Nodes and performing network attack. Assuming that honest Nodes represent at least 50% of the Authority Nodes at the moment of attack preparation suspicion, they shall blacklist proposed node candidates to tolerate potential attack.
In case if network attack such as double spending under very unlikely situation, when attackers mange to get control of more than 50% of Authority Nodes, token stakeholders together with honest Nodes can make hard fork of the blockchain and use media resources to distribute information and updates on proper version of the network to network customers. 

Node requirements
-----------------
An Authority Node must be located on a server or virtual private server (VPS) running Linux with a fixed IP address. Servers should not be exposed to anything critical or high-risk vulnerabilities.
