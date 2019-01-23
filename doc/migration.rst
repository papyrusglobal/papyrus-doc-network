Migration
===================

How to migrate smart contract from Ethereum
-------------

Before making any transaction (including deploy of a new contract), user need
to have its address staked.

For staking addresses we have a contract at address
`0x0000000000000000000000000000000000000022`. It source is
[here](contracts/papyrus.sol).

To check that the address is already staked and can be used to make
transactions, call `IsFrozen` method with the address as the argument.

To stake the current address, call `freeze` method with no parameters. After
that, all its balance will become unavailable for any subsequent transactions
that try to decrease it. And after the `freezeGap` time, the address will
be staked.

To stop staking and resume the ability to use the balance, call `unfreeze`
from that account and wait `freezeGap` time.
