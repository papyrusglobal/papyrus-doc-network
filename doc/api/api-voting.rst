API: Voting
===========

Contract overview
-----------------

``Bios.sol`` - is the main kernel smartcontract with all the logic about consensus and staking. Its based on the ``QueueHelper`` that brings queue implementation code.

its global variables defined as follows:

.. container:: codeset

   .. sourcecode:: solidity

    uint32 constant freezeGap = 5 seconds;   // time gap before withdrawing melted stake

    /// Public data shared with client code.
    mapping(address=>uint) public stakes;    // stakes map reside in slot #0
    address[] public sealers;                // sealers array reside in slot #1

    /// Public contract state.
    uint constant public version = 1;        // contract code version
    mapping(address=>Queue) public melting;  // melting stakes queues
    

Functions
---------

- **function freeze() payable public**
Stake the specified amount of money.
The value is on the contract account and thus inaccessible to the sender.
Input parameter: "msg.value" the value to be staked.


- **function melt(uint224 val) public**
Unstake the specified value of money.
The value is put to the melting queue and can be withdrawn after `freezeGap`.
Input parameter: "val" - value to unstake.


- **function withdraw() public**
Withdraw the previously unstaked amount of money provided the `freezeGap` time had passed since its unstake.
Every 'unstake' call must match 'withdraw' call.
Takes the latest melting queue element and transfers its money amoun to the sender's account.


- **function getFreeMeltingSlots() view public returns (uint8)**
Service function, calculates the number of queue elements (slots) is aviable in the melting conveyer for the sender's account.
Every unstake call consumes a slot, every withdrawal releases it.


- **function getMeltingHead() view public returns (uint224 stake, uint32 timestamp)**
Service function, calculates the latest melting conveyer slot to bewithdrawn first.
Return Stake and timestamp pair, where stake is the amount of money unstaked and timestamp is the time of the unstake call.
