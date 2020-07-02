---
title: getBlockByOrder
weight: 1
---

## getBlockByOrder
### 函数名：getBlockByOrder {order} {verbose} {inclTx} {fullTx} 
### 说明：返回指定Order的Block
- order:区块order，qitmeer采用BlockDAG算法进行共识，对区块的先后顺序进行排序。order指区块序列的序号，是一个从0开始，按顺序连续递增的整数值。请注意order不是区块的高度。
- verbose: 是否显示详细信息，默认为false
- inclTx: 是否包含交易信息，默认为true
- fullTx：是否显示完整交易信息，默认为true

#### 实例1:
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockByOrder","params":[1,true],"id":1}' https://127.0.0.1:18131
```
实例1输出:
```
{
  "hash": "0012c535ed43311b0670341fad3a489642c0bc6e6796f836aa6d235826fc9c66",
  "txsvalid": true,
  "confirmations": 20651,
  "version": 12,
  "weight": 433,
  "height": 1,
  "txRoot": "845738befb45db6872e37295b39837cd8dc98e77417754fd4ddab5ff169317be",
  "order": 1,
  "transactions": [
    {
      "hex": "0c000000010a7ebb3e65b3be8a2e3425407e8e649c4bde818b7db70bdb3d4b8c3256745f37ffffffffffffffff01007841cb020000001976a91409eb5fc744c14c8cdd5a05b552c58c1fb6e7ebd088ac000000000000000072b6f25e01175108461004cbac974daf0c2f363636706f6f6c2e636e2f",
      "txid": "845738befb45db6872e37295b39837cd8dc98e77417754fd4ddab5ff169317be",
      "txhash": "93772af2957ecd066841fda4606bfa5e001ac151062c0b3ca7cfea60ec35e8b3",
      "size": 117,
      "version": 12,
      "locktime": 0,
      "timestamp": "2020-06-24T10:12:02+08:00",
      "expire": 0,
      "vin": [
        {
          "coinbase": "5108461004cbac974daf0c2f363636706f6f6c2e636e2f",
          "sequence": 4294967295
        }
      ],
      "vout": [
        {
          "amount": 12000000000,
          "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 09eb5fc744c14c8cdd5a05b552c58c1fb6e7ebd0 OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a91409eb5fc744c14c8cdd5a05b552c58c1fb6e7ebd088ac",
            "reqSigs": 1,
            "type": "pubkeyhash",
            "addresses": [
              "TmPrXkjpjSUBiFG9RZKPjfdsAPbiaar94Ta"
            ]
          }
        }
      ],
      "blockhash": "0012c535ed43311b0670341fad3a489642c0bc6e6796f836aa6d235826fc9c66",
      "confirmations": 20651
    }
  ],
  "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
  "bits": "34ad1ec",
  "difficulty": 55235052,
  "pow": {
    "pow_name": "cuckaroom",
    "pow_type": 3,
    "nonce": 5,
    "proof_data": {
      "edge_bits": 29,
      "circle_nonces": "fa50c20086aef40090ebab01295d5102697fcb0229e83b04b0ac4604fd9a6505118a6f05deb21206e88f9c07184fae075e218408884ed90bdfca630cf9e2a60c12fae80f909b831084669a109390e6105aa9c611aea1e71288408713c670641405f9a714abfcf81557ded81665b20f17a17370170628de17d4ccfb1755515618f5456918efd27918d4f4d218f91bb71954e3b11cb648ca1c9779541d51ee6b1ee12a711e0679131f"
    }
  },
  "timestamp": "2020-06-24T10:05:33+08:00",
  "parentroot": "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a",
  "parents": [
    "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a"
  ],
  "children": [
    "000de974590581de8294866535b3af182041a4cb29b71a7680b024e3bd7d12da"
  ]
}

```

#### 实例2:
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockByOrder","params":[1,false],"id":1}' https://127.0.0.1:18131
```
实例2输出:
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0c0000008a3a4dc9fa02a45648c4fb3b9e86bc50ea0e76c7de8173bc3cfe70b9218b9836be179316ffb5da4dfd547741778ec98dcd3798b39572e37268db45fbbe3857840000000000000000000000000000000000000000000000000000000000000000ecd14a03edb4f25e05000000031dfa50c20086aef40090ebab01295d5102697fcb0229e83b04b0ac4604fd9a6505118a6f05deb21206e88f9c07184fae075e218408884ed90bdfca630cf9e2a60c12fae80f909b831084669a109390e6105aa9c611aea1e71288408713c670641405f9a714abfcf81557ded81665b20f17a17370170628de17d4ccfb1755515618f5456918efd27918d4f4d218f91bb71954e3b11cb648ca1c9779541d51ee6b1ee12a711e0679131f018a3a4dc9fa02a45648c4fb3b9e86bc50ea0e76c7de8173bc3cfe70b9218b9836010c000000010a7ebb3e65b3be8a2e3425407e8e649c4bde818b7db70bdb3d4b8c3256745f37ffffffffffffffff01007841cb020000001976a91409eb5fc744c14c8cdd5a05b552c58c1fb6e7ebd088ac000000000000000072b6f25e01175108461004cbac974daf0c2f363636706f6f6c2e636e2f"
}
```

#### 实例3:
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockByOrder","params":[1,true,false],"id":1}' https://127.0.0.1:18131
```
实例3输出:
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hash": "0012c535ed43311b0670341fad3a489642c0bc6e6796f836aa6d235826fc9c66",
    "txsvalid": true,
    "confirmations": 20686,
    "version": 12,
    "weight": 433,
    "height": 1,
    "txRoot": "845738befb45db6872e37295b39837cd8dc98e77417754fd4ddab5ff169317be",
    "order": 1,
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "bits": "34ad1ec",
    "difficulty": 55235052,
    "pow": {
      "pow_name": "cuckaroom",
      "pow_type": 3,
      "nonce": 5,
      "proof_data": {
        "edge_bits": 29,
        "circle_nonces": "fa50c20086aef40090ebab01295d5102697fcb0229e83b04b0ac4604fd9a6505118a6f05deb21206e88f9c07184fae075e218408884ed90bdfca630cf9e2a60c12fae80f909b831084669a109390e6105aa9c611aea1e71288408713c670641405f9a714abfcf81557ded81665b20f17a17370170628de17d4ccfb1755515618f5456918efd27918d4f4d218f91bb71954e3b11cb648ca1c9779541d51ee6b1ee12a711e0679131f"
      }
    },
    "timestamp": "2020-06-24T10:05:33+08:00",
    "parentroot": "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a",
    "parents": [
      "36988b21b970fe3cbc7381dec7760eea50bc869e3bfbc44856a402fac94d3a8a"
    ],
    "children": [
      "000de974590581de8294866535b3af182041a4cb29b71a7680b024e3bd7d12da"
    ]
  }
}
```



