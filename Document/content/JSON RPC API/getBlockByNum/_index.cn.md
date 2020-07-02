---
title: getBlockByNum
weight: 1
---

## getBlockByNum
### 函数名：getBlockByNum {number} {verbose} {inclTx} {fullTx}
### 说明：
- number：number指按照当前节点所观察到的区块所构造的本地DAG图的区块序号，是一个从0开始，按顺序递增的连续整数值。该序号（Num）与全网其他节点无关，即并非BlockDAG共识结果的Block排序，请注意该方法和`getBlockByOder`的区别。该方法只用于帮助二级应用构造特殊业务场景而存在，返回结构并非BlockDAG共识结果，使用时请注意。
- verbose: 是否显示详细信息，默认为false
- inclTx: 是否包含交易信息，默认为true
- fullTx：是否显示完整交易信息，默认为true

#### 实例:

```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockByNum","params":[1,true],"id":1}' https://127.0.0.1:18131
```
输出：
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hash": "83d98f64ff6517e5899a1c392d91c334ae77a8c7705cd3ca0b147a6470d8eb08",
    "txsvalid": false,
    "confirmations": 0,
    "version": 12,
    "weight": 443,
    "height": 1,
    "txRoot": "0cda5bc3744da7fcdd4a6dbbd72b24a58b9dcd927a171021646af87aa926315d",
    "transactions": [
      {
        "hex": "010000000114898f3cc6b4de34ca419365fee41fd78d74d71a70a98caa88e1260efb876a79ffffffffffffffff01007841cb020000001976a914499896c7814a6f49fa256bc5feaa5882a665339188ac000000000000000000000000012151080300009030da6dd9162f7777772e6d656572706f6f6c2e636f6d2f32303230",
        "txid": "0cda5bc3744da7fcdd4a6dbbd72b24a58b9dcd927a171021646af87aa926315d",
        "txhash": "0ac294d88ec9ab3f9cdfff2775d3c881a44cf4b73a1aaa2c2b57e58f055e3168",
        "size": 127,
        "version": 1,
        "locktime": 0,
        "expire": 0,
        "vin": [
          {
            "coinbase": "51080300009030da6dd9162f7777772e6d656572706f6f6c2e636f6d2f32303230",
            "sequence": 4294967295
          }
        ],
        "vout": [
          {
            "amount": 12000000000,
            "scriptPubKey": {
              "asm": "OP_DUP OP_HASH160 499896c7814a6f49fa256bc5feaa5882a6653391 OP_EQUALVERIFY OP_CHECKSIG",
              "hex": "76a914499896c7814a6f49fa256bc5feaa5882a665339188ac",
              "reqSigs": 1,
              "type": "pubkeyhash",
              "addresses": [
                "TmVfDq18VqSg735ko9aAo36tFwYww4PBGMC"
              ]
            }
          }
        ],
        "blockhash": "83d98f64ff6517e5899a1c392d91c334ae77a8c7705cd3ca0b147a6470d8eb08",
        "confirmations": 0
      }
    ],
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "bits": "1b00ffff",
    "difficulty": 453050367,
    "pow": {
      "pow_name": "qitmeer_keccak256",
      "pow_type": 6,
      "nonce": 1067495060
    },
    "timestamp": "2020-06-24T10:06:46+08:00",
    "parentroot": "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a",
    "parents": [
      "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a"
    ],
    "children": [
      "null"
    ]
  }
}
```


