BIOS Contract
=============

Overview
--------

``Bios.sol`` - is the main kernel smartcontract with all the logic about consensus, staking and voting. Its based on the ``QueueHelper`` that brings queue implementation code.
Latest version of the Bios contact you can always  `find in our repo <https://github.com/papyrusglobal/papyrus/blob/master/papyrus-stuff/contracts/Bios.sol>`_

BIOS Addresses
--------------

To track the current address of the Bios contract, there is a
[Versioner](Versioner.sol) contract located at fixed address
`0x0000000000000000000000000000000000000022`. To query it for the Bios contract
address, use `bios` public method. Here is an example in javascript:

.. code-block:: javascript

    const versionerAbi = [
      {
        constant: true,
        inputs: [],
        name: 'bios',
        outputs: [{ name: '', type: 'address' }],
        payable: false,
        stateMutability: 'view',
        type: 'function'
      }
    ];
    const versionerAddress = '0x0000000000000000000000000000000000000022';
    const versioner = new web3.eth.Contract(versionerAbi, versionerAddress);
    const biosAddress = await versioner.methods.bios().call({ from: account });

Note that the resulting address may be zero, this means that the Bios contract
is not yet installed.

BIOS Usages examples
--------------------

Let's take a look at the simple example of Javascript code that will get all authorities nodes from our BIOS contract.

.. code-block:: javascript
      :emphasize-lines: 2, 7, 15

        const { eth } = require('./web3relay');
        const ABI = require('../abi/bios');
        const { getConfig } = require('../utils');

        const config = getConfig();
        if (!config.biosAddress) throw new Error('Setup config.biosAddres');
        const contract = new eth.Contract(ABI, config.biosAddress);

        module.exports = function (req, res) {
          if (typeof contract.methods.getAuthorities !== 'function') {
            console.error('Contract method \'getAuthorities\' not found', err);
            res.send([]);
            res.end();
          }
          contract.methods.getAuthorities().call()
            .then(authorities => {
              res.send(authorities);
              res.end();
            })
            .catch(err => {
              console.error('Can\'t get authorities from contract. Silently return empty array', err);
              res.send([]);
              res.end();
            })
        };


If you are interested to see more examples how to call BIOS contact API you could check our API documentation sections for example - `Voting API <https://papyrus-network.readthedocs.io/en/latest/doc/api/api-staking.html#api-usage-example>`_
