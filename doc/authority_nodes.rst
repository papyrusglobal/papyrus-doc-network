Authority Nodes
===============

Papyrus Network is operated by Authority Nodes, which provide their hardware capacities to run Papyrus Network software, which implements Papyrus Network protocol. Authority Nodes are operated by identified business entities and are elected by other Authority Nodes according to established network governance model (see http://docs.papyrus.network/en/latest/doc/network_architecture.html for more details).

Papyrus Network protocol allows up to 47 Authority Nodes to be a part of the network.

In exchange for maintaining network operations Authority Nodes get mining rewards equal to 1.5*K PPR tokens per block, where K = {AMOUNT OF AUTHORITY NODES}/47. 
This formula ensures that existing Authority Nodes will keep receiving same amount of daily/monthly rewards with the growth of amount of Authority Nodes in the network. 
It fact, Authority Nodes are incentivised to make network more decentralised and invite new nodes to the network without losing own rewards.

PPR token is a native token of Papyrus Network required to allocate network resources to execute transactions. 
There are 1 000 000 000 PPR tokens distributed at the genesis block, and according to mining rewards schedule with 1 second block interval annual inflation is limited with a maximum amount of new tokens equal to (60 blocks per minute)*60*24*365*1.5*(47/47)= 47 304 000 PPR, ie ~ 4.7% of total emission.

Mining rewards are subject to change only based on community voting (see Governance documentation).

Initially Papyrus Network mainnet is launched with 5 Authority Nodes chosen by Papyrus. 
Papyrus audits each current and potential node owner entity's mission, executive leadership, net annual revenue, number of full-time employees, years in business, organizational structure, and the industry they are a part of. 

After the launch Authority Nodes election procedures are activated, network governance becomes decentralised and existing Authority Nodes are able to elect new Authority Nodes. 

It is strongly recommended in the interest of network reliability that existing Authority Nodes do a regular audit of current and potential Authority Node owner entity's mission, executive leadership, net annual revenue, number of full-time employees, years in business, organizational structure, and the industry they are a part of.
In case of doubt in other Authority Node reliability, Authority Nodes should use BIOS Contract to set a vote on adding suspicious Nodes to the Blacklist. 
Papyrus Wallet and Papyrus Explorer support necessary functionality. 

If you would like to run an Authority Node and receive mining rewards in Papyrus Network, you can apply here: 
https://papyrusglobal.typeform.com/to/Va9wX5

Instruction on how to set up a node can be found here:
https://github.com/papyrusglobal/papyrus

**Recommended Authority Node configuration:**

CPU - Intel® Core™ i7 or more powerful

RAM: 64Gb+

Hard drive: 512Gb+ (SSD recommended)

Connection: 100 MBit/s+ port

**Expected Authority Node rewards:**

Expected monthly PPR reward for active Authority Node is equal to 60*60*24*30*(K/47)*(1.5/K) = ~82,723 PPR

