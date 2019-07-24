---
title: Qitmeer-cli 
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

## Qitmeer-cli user guide
***qitmeer-cli*** is a command-line tool that allows you to send RPC commands to the ***qitmeer*** network from the command line. 

## Prerequisites

Update Go to version at least 1.12 (required >= **1.12**)

Check your golang version

```shell
$ go version
go version go1.12 darwin/amd64
```

## How to build

```shell
$ mkdir -p /tmp/work
$ cd /tmp/work
$ git clone https://github.com/HalalChain/qitmeer-cli.git
$ cd qitmeer-cli
$ go build

```

## Qitmeer Commands

```shell
$ ./qitmeer-cli --help
qitmeer cli is a RPC tool for the qitmeer network

Usage:
  qitmeer-cli [command]

Available Commands:
  createrawtransaction createRawTransaction
  decoderawtransaction decodeRawTransaction
  generate             generate {n}, cpu mine n blocks
  getUtxo              getUtxo tx_hash vout include_mempool,
  getblock             get block by number or hash
  getblockcount        get block count
  getblockhash         get block hash by number
  getblocktemplate     getblocktemplate
  getmempool           get mempool
  getrawtransaction    getrawtransaction
  help                 Help about any command
  sendrawtransaction   sendRawTransaction
  txSign               txSign private_key raw_tx

Flags:
      --cert string        RPC server certificate file path
  -c, --config string      config file path (default "config.toml")
      --debug              debug print log
  -h, --help               help for qitmeer-cli
      --notls              Do not verify tls certificates (not recommended!) (default true)
  -P, --password string    RPC password
      --proxy string       Connect via SOCKS5 proxy (eg. 127.0.0.1:9050)
      --proxypass string   Password for proxy server
      --proxyuser string   Username for proxy server
  -s, --server string      RPC server to connect to (default "127.0.0.1:18131")
      --simnet             Connect to the simulation test network
      --skipverify         Do not verify tls certificates (not recommended!) (default true)
      --testnet            Connect to testnet
      --timeout string     rpc timeout,s:second h:hour m:minute (default "30s")
  -u, --user string        RPC username

Use "qitmeer-cli [command] --help" for more information about a command.
```

