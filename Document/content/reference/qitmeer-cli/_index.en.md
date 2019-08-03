---
title: "qitmeer-cli"
date: 2019-07-29T00:38:09+08:00
weight: 0
---

## qitmeer-cli



### Usage


The command line utility of Qitmeer and Qitmeer-wallet.

Configuration file config.toml will be made automatically

### download or build

you can download the compiled binary version.

[download](https://github.com/HalalChain/qitmeer-cli/releases)

if you have go environment,you can also build it by yourself.
```
git clone https://github.com/HalalChain/qitmeer-cli.git

cd qitmeer-cli

go build
 
```

### Command list
```

Usage:
qitmeer-cli [command]

block Commands:
	getBlockCount        getBlockCount; count all synchronous blocks
	getBlockHash         getBlockHash {number}; get block hash by number
	getBlock             getBlock {number|hash} [verbose]; verbose: defalut true,show block detail,get block by number or hash
	getBlockHashByRange  getBlockHashByRange {start} {end};Return the hash range of block from 'start' to 'end'(exclude self)
	getBlockByOrder      getBlockByOrder {order} {fullTx}
	getBestBlockHash     getBestBlockHash
	getBlockHeader       getBlockHeader {number|hash} [verbose];verbose:bool,show detail,defalut true; get block by number or hash
	isOnMainChain        isOnMainChain {hash}; query whether a given block is on the main chain
	getMainChainHeight   getMainChainHeight
	getBlockWeight       getBlockWeight

blockChain Commands:
	createRawTransaction createRawTx {inTxid:vout}... {toAddr:amount}... {lockTime},crate raw transaction
	getRawTransaction    getRawTransaction {tx_hash} [verbose]; verbose: bool,show detail,defalut true
	decodeRawTransaction decodeRawTransaction {raw_tx}
	sendRawTransaction   sendRawTransaction {sign_raw_tx} {allow_high_fee}; allow_high_fee: default false; send sing_raw_tx to network
	txSign               txSign {private_key} {raw_tx}; sign rawTx
	getUtxo              getUtxo {tx_hash} {vout} [include_mempool]; vout:index of the output; include_mempool: default=true,include the mempool , get information about an unspent transaction output
	getNodeInfo          getNodeInfo
	getPeerInfo          getPeerInfo

mempool Commands:
	getMempool           getMempool [type] [verbose]; type: defalut regular; verbose: bool ; get mempool info

miner Commands:
	generate             generate {number}, cpu mine {number} blocks
	getBlockTemplate     getBlockTemplate; get new block work to mine
	submitBlock          submitBlock {blockHex}; broadcast mine block to network

Flags:
      --cert string        RPC server certificate file path
  -c, --config string      config file path (default "cli.toml")
      --debug              debug print log
      --format             print json format
  -h, --help               help for qitmeer-cli
      --notls              Do not verify tls certificates (not recommended!) (default true)
  -P, --password string    RPC password
      --proxy string       Connect via SOCKS5 proxy (eg. 127.0.0.1:9050)
      --proxypass string   Password for proxy server
      --proxyuser string   Username for proxy server
  -s, --server string      RPC server to connect to (default "127.0.0.1:18131")
      --skipverify         Do not verify tls certificates (not recommended!) (default true)
      --timeout string     rpc timeout,s:second h:hour m:minute (default "30s")
  -u, --user string        RPC username

Use "qitmeer-cli [command] --help" for more information about a command.
		
```

### Options

```
  -h, --help   help for qitmeer-cli
```

### SEE ALSO

* [block](/en/reference/qitmeer-cli/block/)	 
* [blockChain](/en/reference/qitmeer-cli/blockchain/)	 
* [mempool](/en/reference/qitmeer-cli/mempool/)	 
* [miner](/en/reference/qitmeer-cli/miner/)	 

