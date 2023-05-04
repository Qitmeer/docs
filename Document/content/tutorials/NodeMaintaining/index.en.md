---
title: "Qitmeer Node Monitoring & Maintaining"
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# Qitmeer Node Monitoring & Maintaining


## Table of Contents

* [Checking Node Connectivity](#checking-onde-connectivity)
    * [Check if the P2P port and RPC port are open](#check-if-the-P2P-port-and-RPC-port-are-open)
    * [Check peer connection status](#check-peer-connection-status)
    * [Reload peer connections](#reload-peer-connections)
* [Check Node Synchronisation and Data Consistency](#check-node-synchronisation-and-data-consistency)
    * [BlockDAG Status Check](#blockDAG-status-check)
    * [EVM Status Check](#evm-status-check)
    * [Checking and handling tx pending situations](#checking-and-handling-tx-pending-situations)


## 1. Checking Node Connectivity

To ensure that nodes can participate properly in the network, provide transaction broadcast services, etc., checking the connectivity of nodes is essential to guarantee the stability and reliability of the network. The following are some common node connectivity checks:

### 1.1  Check if the P2P port and RPC port are open

Use command line tools or network monitoring tools to test port availability:

```bash
telnet 43.161.24.123 18130

Trying 43.161.24.123...
Connected to 43.161.24.123.
Escape character is '^]'.
/multistream/1.0.0
```

If the telnet ip p2pport command gives the result `/multistream/1.0.0`, the P2P port is open properly, otherwise, you need to check the firewall settings.

### 1.2  Check peer connection status

Ensuring that a node is connected to a sufficient number of peers increases the reliability, stability and security of the node to better serve the network. The more peers a node is connected to, the more stable the node's position in the network is and the faster it can receive and broadcast new blocks and transaction data. If a node does not have enough peers connected to it, the node may experience network delays or broken connections, resulting in the node not being able to synchronise the latest data in a timely manner.

Qitmeer provides peerinfo RPC for querying peer connections. There are two ways to make a request to this RPC:

- Initiate a JSON RPC request using the `curl` command

```bash
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"method":"getPeerInfo","params":[],"jsonrpc":"2.0","id":1}' https://127.0.0.1:18131 | jq '.result | length'

12
```

  This will give you the number of other peer nodes in the network that the node is currently connected to. Remove the `'.result | length'` to see the peer details.
  
  ⚠️Please replace `test:test` here with `rpcuser:rpcpass` in your own node configuration and `https://127.0.0.1:18131` with your own node `https://ip:rpcport`.

- Use the `cli.sh` RPC script provided by Qitmeer to initiate the request

The `cli.sh` script located in this directory ( https://github.com/Qitmeer/qng/tree/main/script ) makes it possible to initiate RPC requests more concisely.

```bash
./cli.sh -h 43.161.24.123 -p 18131 --user test --password test peerinfo | jq 'length'

12
```

  Similarly, you will need to configure your own node ip, rpcport, rpcuser, rpcpass. To make it easier to use it more often, you can create a separate `cli-mynode.sh` script (you can use the command `touch cli-mynode.sh`) and copy the following to the script:

```bash
#!/bin/bash
# the rpc config of your node 
host=43.161.24.123
port=18131
user=test
pass=test
./cli.sh -h "$host" -p "$port" --user "$user" --password "$pass" $@
 ```
  
In this way, you can directly use ./cli-mynode.sh peerinfo | jq 'length', e.g:

```bash
./cli-mynode.sh peerinfo | jq 'length'

12
```

⚠️ Make sure that `cli-mynode.sh` and `cli.sh` are in the same directory.

### 1.3  Reload peer connections

Qitmeer provides RPC `p2p_reloadPeers` for reloading peers. If your node's peer connection count stays very low for a long time, you can try resetting the peer connections. Two ways to do this:

- Using the `curl` method

```bash
curl -s -k -u test:test -X POST -H 'content-type: application/json' -d '{"jsonrpc":"2.0","method":"p2p_reloadPeers","params":[],"id":1}'  https://127.0.0.1:18131
```

- Using the `cli.sh` script

```bash
./cli.sh -p 18131 reloadpeers
or
./cli-mynode.sh reloadpeers
```

⚠️ To use the `reloadpeers` RPC, add the parameter `--modules=p2p` when the node is started.

## 2.  Check Node Synchronisation and Data Consistency

Data consistency is fundamental for nodes to provide proper blockchain services. Ensuring data consistency between a node and the whole network can prevent blockchain forks and abnormalities in the blockchain services of this node, or other problems, due to inconsistent node data.

The Qitmeer Network is EVM-compatible in the form of an underlying container, and there is linkage work between the BlockDAG data layer and the EVM data layer at the bottom of the network. Therefore, checking the state consistency of Qitmeer nodes requires two checks: blockdag state consistency check and evm state consistency check.

Once a deviation in state consistency is detected, the node data has been corrupted and the node needs to be recovered by performing one of the following actions:

- Execute the `"--cleanup"` operation to clear the data and resync

```bash
./qng --cleanup -A value(default: "/root/.qng")
For example:
./qng --cleanup --testnet -A .
```

- Recovery using data backup

### 2.1 BlockDAG Status Check

#### 2.1.1 BlockDAG synchronicity check

BlockDAG synchronisation checks check the synchronisation between a node's blockorder and multiple other peers. This can be done in two ways, mainly by checking the synchronisation of mainorder and mainheight in the following data:

- Using the `curl` method

```bash
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"method":"getNodeInfo","params":[],"jsonrpc":"2.0","id":1}' https://127.0.0.1:18131 | jq '.result.graphstate'

{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
```

```bash
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"method":"getPeerInfo","params":[],"jsonrpc":"2.0","id":1}' https://127.0.0.1:18131 | jq '.result|.[].graphstate'

{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
null
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
```

- Using the `cli.sh` script
 
 ```bash
 ./cli-mynode.sh nodeinfo |jq '.graphstate'
 
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
```

```bash
./cli-mynode.sh peerinfo | jq '.[].graphstate'

{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
null
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
{
  "tips": [
    "f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541 main"
  ],
  "mainorder": 59543,
  "mainheight": 51579,
  "layer": 51699
}
```

#### 2.1.2 BlockDAG data consistency check

The BlockDAG data consistency check checks the consistency of a node's blockhash with multiple other peers at the same blockorder height.

- Using the `curl` method

```bash
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"method":"getBlockByOrder","params":[59543, true, true, false],"jsonrpc":"2.0","id":1}'  https://127.0.0.1:18131 | jq '.result.hash'

"f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541"
```

Replace "59543" in "params" with the number of block orders you want to query to get the blockhash of the corresponding block.

- Using the `cli.sh` script

```bash
./cli-mynode.sh block 59543 | jq '.hash'
"f11a571165cefcf8fc61122cbe08c5c4e906324606eaf992ea1a391aa3467541"
```

Check the consistency of a node's BlockDAG data by comparing the consistency of this node's blockhash with that of other nodes.

### 2.2  EVM Status Check

In previous tests we have found that there is a probability that the EVM state may differ when the BlockDAG state is consistent, so checking the consistency of the EVM state is the most important part of the node state check. The EVM state consistency check focuses on the synchronization of EVM blockNumber, the consistency of blockhash and stateRoot of the same block, and the consistency of the transaction count of a given account.

We can query this interactively by going to the JavaScript console of the EVM, or we can query it via JSON RPC.

- QNG attach console

By executing the `qng attach` command, you can access the JavaScript console of the Qitmeer node EVM and query the EVM status of the node.

```bash
./qng attach http://127.0.0.1:18545
Welcome to the Geth JavaScript console!

 modules: admin:1.0 eth:1.0 rpc:1.0 txpool:1.0

To exit, press ctrl-d or type exit
> eth.blockNumber
48696
> eth.getBlockByNumber("48696").hash
"0x9977ed979b5e3d26d1cf98e865f53a613e2c44d9418c739d3d7f9ea6d024f9a8"
> eth.getBlockByNumber("48696").stateRoot
"0x89be6b57b6a14a6ed729e5c34dc8a49a37fc889e02cfe3be0474cf885b3a1b07"
> 
> exit
```

⚠️ Please replace `http://127.0.0.1:18545` with the EVM RPC interface of the node to be queried (`http://ip:rpcport` or the RPC domain).  You need to ensure that the EVM environment is configured `--evmenv` has the appropriate module and you can configure the EVM environment of the node like this: `--evmenv="--http --http.port=18545 --http.addr=0.0.0.0 --http.api=admin,web3,eth,qng,txpool"`。

We can perform the same operation on the common node or on other nodes for comparison purposes:

```bash
./qng attach https://rpc.evm.meerscan.io
Welcome to the Geth JavaScript console!

 modules: admin:1.0 debug:1.0 eth:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

To exit, press ctrl-d or type exit
> eth.blockNumber
526361
> eth.getBlockByNumber("526361").hash
"0x37ef8e5048706fb069cec97c529289a0eb6a92fdd9adfca720697e87fd3c3578"
> eth.getBlockByNumber("526361").stateRoot
"0x8d570b26d269d46d22cbac48ebb8385ec5ee2f6b1e58e29c8fb742067beb5965"
> 
> exit
```

- JSON RPC

  - get blockNumber
 
```bash
curl -s -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' http://127.0.0.1:18545 | jq '.result'
"0xbee6" // 48870
```

  - get block hash/stateRoot
  
```bash
curl -s -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0xbee6", false],"id":1}'  http://127.0.0.1:18545 | jq '.result.hash'
"0x9bf0093f9c0f26d56a81cab0a0a9b7cbebfa52515b51cf5ae42263945855870e"
```
 
```bash
curl -s -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0xbee6", false],"id":1}'  http://127.0.0.1:28545 |jq '.result.stateRoot'
"0x5a10eb1d39e2a43cd2a0b88485981d465ca06804964fca92e48034906aca187d"
```

⚠️ The "0xbee6" in the parameter `"params":["0xbee6", false]` is the hex format of the blockNumber, which can be converted using the toHex utility: `web3.toHex(48870) = "0xbee6"`.

### 2.3  Checking and handling tx pending situations

When we use a node to send a transaction that has been tx pending for a long time, other than the fact that the hash of the transaction is not available on other nodes, we need to check the status of the transaction in the txpool via the web3 backend to see if there are any nonce conflicts etc.

Here again, we need to use the `attach` command to access the JavaScript console and query the status of the node txpool. Use the `txpool.status` command to check the statistics of the number of pending and queued transactions. Use the `txpool.inspect` command to find out the status of the txpool.

The `txpool.inspect` command  gives you an object with two fields pending and queued. Each entry in these fields is a mapping of the nonce to the transaction summary string association. As there may be multiple transactions for the same account and nonce, for example a user broadcasting multiple transactions with different gas charges (or even completely different transactions), a queued situation may occur due to conflicting nonces.

```bash
./qng attach http://127.0.0.1:18545
Welcome to the Geth JavaScript console!

 modules: admin:1.0 eth:1.0 rpc:1.0 txpool:1.0 web3:1.0

To exit, press ctrl-d or type exit
> txpool.inspect
{
  pending: {
    0x35460b6973b3b51b273326b6ADFa2B0346af9Ec1: {
      291: "0xFEDBCdc8998dd86aB6FB5935BBC4BEe689F1D5B9: 0 wei + 450934 gas × 20000000000 wei"
    },
    0x4EA3a466630C00a712Fe18b2AC838010C45e2E72: {
      0: "0x227291F883eDDE3de683b0FA48Ecb7767f274d4E: 0 wei + 219595 gas × 20000000000 wei"
    },
    0xcCA1084c611418C4cc8688bc9207b8beE7c29b43: {
      31: "0x512b14c73a86858F238dDC96849B06970DB8081F: 0 wei + 1098690 gas × 20000000000 wei",
      32: "0xD74B5e30A2EaFBe4fBB4709f1A64Fe7D2B9Bc391: 0 wei + 1641080 gas × 20000000000 wei"
    },
    0xd1D9D236f0f059a2a9d193Ce5E46F3D668FE630a: {
      1266: "0xC69C4968F0A35b596689511014C8A44156d624f9: 0 wei + 1131800 gas × 20000000000 wei"
    }
  },
  queued: {
    0x0f6000de1578619320aba5e392706b131fb1de6f: {
      6: "0x8383534d0bcd0186d326c993031311c0ac0d9b2d: 9000000000000000000 wei + 21000 gas × 20000000000 wei"
    },
    0x5b30608c678e1ac464a8994c3b33e5cdf3497112: {
      6: "0x9773547e27f8303c87089dc42d9288aa2b9d8f06: 50000000000000000000 wei + 90000 gas × 50000000000 wei"
    },
    0x976a3fc5d6f7d259ebfb4cc2ae75115475e9867c: {
      3: "0x346fb27de7e7370008f5da379f74dd49f5f2f80f: 140000000000000000 wei + 90000 gas × 20000000000 wei"
    }
  }
}
> 
```
More detailed information on the use of txpool can be found in the documentation at： https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-txpool
