---
title: getTx
weight: 3
---

## wallet_getTx
get transaction by ID

### Parameters
1. `txID: (hex string)` transaction ID

### Returns

### Example
#### Request
```sh
$ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getTx","params":["86140f1fa1e7d95707ec7e61748b91838e24a00ca8803f299c7caca591ff1af4"],"id":1}' http://127.0.0.1:8130/api |jq .
```

#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hex": "010000000149bb689f3a5d0ae222dc3c51127903e6dd316b0ebdfe704e305c9e344c7f927a00000000ffffffff0200e1f505000000001976a914a0e30372347bc1e945f5086b7bbeaa38d912dcfe88aca888ae2f000000001976a91486439eb19afe8c091a01cbb3813b052f7fa3a08b88ac00000000000000008215895f016a473044022038fc5c5fef1a7a3bb0117b53556137c75dd9f4970387f2fc2c28c65d30655cea022077eeb7f1a105d9b9353517dc19c6af9ae953a875986bbbe7f5e69cfb3f8a78b2012102e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92",
    "txid": "86140f1fa1e7d95707ec7e61748b91838e24a00ca8803f299c7caca591ff1af4",
    "txhash": "9f3b9d8bf6f893c3b66ef5cd09d73ef3551b93c87d706bedda6ba4a104d469e0",
    "size": 234,
    "version": 1,
    "locktime": 0,
    "timestamp": "2020-10-16T11:37:38+08:00",
    "expire": 0,
    "vin": [
      {
        "txid": "7a927f4c349e5c304e70febd0e6b31dde6037912513cdc22e20a5d3a9f68bb49",
        "vout": 0,
        "sequence": 4294967295,
        "scriptSig": {
          "asm": "3044022038fc5c5fef1a7a3bb0117b53556137c75dd9f4970387f2fc2c28c65d30655cea022077eeb7f1a105d9b9353517dc19c6af9ae953a875986bbbe7f5e69cfb3f8a78b201 02e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92",
          "hex": "473044022038fc5c5fef1a7a3bb0117b53556137c75dd9f4970387f2fc2c28c65d30655cea022077eeb7f1a105d9b9353517dc19c6af9ae953a875986bbbe7f5e69cfb3f8a78b2012102e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92"
        }
      }
    ],
    "vout": [
      {
        "amount": 100000000,
        "scriptPubKey": {
          "asm": "OP_DUP OP_HASH160 a0e30372347bc1e945f5086b7bbeaa38d912dcfe OP_EQUALVERIFY OP_CHECKSIG",
          "hex": "76a914a0e30372347bc1e945f5086b7bbeaa38d912dcfe88ac",
          "reqSigs": 1,
          "type": "pubkeyhash",
          "addresses": [
            "Tmdcmmo7JqxxwHy6r46Sx2ZRbVF2dSjG9mm"
          ]
        }
      },
      {
        "amount": 799967400,
        "scriptPubKey": {
          "asm": "OP_DUP OP_HASH160 86439eb19afe8c091a01cbb3813b052f7fa3a08b OP_EQUALVERIFY OP_CHECKSIG",
          "hex": "76a91486439eb19afe8c091a01cbb3813b052f7fa3a08b88ac",
          "reqSigs": 1,
          "type": "pubkeyhash",
          "addresses": [
            "TmbC1Fx1UXNt7D6zpaj83UrAEW7MbcUWuQz"
          ]
        }
      }
    ],
    "blockhash": "2a215f23d2d4269ee235d730049cbdd18721de11b58e56fe29859f77f64ef82c",
    "confirmations": 12
  }
}
```