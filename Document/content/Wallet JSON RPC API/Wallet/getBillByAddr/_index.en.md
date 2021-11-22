---
title: getBillByAddr
weight: 3
---

### wallet_getBillByAddr
request the bill of a specific address, a bill is the log of payments, which are the effects that a transaction makes on a specific address a payment can affect only ONE address

#### Parameters
1. `addr: (string)` address
2. `filter: (numeric)`  filter 
    * `0` received payments
    * `1` sent payments
    * `2` all payments
3. `page: (numeric)`   page number
    * `0` all pages
4. `page size: (numeric, 10)`   page size
    * `0` use default page size 10

#### Returns
`transactions: (array of TRANSACTION)` 

##### TRANSACTION
`hex: (hex string)`  raw transaction 
`txid: (hex string)`  transaction ID
`txhash: (hex string)`  transaction hash (differs from txid for witness transactions)
`size: (numeric)`   size in byte
`version: (numeric)`  version, used to check if protocol matches 

#### Example
##### Request
```sh
$ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getTxListByAddr","params":["TmbC1Fx1UXNt7D6zpaj83UrAEW7MbcUWuQz", 2, 0, 0 ],"id":1}' http://127.0.0.1:8130/api |jq .

```
##### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "total": 1,
    "page": 0,
    "page_size": 0,
    "transactions": [
      {
        "hex": "0100000001b5c641e5b4d91a235a61aebe2417b2d9c57283a65517f5b764ce4ff03b086c0683010000ffffffff0200e9a435000000001976a91486439eb19afe8c091a01cbb3813b052f7fa3a08b88acdadf42069f0000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac0000000000000000e33ffd5e016a473044022057ec222a8f2f1c7b0cc44d8c375a73bd0bab7816bfe263a527a0cce22c6e2aa8022078c4dfc7fd715732f2b54f7c2a3928bc247bdc2cf65537983c6cc5eaf1827185012103dc8928f91de8af790e7845d30b3b12871f4db39f35ffecfe3f10a1e3e648dc19",
        "txid": "7a927f4c349e5c304e70febd0e6b31dde6037912513cdc22e20a5d3a9f68bb49",
        "txhash": "6a6dd7bcbd472912654a794ba46c82ce775271a40621fc91ad176069ae638c43",
        "size": 234,
        "version": 1,
        "locktime": 0,
        "timestamp": "2020-07-02T06:01:07+04:00",
        "expire": 0,
        "vin": [
          {
            "txid": "066c083bf04fce64b7f51755a68372c5d9b21724beae615a231ad9b4e541c6b5",
            "vout": 387,
            "sequence": 4294967295,
            "scriptSig": {
              "asm": "3044022057ec222a8f2f1c7b0cc44d8c375a73bd0bab7816bfe263a527a0cce22c6e2aa8022078c4dfc7fd715732f2b54f7c2a3928bc247bdc2cf65537983c6cc5eaf182718501 03dc8928f91de8af790e7845d30b3b12871f4db39f35ffecfe3f10a1e3e648dc19",
              "hex": "473044022057ec222a8f2f1c7b0cc44d8c375a73bd0bab7816bfe263a527a0cce22c6e2aa8022078c4dfc7fd715732f2b54f7c2a3928bc247bdc2cf65537983c6cc5eaf1827185012103dc8928f91de8af790e7845d30b3b12871f4db39f35ffecfe3f10a1e3e648dc19"
            }
          }
        ],
        "vout": [
          {
            "amount": 900000000,
            "scriptPubKey": {
              "asm": "OP_DUP OP_HASH160 86439eb19afe8c091a01cbb3813b052f7fa3a08b OP_EQUALVERIFY OP_CHECKSIG",
              "hex": "76a91486439eb19afe8c091a01cbb3813b052f7fa3a08b88ac",
              "reqSigs": 1,
              "type": "pubkeyhash",
              "addresses": [
                "TmbC1Fx1UXNt7D6zpaj83UrAEW7MbcUWuQz"
              ]
            }
          },
          {
            "amount": 683004846042,
            "scriptPubKey": {
              "asm": "OP_DUP OP_HASH160 a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a0 OP_EQUALVERIFY OP_CHECKSIG",
              "hex": "76a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac",
              "reqSigs": 1,
              "type": "pubkeyhash",
              "addresses": [
                "Tme9dVJ4GeWRninBygrA6oDwCAGYbBvNxY7"
              ]
            }
          }
        ],
        "blockhash": "e2ec97db55cff510e30f104e27c9fb687ef7c846fb025dcc1e08b671ee1a2f34",
        "confirmations": 1141
      }
    ]
  }
}
```