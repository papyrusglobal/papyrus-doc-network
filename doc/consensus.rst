Consensus
=========

Papyrus Network is a distributed computing system, where network nodes has to agree on transactions, before they are included in the distributed ledger, to maintain synchronized copies of the ledger and avoid inappropriate transactions. How network nodes reach the agreement is determined by consensus protocol, deisgned with the goal to maintain system reliability in the presence of a number of faulty processes. 

Assumptions used in Papyrus Network design

* Cost of network protocol manipulation should exceed potential benefit for an attacker;

* If total amount of value stored in the network is X, than cost of an attack on the network should be >X; 

* Economy processes within the network is complemented with economy processes outside the network:

 * poor behaviour of network node owned by some business entity, may be covered in the media and cause reputational damage to the entity's other businesses, leading to its financial losses;

 * attack on the network by a group of network nodes will cause their removal from the network and possible hard fork, meaning that they will lose ability to receive mining rewards in the network;  

* There are governance rules, initially established as constitutional for the network, which require agreement not only between network nodes, but also between token holders, to change protocol;

* Technically collusion/agreement between minimum of >50% of active network nodes should be required to manipulate/change the protocol, but it is not enough to run a successful attack, as it will be detected and considered as constitution violation, if change was not approved by token holders according to established policy.

Keeping in mind these assumptions we developed a Proof-of-Authority consensus for Papyrus Network, which have the following features:

* Network nodes allowed to participate in consensus protocol for network transactions confirmation are called Authority Nodes;

* Amount of Authority Nodes is allowed to be in a range of 5 to 47 nodes, upper limit of 47 is chosen as reasonable to avoid excessive infrastructure cost, while keeping network security at high level;

* We use the same logic as in EIP225 ( https://eips.ethereum.org/EIPS/eip-225 ) Clique consensus to reach an agreement between Authority Nodes, but change the voting logic to elect Authority Nodes (see http://docs.papyrus.network/en/latest/doc/network_architecture.html for more details).

