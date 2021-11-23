---
title: Exchange API/SDK
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

This tutorial explains how exchanges can use the Exchange service to send transactions.

## How to use
### 1.Start a Qitmeer node

* Docker  
  Follow [Qitmeer Installation](../qitmeer-installation) to install docker
* Build from Source  
  Follow [Qitmeer_GetStart](../../getstart) to build from Source
  
### 2.Start the Exchange service
```sh
git clone https://github.com/Qitmeer/exchange-lib.git
cd exchange-lib/exchange
go build
vim config.toml
```
```sh

[api]
# Configure the service listening port
listen="0.0.0.0:11360"  

# Qitmeer Node RPC
[rpc]
host="127.0.0.1:8131"
# If the node is configured with -notls, TLS = false
tls=true
admin="test"
password="test"

[sync]
# Start sync from block order
start=0
# How many confirmations UTXO are available
confirmations=5
# The address to be synchronized
address=[
    "TnNbgxLpoPJCLTcsJbHCzpzcHUouTtfbP8c",
    "TnU8gXq9xHFrfchwk2bjyGHR2HMswANsVU5",
]

[log]
# console=12 | file=11
mode=12
# debug=0 | info=1 | warn=2 | fail=3 | error=4 | email=5
level=0
# Log directory
path="logs"
```

```sh
./exchange
```
### 3.Create qitmeer address

* Create by exchange-lib, example
  
```go
import (
	"github.com/qitmeer/exchange-lib/address"
)

func createAddress() (string, error){
	ecPrivate, err := address.NewEcPrivateKey()
	if err != nil{
		return "", err
	}
	ecPublic, err := address.EcPrivateToPublic(ecPrivate)
	if err != nil{
		return "", err
	}
	return address.EcPublicToAddress(ecPublic, "mainnet")
}
```
* Create by qitmeer-js 
  
  Follow [qitmeer-js](../qitmeer-js) to create address

* Create by qx
  
  Follow [qxtools](../../reference/qxtools) to create address

### 4.Add an ADDRESS to the Exchange service

```sh
curl --location --request POST '127.0.0.1:11360/api/v1/address' \
--header 'Content-Type: application/json' \
--data-raw '{
    "address":"TnNbgxLpoPJCLTcsJbHCzpzcHUouTtfbP8c"
}'
```
### 5.Query the UTXO of an address
```sh
curl --location --request GET '127.0.0.1:11360/api/v1/utxo?address=TnNbgxLpoPJCLTcsJbHCzpzcHUouTtfbP8c' \
--header 'Content-Type: application/json'
```

```sh
{
  "code": 0,
  "msg": "ok",
  "rs": {
    "balance": 100000000000,
    "utxo": [
      {
        "txid": "b9abd7a213b490f088370dbc0d6eef8cd39541ac305cfae782b0b75ccb148b5f",
        "vout": 0,
        "address": "TnNbgxLpoPJCLTcsJbHCzpzcHUouTtfbP8c",
        "coin": "MEER",
        "amount": 50136986301,
        "spent": "",
        "height": 0,
        "lock": 0,
        "iscoinbase": true,
        "pkhex": "76a914785bfbf4ecad8b72f2582be83616c5d364a3244288ac"
      },
      {
        "txid": "b9abd7a213b490f088370dbc0d6eef8cd39541ac305cfae782b0b75ccb148b5f",
        "vout": 1,
        "address": "TnNbgxLpoPJCLTcsJbHCzpzcHUouTtfbP8c",
        "coin": "MEER",
        "amount": 49863013699,
        "spent": "",
        "height": 0,
        "lock": 0,
        "iscoinbase": true,
        "pkhex": "02400bb17576a914785bfbf4ecad8b72f2582be83616c5d364a3244288ac"
      }
    }
}
```

### 6.Create transaction example

```go
import (
    "github.com/Qitmeer/qitmeer/qx"
    "github.com/qitmeer/exchange-lib/exchange/db"
    "time"
)

func createTransaction(private string, utxos []db.UTXO, to string, amount int64) (string, error){
    var inputs []qx.Input
    var privateList, pkHexList []string
    var vinAmount int64 = 0
    var from string
    for _, utxo := range utxos{
        from = utxo.Address
        vinAmount += int64(utxo.Amount)
        inputs = append(inputs, qx.Input{
            TxID:     utxo.TxId,
            OutIndex: uint32(utxo.Vout),
        })
        privateList = append(privateList, private)
        pkHexList = append(pkHexList, utxo.PkHex)
        if vinAmount > amount{
            break
        }
    }
  
    outputs := map[string]qx.Amount{
        to: {
            TargetLockTime: 0,
            Value:          amount,
            Id:             0,
        },
    }
    txFees := (len(inputs) - 1 * 1600 + 2000 + (len(outputs) + 1) * 400) * 2
    change := vinAmount - amount - int64(txFees)
    outputs[from] = qx.Amount{
        TargetLockTime: 0,
        Value:          change,
        Id:             0,
    }
    now := time.Now()
    txRaw, err := qx.TxEncode(1, 0, &now, inputs, outputs)
    if err != nil{
          return "", err
    }
    return qx.TxSign(privateList, txRaw, "mainnet", pkHexList)
}

```

### 7.Send transaction

```sh
curl --location --request POST '127.0.0.1:11360/api/v2/transaction' \
--header 'Content-Type: application/json' \
--data-raw '{
    "raw":"0100000001029bf740dc1ddb2147c55d779ff3f1b171e2fc94e0efc489d064d5fbf4cc61dc01000000ffffffff02000000e1f505000000001976a914caf0e6f1e0b174131b33bba3ffb3510027230ff588ac0000331e420f000000001976a914caf0e6f1e0b174131b33bba3ffb3510027230ff588ac751f0200000000007aaf9161016a47304402202aaeb8227533bcbc7a5cba30e8ffffeb247c16b55671e9085f74c3ada648db3802200388b7db48f17626746e6d2f9c9fe571d3de17567d8d9bffca1797df0998b7e50121026c3f92961caa80e0b6a9f534040ac32c3c084cbff71897ff59ed6ac550b15228"
}'
```
