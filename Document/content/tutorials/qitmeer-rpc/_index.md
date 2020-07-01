---
title: Qitmeer RPC
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# Qitmeer RPC 说明

### 1. getBlockByOrder
#### 函数名：getBlockByOrder {order} {fullTx}
#### 说明：
- order:区块order，qitmeer采用BlockDAG算法进行共识，对区块的先后顺序进行排序。order指区块序列的序号，一个从0开始增大的整数值。请注意order不是区块的高度。
- fullTx: true/false,该值一般为true，

```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockByOrder","params":[1,true,true,true],"id":1}' https://127.0.0.1:18131
```

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

### 2.getBlockByNum
#### 函数名：getBlockByNum {number} {fullTx}
#### 说明：
- number：number指按照当前节点所接受到的区块先后顺序，进行顺序的序号，一个从0开始向上增大的整数值。该序号（Num）与全网其他节点无关，即非BlockDAG共识结果的Block排序。
- fullTx：true/false，一般为true

### 3.getBlockCount
#### 函数名：getBlockCount 
#### 说明：无参数，获取区块数量

### 4.getMempool
#### 函数名：getMempool 
#### 说明：无参数，获取交易池交易

### 5.getPeerInfo
#### 函数名：getPeerInfo 
#### 说明：无参数，取邻近节点信息


### 6.getNodeInfo
#### 函数名：getNodeInfo 
#### 说明：无参数，获取该节点信息

```

{
    "UUID": "d66d8f6d-c5c8-422a-befe-aa0b7ec3c5f1",
    "version": 70800,
    "protocolversion": 12,
    "totalsubsidy": 102856000000000,
    "graphstate": {
        "tips": [
            "078f9626c4fc6b18dfc6698bddbeb212808f148f31ac0aa777829b56e5469929"
        ],
        "mainorder": 7912,
        "mainheight": 7816,
        "layer": 7816
    },
    "timeoffset": 0,
    "connections": 5,
    "pow_diff": {
        "blake2bd_diff": 5.200604516135472e+63,
        "cuckaroo_diff": 0.14814815,
        "cuckatoo_diff": 2.86419753
    },
    "testnet": true,
    "mixnet": false,
    "confirmations": 10,
    "coinbasematurity": 720,
    "errors": "",
    "modules": [
        "qitmeer",
        "miner",
        "test"
    ]
}

```
### 结果说明：

- confirmations：代表区块中非coinbase输出可用的最小确认数，凡是区块confirmations确认数大于该值的区块中的非coinbase输出可进行交易
- coinbasematurity：代表区块coinbase输出可以用的最小确认数，凡是区块confirmations确认数大于该值的区块中的coinbase输出可进行交易的第一个条件，第二个条件是必须是蓝色区块，见rpc isBule

### 7.isBlue
#### 函数名：isBlue {blockhash}
#### 说明：通过节点判断该块是否为蓝色区块

- blockhash：需要查找额块hash

#### 结果说明：
- 0:为红色区块，该块coinbase不能交易
- 1:为蓝色区块，该块的coinbase可以交易
- 2:还不能确定是蓝色或红色，待确认


### 8.getRawTransaction
#### 函数名：getRawTransaction {txid}
#### 说明：通过txid获取交易

```

getRawTransaction 000000e4c6b7f5b89827711d412957bfff5c51730df05c2eedd1352468313eca


{
    "hex": "0100000001cf6849e307726cfd51ad93b994c4dcdc390b782ad34cfafbcacf47f17c639606ffffffffffffffff010042dc06030000001976a914883e0d08cf453696b756baabadae1da8ab3f227888ac000000000000000001435c08d0b7b3581e39345913363432373832353337303636343531353533362431613037373964612d616466352d346365392d613962652d626238613732636639333232",
    "txid": "df492c0f85fee7fd883c45dbb1bbbcec4bf2ea1e315f33aee0e27bddaede35c3",
    "txhash": "26f8a70736ef23ac4ba57c91563360ba44ec8c0b448c2b20d05ad5387040acaa",
    "size": 157,
    "version": 1,
    "locktime": 0,
    "expire": 0,
    "vin": [
        {
            "coinbase": "5c08d0b7b3581e39345913363432373832353337303636343531353533362431613037373964612d616466352d346365392d613962652d626238613732636639333232",
            "sequence": 4294967295
        }
    ],
    "vout": [
        {
            "amount": 13000000000,
            "scriptPubKey": {
                "asm": "OP_DUP OP_HASH160 883e0d08cf453696b756baabadae1da8ab3f2278 OP_EQUALVERIFY OP_CHECKSIG",
                "hex": "76a914883e0d08cf453696b756baabadae1da8ab3f227888ac",
                "reqSigs": 1,
                "type": "pubkeyhash",
                "addresses": [
                    "TmbNTwPm9aTN7TtStnJjrcjsaRJWm4gt3Fs"
                ]
            }
        }
    ],
    "blockhash": "3df0e5bb739d7ac0e4d34f621514d485dff3a3c0be31c161cc891787172caade",
    "confirmations": 7838
}

```

### 9.sendRawTransaction
#### 函数名：sendRawTransaction {sign_raw_tx} {allow_high_fee}
#### 说明：发送交易

- sign_raw_tx:签名后的交易
- allow_high_fee：允许的最大交易费

### 例：

```

sendRawTransaction 0100000001ff5d53a7070fa9f0a9d12af729d2cbaf355ef1173c106a84cf9ef3a46bff03b202000000ffffffff01005504790a0000001976a914627777996288556166614462639988446255776688ac000000000000000001000000000000000000000000ffffffff6b483045022100dced4d67dd74647d0036077ee5b435838934377b1d296dd9da852772911e3be2022063dd346bd812a894968b8acacead7e7beff48947657a82f1e8f9c38876d4c905012103aba0a09f5b44138a46a2e5d26b8659923d84c4ba9437e22c3828cac43d0edb49 true

```
