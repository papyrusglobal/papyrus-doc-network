Papyrus network introduction
=============================

There are many issues with governance paradigms used in other blockchain solutions, which lead to unacceptable level of centralization. For instance, EOS network is governed by Constitution and 21 Block Producers, which execute EOS protocol and are elected using dPoS mechanism. But voting thresholds to become elected BPs are low due to absence of quorum requirements, and power is consolidated in the hands of few people with significant token holdings and influence over BP decisions. Political systems, where power is consolidated in the hands of richest, are called plutocracy. In another dPoS network - TRON - situation is even worse, as not only BPs are elected by elite token holders with large stakes, but BPs are allowed to buy votes from token holders, and they spend their mining rewards to attract votes, instead of investments in better service and infrastructure. On the opposite, PoW networks have an issue with consolidation of power in large mining pools, controlling a significant percentage of network’s hashpower and effectively controlling the network itself. 

Our design goal in Papyrus Network was to construct governance protocol, which is aligned with Proof-of-Authority consensus for network scalability reasons, in a way to maintain greater level of decentralization and incentivize benefit of everyone: token holders, miners (authority nodes) and network customers (application developers and users). To achieve this goal we implemented flexible governance protocol, which somewhat reflects how corporations are managed in the modern world by shareholders and the board of directors. We believe that this is the best construction to be used as the network evolves and its usage grow, and also to stimulate this growth.

Constitution
------------

Constitution of Papyrus Network consists of the articles, accepted by default by all network participants (authority nodes, application developers, users). When anyone starts using the network, it is assumed that he is ready to work according to the Constitution and agreed network protocol. 

We found a good fit in EOS constitution and used it as a basis for Papyrus Network Constitution.

Articles
--------

This Constitution is a multi-party contract entered into by the Members by virtue of their use of Papyrus Network.

- Article I - No Initiation of Violence - Members shall not initiate violence or the threat of violence against another Member.

- Article II - No Perjury - Members shall be liable for losses caused by false or misleading attestations and shall forfeit any profit gained thereby.

- Article III - Rights - The Members grant the right of contract and of private property to each other, therefore no property shall change hands except with the consent of the owner, by a valid Arbitrator’s order, or via community referendum. This Constitution creates no positive rights for or between any Members.

- Article IV - No Vote Buying - No Member shall offer nor accept anything of value in exchange for a vote of any type, nor shall any Member unduly influence the vote of another.

- Article V - No Fiduciary - No Member nor PPR token holder shall have fiduciary responsibility to support the value of the PPR token. The Members do not authorize anyone to hold assets, borrow, nor contract on behalf of PPR token holders collectively. Papyrus Network blockchain has no owners, managers or fiduciaries.

- Article VI - Restitution - Each Member agrees that penalties for breach of contract may include, but are not limited to, fines, loss of account, and other restitution.

- Article VII - Open Source - Each Member who makes available a smart contract on Papyrus Network blockchain shall be a Developer. Each Developer shall offer their smart contracts via a free and open source licenses, and each smart contract shall be documented with a Ricardian Contract stating the intent of all parties and naming the Arbitration body that will resolve disputes arising from that contract.

- Article VIII - Language - Multilingual contracts must specify one prevailing language in case of dispute and the author of any translation shall be liable for losses due to their false, misleading, or ambiguous attested translations.

- Article IX - Dispute Resolution - All disputes arising out of or in connection with this Constitution shall be finally settled under the Rules of Arbitration of the International Chamber of Commerce by one or more arbitrators appointed in accordance with the said Rules.

- Article X - Choice of Law - Choice of law for disputes shall be, in order of precedence, this Constitution and the Maxims of Equity.

- Article XI - Amending - This Constitution and its subordinate documents can be amended by a general vote of the token holders with no less than 15% vote participation among tokens and no fewer than 10% more Yes than No votes, sustained for 15 continuous days within a 60 day period.

- Article XII - Publishing - Members may only publish information to the Blockchain that is within their right to publish. Furthermore, Members voluntarily consent for all Members to permanently and irrevocably retain a copy, analyze, and distribute all broadcast transactions and derivative information.

- Article XIII - Informed Consent - All service providers who produce tools to facilitate the construction and signing of transactions on behalf of other Members shall present to said other Members the full Ricardian contract terms of this Constitution and other referenced contracts. Service providers shall be liable for losses resulting from failure to disclose the full Ricardian contract terms to users.

- Article XIV - Severability - If any part of this Constitution is declared unenforceable or invalid, the remainder will continue to be valid and enforceable.

- Article XV - Termination of Agreement - A Member is automatically released from all revocable obligations under this Constitution 10 years after the last transaction signed by that Member is incorporated into the blockchain. After 10 years of inactivity an account may be put up for auction and the proceeds distributed to all Members according to the system contract provisions then in effect for such redistribution.

- Article XVI - Developer Liability - Members agree to hold software developers harmless for unintentional mistakes made in the expression of contractual intent, whether or not said mistakes were due to actual or perceived negligence.

- Article XVII - Consideration - All rights and obligations under this Constitution are mutual and reciprocal and of equally significant value and cost to all parties.

- Article XVIII - Acceptance - A contract is deemed accepted when a member signs a transaction and said transaction is incorporated into the blockchain according to the protocol.

- Article XIX - Counterparts - This Constitution may be executed in any number of counterparts, each of which when executed and delivered shall constitute a duplicate original, but all counterparts together shall constitute a single agreement.

- Article XX - Protocol - Members agree to use the protocol of communication and Papyrus Network maintenance, selected and implemented by Authority Nodes. Initial Authority Nodes represent those organizations and individuals, which decided to become first Members of the Papyrus Network and to launch the Network by implementing agreed network communication protocol. After the network is launched, Authority Nodes are able to add and remove Authority Nodes according to agreed protocol rules. As a general rule, approval of majority of Authority Nodes is required to change protocol rules, except for the rules listed in article XXI.

- Article XXI - Amending the protocol - Members agree to hold special decision making process for specific actions.

Adding new Authority Node
-------------------------

Any Authority Node can make proposal on adding new Authority Node to the network, which follows the approval process.
Any Authority Node can vote for proposed Authority Node candidate, if it is not blacklisted in either authority nodes blacklist or stakeholders blacklist. In total each Authority Node can vote for a maximum of 7 other Authority Nodes or candidates. Authority Node can move their votes from one Node to another at any time. 
Candidate Node becomes Authority Node if it keeps minimum 3 votes and holds in the top 47 Candidate and Authority Nodes by received votes number for continuous 7 days. Only votes from Authority Nodes are counted.    

Removal of Authority Node
-------------------------
Authority Node or candidate Node is removed and added to the authority nodes blacklist if other Authority Node proposes blacklisting of the Node and a) quorum of >50% of Authority Nodes votes for the proposal keeps for 3 continuous days; b) at least 50% of Authority Nodes vote in favor of blacklisting the Node for the same 3 continuous days. Blacklisted nodes cannot become Authority Nodes again until they are removed from the authority nodes blacklist. Removal from the authority nodes blacklist may be performed by using the same approval process as for adding to the authority nodes blacklist.
Authority Node or candidate Node is removed and added to the stakeholders blacklist if token stakeholder propose blacklisting of the Node and a) quorum of >10% of staked token votes for the proposal keeps for 3 continuous days; b) at least 50% of token votes are in favor of blacklisting the Node for the same 3 continuous days. Blacklisted nodes cannot become Authority Nodes again until they are removed from the stakeholders blacklist. Removal from the stakeholders blacklist may be performed by using the same approval process as for adding to the stakeholders blacklist.
Authority Node is removed if a) current amount of Authority nodes is 47; b) new Authority Node is being added; c) the Node had the lowest average amount of votes for past 7 days period among Authority Nodes, where only votes from other Authority Nodes are counted.

Changing the maximum number of allowed Authority Nodes
------------------------------------------------------
Initial number of allowed Authority Nodes is 47. This number is used as parameter in the process of decision making for adding new Authority Node or removal of existing Authority Node. Token stakeholder can propose amending this number and it will be amended if a) quorum of >10% of staked token votes for the proposal keeps for 7 continuous days within 30 days period; b) no fewer than 10% more Yes than No votes sustain for the same 7 continuous days within 30 days period. 
Changing token rewards for Authority Nodes. 
Token reward rules for Authority Nodes are defined within the protocol implemented at the launch of Papyrus Network. Token stakeholder can propose amending these rules and they will be amended if a) quorum of >10% of staked token votes for the proposal keeps for 7 continuous days within 30 days period; b) no fewer than 10% more Yes than No votes sustain for the same 7 continuous days within 30 days period. 

Authority Nodes approval recommendation
---------------------------------------
 
It is recommended that Authority Node vote for other Authority Node approval only if it verified the following. 
Node is owned by specific registered business identity. Proof of ownership is provided in a form of information disclosure on the authorized website of business identity. For example, Node network address may be published on the website of business identity. Ownership of the website shall be verified as well using internet domain registry or other means. 
Owner of the node have proven good reputation in the business society. 
Node is compliant with technical requirements 
It is also recommended that Authority Node make a proposal and vote for proposal to blacklist other Authority Nodes or candidates as soon as it gets information that the Node violates recommended requirements.
 
Authority Nodes token reward recommendation
-------------------------------------------
 
To incentivize Authority Nodes participation, they shall receive token rewards for each block, which they include in the blockchain. With 3 seconds block interval it is recommended to set block reward at 5*K PPR tokens per block, where K = {AMOUNT OF AUTHORITY NODES}/47. It will keep annual inflation of PPR token supply at ~5% for the network with 47 Authority Nodes, and it will avoid Authority Node reward dilution due to new nodes joining the network. As rewards aren’t diluted, Authority Nodes will be incentivized to propose new nodes inclusion to increase trust and adoption of the network, influencing token value. 
As network usage grow token holders may amend block reward amount by facilitation decision process, established by the Constitution.

Attack considerations
---------------------

Network governance and resistance to attacks is considered sufficient, assuming that >50% of Authority Nodes are controlled by honest owners at all times.  
When amount of Authority Nodes in the network is between 5 and 47, three or more nodes can collude to include more their allies as nodes into the network with the idea of eventually getting control over 50%+ Authority Nodes and performing network attack. Assuming that honest Nodes represent at least 50% of the Authority Nodes at the moment of attack preparation suspicion, they shall blacklist proposed node candidates to tolerate potential attack.
In case if network attack such as double spending under very unlikely situation, when attackers mange to get control of more than 50% of Authority Nodes, token stakeholders together with honest Nodes can make hard fork of the blockchain and use media resources to distribute information and updates on proper version of the network to network customers. 

Add Admin grants & possibility to change bios contract
------------------------------------------------------
