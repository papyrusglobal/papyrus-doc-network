Papyrus network on-boarding manual
==================================

Prerequisites
-------------

1. You need to have a machine capable of running ethereum client
   [geth](https://geth.ethereum.org/).

2. Your network firewall should allow connection to at least one TCP and UDP
   port. This manual uses port number 30301 but you can change it to any other
   number.

3.  You need docker installed on your machine.

    To quickly install docker on Ubuntu, follow these steps:

        curl -fsSL https://get.docker.com -o get-docker.sh
        sudo sh get-docker.sh

    I also recommend adding your user to the docker group so you can run
    following docker commands without sudo prefix.

        sudo usermod -aG docker $USER

    ⚠ Note that you need to log out all you existing sessions. Then log in
    again.


Run the node
------------

    sudo docker run -d --name=my-node -p 32303:32303 -p 32303:32303/udp papyrusglobal/geth-papyrus:test2-latest --port 32303 --ethstats='My node:ante litteram@head.papyrus.network:3500'

This command downloads and runs the docker container
"papyrusglobal/geth-papyrus:test-latest" that will use ports 30301/tcp and
30301/udp for peer communication and report statistics to public server as "My
node".

You may use standard docker commands (start/stop/rm/exec) to operate the
container. For example, to see logs, run `docker logs my-node`.

For more useful parameters that you may want to add, see sections below.


Statistics
----------

Network statistics is on http://status.papyrus.network. If you allowed stats
reporting (`--ethstats` option above), you should see your node there too.


Optional parameters
-------------------

You can use any geth command line options
(https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options).

I recommend the following useful additions to your command line:

To allow rpc interface, to use it for your application, consider adding the
following options:

    --rpc --rpcaddr='0.0.0.0'
    --rpccorsdomain="*"
⚠ Note that you need to add `-p 8545:8545` option to the docker part of the
command to expose the port to your machine network.

⚠ Note also that if you want to connect Metamask or other software from the
outside of your machine, make sure that your firewall accepts incoming
8545/tcp port connections. Port number may be changed with `--rpcport` option.

The same for websocket interface.

    --ws  --wsaddr='0.0.0.0'
    --wsorigins="*"
Same notes above apply to the default websocket port 8546/tcp.

To add much more verbose logs, add the following. Remember to remove this as
you don't need it anymore to save space.

    --verbosity=5


Commands
--------

To add a new account:

    docker exec -it my-node geth account new

Or to import the existing account:

    docker cp path/to/account.json my-node:/root/.ethereum/keystore/

To check accounts you have:

    docker exec -it my-node geth account list

To unlock the account the first account with password "password" for unlimited
time:

    docker exec -it my-node ./console.sh 'personal.unlockAccount(eth.accounts[0], "password", 0)'

To check the sealers, run:

    docker exec -it my-node ./console.sh 'papyrus.getSigners()'

To vote for the new sealer, run:

    docker exec -it my-node ./console.sh 'papyrus.propose("0x123...321", true)'

To start mining, using your first account for the coin-base, run:

    docker exec -it my-node ./console.sh 'miner.setEtherbase(eth.accounts[0]); miner.start()'
