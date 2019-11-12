Papyrus Network key facts
=========================

This section presents key variables of Papyrus Network setup, which dApp developers need to know. 

ChainId = 32328

Block interval = 1s

Native token for resource allocation = PPR

Native token emission at genesis block = 1000000000 PPR

Mining rewards = (1.5 * A) / 47 PPR per mined block, where A equals to the count of Authority Nodes


Block gas limit = 210284448

Unstaking lock period = 3 * 24 hours

Maximum gas allocation allowed for an address for X PPR stake = 3 * 24 * X in wei * blockGasLimit * 60 * 60 / (totalStake 
in wei + X in wei), 
where blockGasLimit = block gas limit, totalStake = total amount of PPRs staked before new stake (X) happened

Hourly gas allocation for an address for X PPR stake = X in wei * blockGasLimit * 60 * 60 / (totalStake in wei + X in wei), 
where blockGasLimit = block gas limit, totalStake = total amount of PPRs staked before new stake (X) happened


New Authority Node voting period = 14 days

Authority Node blacklist voting period = 5 days

Minimum votes required for Authority Node candidate approval = 3 

Maximum number of Authority Nodes and candidates each Authority Nodes can vote for = 7

Vote withdrawal lock period = 14 days

BIOS contract versioner address = 0x0000000000000000000000000000000000000022
(see http://docs.papyrus.network/en/latest/doc/api/api-bios.html)

Actual version of BIOS contract: 
https://github.com/papyrusglobal/papyrus/blob/master/papyrus-stuff/contracts/Bios.sol

Actual version of Papyrus Network User Agreement: 
https://github.com/papyrusglobal/papyrus/blob/master/PNUA

SHA-256 hash of Papyrus Network User Agreement verifiable in network BIOS contract:
0x5c366dc1ffa995d93fae49888f1283d5e8429a372757f43af315a79e84cd1583

Network explorer provided by Papyrus:

https://explorer.papyrus.network

MetaMask wallet extension for token staking and Authority Nodes voting provided by Papyrus:

https://wallet.papyrus.network

Network status page:

https://status.papyrus.network

HTTP RPC gateways provided by Papyrus:

https://gateway.papyrus.network

https://gateway2.papyrus.network
