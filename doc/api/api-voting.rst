API: Voting
===========

Contract overview
-----------------

``Bios.sol`` - is the main kernel smartcontract with all the logic about consensus, staking and voting. Its based on the ``QueueHelper`` that brings queue implementation code.

Voting mechanism consists of two parts - firs is "proposal call" that initiates possibility for voting for any change for other participants (for instance - adding new Authority node or Bios contract changing etc).
After that voting begins and in the in a certain period of time Authority Nodes could vote for any active initiatives.    

Proposal Functions
------------------

- **function proposeNewAuthority(address participant) public**
Propose a poll for a new authority.
``Input parameter`` : "address participant" - the address of the new Autority Node. 
``Output parameter`` : none

- **function proposeBlacklistAuthority(address participant) public**
Propose a poll for blacklisting the authority to the authority black list.
``Input parameter`` : "address participant" - the address of the Autority Node that should be added to the black list. 
``Output parameter`` : none

Proposal Examples
-----------------

Below you can see JS example of usage ``Bios.sol`` smartcontract from the Papyrus Wallet implemetatin

.. code-block:: javascript
      :emphasize-lines: 3, 14
      
    async proposeNewAuthority(address, callbacks = {}) {
	    return this.process(
	      this.contract.methods.proposeNewAuthority(address).send({
	        from: this.account,
	        gas: 100000
	      }),
	      callbacks
	    );
  	}

    async proposeBlacklistAuthority(address, callbacks = {}) {
	    return this.process(
	      this.contract.methods.proposeBlacklistAuthority(address).send({
	        from: this.account,
	        gas: 100000
	      }),
	      callbacks
	    );
 	}


Voting Functions
----------------

- **function voteForNewAuthority(uint slot, address participant) public**
Function that could be called by existing Authority Vote for the voting for the new Authority Node
``Input parameter`` : "slot" - number of voting slot to bet.
``Input parameter`` : "participant" - address of the proposed authority.
``Output parameter`` : none

- **function voteForBlackListAuthority(address participant) public**
Function that could be called by existing Authority Vote for the voting for the adding another Authority Node to the blacklist
``Input parameter`` : "slot" - number of voting slot to bet.
``Input parameter`` : "participant" - address of the proposed authority.
``Output parameter`` : none

- **function handleClosedPolls() public**
Handle all pollings where time is up. Anybody could call this function.
``Input parameter`` : none
``Output parameter`` : none


Voting Examples
---------------

.. code-block:: javascript
      :emphasize-lines: 3, 14

	import Web3 from 'web3';
	import abi from '@/abis/abi.json';

	const noop = () => {};
	const cbCaller = function(fn, ...args) {
	  if (fn && typeof fn === 'function') {
	    fn(...args);
	  }
	};

	export class Web3Service {
	web3 = null;
	contract = null;
	provider = null;
	account = null;

	constructor(provider) {
		this.provider = provider;
	    this.web3 = new Web3(provider);
	    this.contract = new this.web3.eth.Contract(
	    	abi,
	    	process.env.VUE_APP_BIOS_ADDRESS
	    );
	}

	async voteForNewAuthority(votes, address, callbacks = {}) {
	    return this.process(
	    	this.contract.methods.voteForNewAuthority(votes, address).send({
	       		from: this.account,
	        	gas: 100000
	    	}),
	    	callbacks
	    );
	}

	async voteForBlackListAuthority(address, callbacks = {}) {
	    return this.process(
	      this.contract.methods.voteForBlackListAuthority(address).send({
	      		from: this.account,
	      		gas: 100000
	    	}),
	    	callbacks
	    );
	}        

