BIOS Contract
=============

Overview
--------

``Bios.sol`` - is the main kernel smartcontract with all the logic about consensus, staking and voting. Its based on the ``QueueHelper`` that brings queue implementation code.
Latest version of the Bios contact you can always  `find in our repo <https://github.com/papyrusglobal/papyrus/blob/master/papyrus-stuff/contracts/Bios.sol>`_

BIOS Addresses
--------------

Testnet BIOS address : `0x8f98d0aa9b01e7d15a7950db68b26b89d6f1be14 <http://explorer-testnet.papyrus.network/addr/0x8f98d0aa9b01e7d15a7950db68b26b89d6f1be14#tab_addr_1>`_

Testnet `BIOS Abi <https://github.com/papyrusglobal/explorer/blob/master/abi/bios.json>`_  

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

