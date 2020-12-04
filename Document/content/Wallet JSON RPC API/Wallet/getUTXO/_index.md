---
title: getUtxo
weight: 3
---

## wallet_getUtxo
get UTXOs of specific address

### Parameters
1. `addr: (string)` address

### Returns

### Example
#### Request
```sh
$ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getUTxo","params":["Tme9dVJ4GeWRninBygrA6oDwCAGYbBvNxY7"],"id":1}' http://127.0.0.1:8130/api |jq .

```
#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    {
      "TxId": "6838ccafe8747007e9dcb918852833d5867ca4cdf5e48e2c419c0ff61927403b",
      "Index": 0,
      "Amount": 100000000
    },
    {
      "TxId": "83f481422d30ad3587afa78c36e1a2d29a28813528ad24f347c5845c32148ade",
      "Index": 1,
      "Amount": 676344792042
    }
  ]
}
```