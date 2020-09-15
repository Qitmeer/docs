---
title: Qitmeer Wallet JSON RPC 
weight: 6
---

## Qitmeer Wallet JSON RPC 命令列表

### Wallet
  - [unlock](unlock)
  - [lock](lock)
  - [getAccountsAndBalance](getAccountsAndBalance)
  - [createAccount](createAccount)
  - [getAddressesByAccount](getAddressesByAccount)
  - [createAddress](createAddress)
  - [sendToAddressByAccount](sendToAddressByAccount)
  - [getTxListByAddr](getTxListByAddr)
  - [importWifPrivKey](importWifPrivKey)
  - [dumpPrivKey](dumpPrivKey)
  - [syncStats](syncStats)
  - [getUtxo](getUtxo)
  - [importPrivKey](importPrivKey)
  - [getBalanceByAddr](getBalanceByAddr)
  - [sendToAddressBatch](sendToAddressBatch)


### UI
  - [openWallet](openWallet)

## Qitmeer-wallet RPC Reference

Download Qitmeer Wallet from [github.com/Qitmeer/qitmeer-wallet](https://github.com/Qitmeer/qitmeer-wallet)

```sh
# run rpc or ul model  will support rpc interface

./qitmeer-wallet web
```

Usage: 

RPC interface URL http://127.0.0.1:38130/api

```sh

curl -k -u "user:password" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_createAccount","params":["account"],"id":1}' http://127.0.0.1:38130/api | jq
```
