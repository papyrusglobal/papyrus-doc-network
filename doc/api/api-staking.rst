API: Staking
===========

Contract overview
-----------------

``Bios.sol`` - is the main kernel smartcontract with all the logic about consensus and staking. Its based on the ``QueueHelper`` that brings queue implementation code.
    

Functions
---------

- **function freeze() payable public**
Stake the specified amount of tokens.
The value is on the contract account and thus inaccessible to the sender.
``Input parameter`` : "msg.value" the value to be staked.
``Output parameter`` : none


- **function melt(uint224 val) public**
Unstake the specified value of tokens.
The value is put to the melting queue and can be withdrawn after `freezeGap`.
``Input parameter`` : "val" - value to unstake.
``Output parameter`` : none

- **function withdraw() public**
Withdraw the previously unstaked amount of tokens provided the `freezeGap` time had passed since its unstake.
Every 'unstake' call must match 'withdraw' call.
Takes the latest melting queue element and transfers its tokens amoun to the sender's account.
``Input parameter`` : none
``Output parameter`` : none

- **function getFreeMeltingSlots() view public returns (uint8)**
Service function, calculates the number of queue elements (slots) is aviable in the melting conveyer for the sender's account.
Every unstake call consumes a slot, every withdrawal releases it.
``Input parameter`` : none
``Output parameter`` : uint8 - slots number

- **function getMeltingHead() view public returns (uint224 stake, uint32 timestamp)**
Service function, calculates the latest melting conveyer slot to bewithdrawn first.
Return Stake and timestamp pair, where stake is the amount of money unstaked and timestamp is the time of the unstake call.
``Input parameter`` : none
``Output parameter`` : uint8 - stake
``Output parameter`` : uint8 - timestamp

API Usage Example
-----------------

Below you can see typical JS example of usage ``Bios.sol`` smartcontract.

.. code-block:: javascript
      :emphasize-lines: 17, 20, 23 

        const gatewayUrl = 'http://148.251.152.112:18545/';  // url to the Papyrus testnet
        const biosAddress = '0x142ac51e2b05a107c1482f4832b73c5bc55b6fd5'; // Address of the Bios contract in the network 

        const ether = 10 ** 18;
        let contract;
        let account;
        let web3;

        web3 = new Web3(window.web3.currentProvider);
        const accounts = await web3.eth.getAccounts();
        account = accounts[0];
        const netId = await web3.eth.net.getId();
        const balance = await web3.eth.getBalance(account);
        contract = new web3.eth.Contract(abi, biosAddress);
        
        //lets freeze some tokens
        contract.methods.freeze().send({ from: account, gas: 0, value })
        
        //lets unfreeze some tokens
        contract.methods.melt(value).send({ from: account, gas: 0 })
        
        //After freeze gap time - lets unfreeze our tokens
        contract.methods.withdraw().send({ from: account, gas: 100000 })
       
