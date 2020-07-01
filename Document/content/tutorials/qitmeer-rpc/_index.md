---
title: Qitmeer RPC
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# Qitmeer RPC 说明

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

## getBlocK
### 函数名：getBlocK {blockhash} {verbose} {inclTx} {fullTx}
### 说明：根据区块hash获取区块
- blockhash : 256位区块hash
- verbose: 是否显示详细信息，默认为false
- inclTx: 是否包含交易信息，默认为true
- fullTx：是否显示完整交易信息，默认为true

#### 实例:
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlock","params":["98294db0634d5afed36554a60d4565a6507e3a78dfb8cc66cc08ba29f328c682",true,true,false],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hash": "98294db0634d5afed36554a60d4565a6507e3a78dfb8cc66cc08ba29f328c682",
    "txsvalid": true,
    "confirmations": 338,
    "version": 12,
    "weight": 682,
    "height": 20831,
    "txRoot": "040807f45457c94ed905bf72ed923154a5e951278e80a5c0eb2de0d7b269c5c1",
    "order": 21300,
    "transactions": [
      "5844ca2e091f8c2a770f4a0ff23318ae780b9e3a9b2076cc27b8c493dce30c03",
      "c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32"
    ],
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "bits": "1a1c60ed",
    "difficulty": 438067437,
    "pow": {
      "pow_name": "qitmeer_keccak256",
      "pow_type": 6,
      "nonce": 1457503796
    },
    "timestamp": "2020-07-01T12:48:52+08:00",
    "parentroot": "000073e5c2787d1d2a04358c8b2fad422a602a38a6070570c2d8b724c054987f",
    "parents": [
      "000073e5c2787d1d2a04358c8b2fad422a602a38a6070570c2d8b724c054987f"
    ],
    "children": [
      "00018c75188cc658705af615684b095bbc85a2dde6772e4bf3929b5d5505f5fb"
    ]
  }
}
```

## getBlocKV2
### 函数名：getBlocK {blockhash} {verbose} {inclTx} {fullTx}
### 说明：根据区块hash获取区块 版本2
- blockhash : 256位区块hash
- verbose: 是否显示详细信息，默认为false
- inclTx: 是否包含交易信息，默认为true
- fullTx：是否显示完整交易信息，默认为true

V2版本RPC将交易手续费显示在单独的`transactionfee`属性中。而之前版本的交易手续费体现在coinbase的Amount中，和挖矿奖励合并显示。请注意，不论使用V1或者V2版本的API，只影响JSON数据的显示。内部的数据模型和共识模型是完全是一致的。

#### 实例

```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockV2","params":["98294db0634d5afed36554a60d4565a6507e3a78dfb8cc66cc08ba29f328c682",true,true,false],"id":1}' https://127.0.0.1:18131
```

输出：
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hash": "98294db0634d5afed36554a60d4565a6507e3a78dfb8cc66cc08ba29f328c682",
    "txsvalid": true,
    "confirmations": 304,
    "version": 12,
    "weight": 682,
    "height": 20831,
    "txRoot": "040807f45457c94ed905bf72ed923154a5e951278e80a5c0eb2de0d7b269c5c1",
    "order": 21300,
    "transactions": [
      "5844ca2e091f8c2a770f4a0ff23318ae780b9e3a9b2076cc27b8c493dce30c03",
      "c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32"
    ],
    "transactionfee": 32000,
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "bits": "1a1c60ed",
    "difficulty": 438067437,
    "pow": {
      "pow_name": "qitmeer_keccak256",
      "pow_type": 6,
      "nonce": 1457503796
    },
    "timestamp": "2020-07-01T12:48:52+08:00",
    "parentroot": "000073e5c2787d1d2a04358c8b2fad422a602a38a6070570c2d8b724c054987f",
    "parents": [
      "000073e5c2787d1d2a04358c8b2fad422a602a38a6070570c2d8b724c054987f"
    ],
    "children": [
      "00018c75188cc658705af615684b095bbc85a2dde6772e4bf3929b5d5505f5fb"
    ]
  }
} 
```

## getBlockHeader
### 函数名：getBlockHeader {blockhash} {verbose}
### 说明：无参数，当前已定序的区块数量。
- blockhash ： 256位区块hash
- verbose ：是否显示详细信息，默认为false
注：该数量-1即为当前最大的Block order 


#### 实例
```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockHeader","params":["0011cc2a9cea757a2aaa235f27f41f00e3e2ed87282175fe76767c4f50b3aa05",true],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "hash": "0011cc2a9cea757a2aaa235f27f41f00e3e2ed87282175fe76767c4f50b3aa05",
    "confirmations": 21145,
    "version": 12,
    "parentroot": "00015f28637b8442e2399924d0db703efebd33ab3176d4ccb7b762a28529087e",
    "txRoot": "c564f2c2e6fd7b7db1d09272a607388861f2bfe34550d5f7176ed4652459bbd7",
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "difficulty": 55235052,
    "layer": 116,
    "time": 1592967313,
    "pow": {
      "pow_name": "cuckaroom",
      "pow_type": 3,
      "nonce": 19,
      "proof_data": {
        "edge_bits": 29,
        "circle_nonces": "2b1c9b002544650140638b036dd04804cbd65304c5963305f3184d055dca110674761d0646e81d0639683d06718d1007c85c150744b960089a99a40878dff708e06320097e0d67098fa51d0a4e7c5f0acc8ad30b1e2e4e0ce5c0990cd0fcb80e1013ba0e3b614d0f5ba19c0f4904b90f0c190f12d5869012f45b621415193315ec0727160314e417b51938185314c218281ce318ca84ec18dd1b001941b7d619a571881e6f4f831f"
      }
    }
  }
}
```


## getBlockCount
### 函数名：getBlockCount 
### 说明：无参数，当前已定序的区块数量。
该数量-1即为当前最大的Block order 

#### 实例
```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockCount","params":[],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 21177
}
```

## getBlockTotal
### 函数名：getBlockTotal
### 说明：无参数，该节点所有已知的区块总数量。
该数量包含可能存在的当前还未被BlockDAG共识定序的区块

#### 实例
```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockTotal","params":[],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 21177
}
```

## getBlockBestHash
### 函数名：getBlockBestHash
### 说明：无参数，获取当前最大区块Order的区块hash
### 实例

```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBestBlockHash","params":[],"id":1}' https://127.0.0.1:18131
```
输出
```

{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "000044c83486609eee3c5bb46cd539eb022ea05ed86c40ef4e6710357f225ea3"
}
```


## getBlockhashByRange
### 函数名 getBlockhashByRange {start} {end}
### 说明：获取在某区间order范围的一组Blockhash
- start 开始区块order
- end   结束区块order

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getBlockhashByRange","params":[100,125],"id":null}' https://127.0.0.1:18131
```
输出：
```
[
  "000c018b33589f2f731d9cfc26d5d329fefce1045b9d1e5b22e3e8e71760e0e7",
  "68d1170256afeae9591bcb49c99734e582f59860d0917e449c03f08c269957a3",
  "0010b1aef1910f1c5662e0991d8ba1d564e3df360c6235f6890486a35a4ca000",
  "0013a4646accf2f11c96e59d51f07be4a510a0e9e12174fd569ae3744a38de24",
  "0016242fcaf6effecf083aa2b7716f8825addb31530ce3141da7d50293f3dce2",
  "00173736aba73591a7ce051c0a4e4605edcbafe48149849880d9b8c7781b538e",
  "0007ae2245017244e3ca355bcbe2947f69ab1ab5c52112bff003842363298395",
  "0016b7148e99c60cf74c96cdeffc8a966817f163013dc3fb89684946d7cbb7bc",
  "000edcf8a5dad7cfdf25461359678421e51930614d73a965b8532bb608c00025",
  "000ea156ad8ef5c90d0c5855a5352a9e156d8d778ee53daa5bb9145268b17693",
  "2fa46ac8fa234ee5950d74fdaf0fd60d6fed406f1208d10ecff11026eaa45c86",
  "000c5816df76fd7b6662cf2c9c57c87f050c1b101c5466a1fa6bbe5eebebbd22",
  "178fc77f4af15e977861510c81f957b6518215ea483f847caa67e0daeb8ac0ce",
  "0014fa7d8499812b5a7f404efa82b4959db5542bae55e60035cc0d5ae0ef29fa",
  "0014c1c5b794c7fa91271841b6c4f63f6216529d7c9076e2e2f861e47bd31290",
  "000207d33febab535405082c9bd78cd463048143429b404a120faa95b139d9b8",
  "0628f63bf041cab884e55192a6bf6615c198390821542a1c3b53ad3fafc9bbd1",
  "000cff170cde98b09f80c76109843d178f67dc7c64d25f6886f93ce0cd25fd7a",
  "000b4c1f4a87f97b5ef7727f2fc4ffb9f5cf34b9c759e12dfb4954cfeb6f65fb",
  "5d138960ca76057f379d8d6cb82bf6a93b7b2c63d1a4950d15305d12124f3b89",
  "7d6d9140f516d9a12ca2109a89a17c777425b73596b9b4a7a4a4d4013da6ddec",
  "2f3817197e885e805229c4be3cf94b9b7581b4e6975068e5583b8295b648d690",
  "46e97b2fda23be092abd8c163c3d2f0a60018904484fd688918b7c5f257686e0",
  "00015f28637b8442e2399924d0db703efebd33ab3176d4ccb7b762a28529087e",
  "0011cc2a9cea757a2aaa235f27f41f00e3e2ed87282175fe76767c4f50b3aa05"
]

```

## isOnMainChain
### 函数名 isOnMainChain {blockhash}
### 说明：判断该block是否在主链上

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"isOnMainChain","params":["0011cc2a9cea757a2aaa235f27f41f00e3e2ed87282175fe76767c4f50b3aa05"],"id":1}' https://127.0.0.1:18131
```

输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "true"
}
```

## getMainChainHeight
### 函数名 getMainChainHeight
### 说明：无参数，得到当前的主链高度。

#### 实例
```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getMainChainHeight","params":[],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "21275"
}
```


## getOrphansTotal
### 函数名 getOrphansTotal
### 说明：无参数，得到当前节点的孤儿区块的数量。
孤儿区块指当前未关联到DAG中的区块。

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getOrphansTotal","params":[],"id":null}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": null,
  "result": 0
}

```

## getTips
### 函数名 getTips
### 说明：得到Tip Block列表
Tips列表是当前节点的DAG图的Tips Block的hash列表

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"tips","params":[],"id":null}' https://127.0.0.1:18131
```

```
{
  "jsonrpc": "2.0",
  "id": null,
  "result": [
    "83d98f64ff6517e5899a1c392d91c334ae77a8c7705cd3ca0b147a6470d8eb08",
    "00001ae85f5c90cc2f1f9ae5b1ac148145555d884f2c7d986cb3df250c8c3ecc"
  ]
}
```


## getMempool
### 函数名：getMempool 
### 说明：
- txType: 交易类型，目前只支持regular。
- verbose：显示详细信息，目前只支持false。

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getMempool","params":["regular",false],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": [
    "8df1c9019dd7110e9c3a421f62973ff245cbad435452808363ac291bf2265613"
  ]
}
```

## getPeerInfo
### 函数名：getPeerInfo 
### 说明：无参数，取邻近节点信息

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getPeerInfo","params":[],"id":null}' https://127.0.0.1:18131
```

输出:
```
[
  {
    "uuid": "f280f357-ee4a-4958-90bf-685d24129703",
    "id": 5,
    "addr": "103.1.154.227:18130",
    "addrlocal": "10.198.1.66:56261",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576243,
    "lastrecv": 1593576298,
    "bytessent": 5029,
    "bytesrecv": 7315,
    "conntime": 1593575403,
    "timeoffset": 0,
    "pingtime": 371602,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "b0c3462f-328d-45ba-8e3f-490c205eec85",
    "id": 6,
    "addr": "47.103.61.128:18130",
    "addrlocal": "10.198.1.66:56262",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576298,
    "lastrecv": 1593576299,
    "bytessent": 2941,
    "bytesrecv": 16892,
    "conntime": 1593575403,
    "timeoffset": 0,
    "pingtime": 871878,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "349a58ee-3537-4576-ba8a-925a27725070",
    "id": 7,
    "addr": "106.15.102.183:18130",
    "addrlocal": "10.198.1.66:56284",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576254,
    "lastrecv": 1593576298,
    "bytessent": 1471,
    "bytesrecv": 7965,
    "conntime": 1593575414,
    "timeoffset": 0,
    "pingtime": 485255,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "400176fd-8155-405c-ae4f-032948581558",
    "id": 8,
    "addr": "148.70.34.136:18130",
    "addrlocal": "10.198.1.66:56413",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576307,
    "lastrecv": 1593576308,
    "bytessent": 1757,
    "bytesrecv": 11162,
    "conntime": 1593575465,
    "timeoffset": 0,
    "pingtime": 830143,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "1df6c4ca-dae0-4632-bdb2-d9ef916b7580",
    "id": 1,
    "addr": "104.224.174.141:18130",
    "addrlocal": "10.198.1.66:56182",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576333,
    "bytessent": 4259,
    "bytesrecv": 1214,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 244235,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "3b3b4e71e7ab837635da8442afb98ba4092a2df62cf25e59a58bda518ce81fca main"
      ],
      "mainorder": 21065,
      "mainheight": 20597,
      "layer": 20597
    }
  },
  {
    "uuid": "a8383106-45dc-4028-ae04-74d25ad09f7d",
    "id": 2,
    "addr": "144.202.90.65:18130",
    "addrlocal": "10.198.1.66:56177",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576333,
    "bytessent": 5178,
    "bytesrecv": 8411,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 259579,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": true,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "277d5f3f-3af3-486e-92ca-8da59eaa6db9",
    "id": 4,
    "addr": "122.112.245.133:18130",
    "addrlocal": "10.198.1.66:56180",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576334,
    "bytessent": 1692,
    "bytesrecv": 9459,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 414095,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "38d8647f-371d-47c6-924b-ddfe32391a83",
    "id": 3,
    "addr": "103.29.70.78:18130",
    "addrlocal": "10.198.1.66:56175",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576334,
    "bytessent": 2421,
    "bytesrecv": 6656,
    "conntime": 1593575373,
    "timeoffset": -1,
    "pingtime": 345824,
    "version": 21,
    "subver": "qitmeer:0.9.1",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  }
]

```

## getNodeInfo
### 函数名：getNodeInfo 
### 说明：无参数，获取该节点信息

#### 实例

```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getNodeInfo","params":[],"id":null}' https://127.0.0.1:18131
```

输出：
```
{
  "UUID": "dc4dffc6-9c0c-417f-9cb2-a1fdc4877915",
  "version": 90100,
  "buildversion": "0.9.1+dev-7ae8c17",
  "protocolversion": 21,
  "totalsubsidy": 254484000000000,
  "graphstate": {
    "tips": [
      "00006869b1f1e29db24cc528a86370b4355f1dc6a618ac0549495679f0bc484b main"
    ],
    "mainorder": 21207,
    "mainheight": 20738,
    "layer": 20738
  },
  "timeoffset": 0,
  "connections": 8,
  "pow_diff": {
    "blake2bd_diff": 1,
    "cuckaroo_diff": 1,
    "cuckatoo_diff": 1
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

#### 结果说明：
- confirmations：代表非coinbase交易的UXTO可以被花费的最小确认数，当前的共识的最小确认数为10个确认。
- coinbasematurity：代表coinbase交易的UXTO可以被花费的最小确认数，当前的共识是720个确认。
- 注：不论coinbase交易还是非coinbase交易，除了满足各自的最小确认条件外，还需要包含该交易的区块满足如下条件，才能满足该该交易的UTXO可花费：
  - 1.）BlockDAG共识约束，即该区块为蓝色区块，详见见rpc isBule
  - 2.）该区块为交易合法区块，即区块的`txsvalid`属性为true。详见rpc getBlockByOrder



# isBlue
### 函数名：isBlue {blockhash}
### 说明：通过节点判断该块是否为蓝色区块
- blockhash：区块hash

### 结果说明：
- 0:为红色区块，该块coinbase不能交易
- 1:为蓝色区块，该块的coinbase可以交易
- 2:还不能确定是蓝色或红色，待确认

#### 实例1 
```
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"isBlue","params":["0003409cc9bcfc328630982797326e62135d6fc2431db7b85c2a0fe38ff5749c"],"id":1}' https://127.0.0.1:18131
```
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 2
}
```
#### 实例2
可以观察到对于是否蓝色区块的判断结果，由2变为1。即由不能确认变为蓝色区块。

```
$ date
Wed Jul  1 12:23:39 CST 2020
$ curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"isBlue","params":
["0003409cc9bcfc328630982797326e62135d6fc2431db7b85c2a0fe38ff5749c"],"id":1}' https://127.0.0.1:18131
```

```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 1
}
```


## getRawTransaction
### 函数名：getRawTransaction {txid}
### 说明：通过txid获取交易
- txid 交易id 为一个256位hash值。
- verbose 是否显示详细信息，默认为false

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getRawTransaction","params":["c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32",true],"id":1}' https://127.0.0.1:18131
```
输出
```
{
  "hex": "0100000001dc7d54db024a1ef06e38b85ab01af2d60043e3d36b5411691224c05dcf36f63c01000000ffffffff02659ca300000000001976a91406e2097d585337cdd10aefa09994b511127af0bb88acf0e8cd6f230200001976a914fe27c90d4ed4de3269c0bb9ae1d7639865e3bf2888ac00000000000000008015fc5e016b48304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a012103cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8",
  "txid": "c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32",
  "txhash": "9b603ba3b17fd8491749ac366a5064d8b7b70be02568e405406a9acd70e971a8",
  "size": 235,
  "version": 1,
  "locktime": 0,
  "timestamp": "2020-07-01T12:48:00+08:00",
  "expire": 0,
  "vin": [
    {
      "txid": "3cf636cf5dc024126911546bd3e34300d6f21ab05ab8386ef01e4a02db547ddc",
      "vout": 1,
      "sequence": 4294967295,
      "scriptSig": {
        "asm": "304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a01 03cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8",
        "hex": "48304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a012103cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8"
      }
    }
  ],
  "vout": [
    {
      "amount": 10722405,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 06e2097d585337cdd10aefa09994b511127af0bb OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a91406e2097d585337cdd10aefa09994b511127af0bb88ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "TmPaUYQuUtfCysrYVHc4AdhpVHxw7EskHTP"
        ]
      }
    },
    {
      "amount": 2351222876400,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 fe27c90d4ed4de3269c0bb9ae1d7639865e3bf28 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914fe27c90d4ed4de3269c0bb9ae1d7639865e3bf2888ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "Tmn7vzzSrvAPNLtwpD5YjiWwVUBD74Hjdww"
        ]
      }
    }
  ],
  "confirmations": 0
}

```

## sendRawTransaction
### 函数名：sendRawTransaction {sign_raw_tx} {allow_high_fee}
### 说明：发送交易

- sign_raw_tx:签名后的交易
- allow_high_fee：允许的最大交易费

#### 实例：

```

sendRawTransaction 0100000001ff5d53a7070fa9f0a9d12af729d2cbaf355ef1173c106a84cf9ef3a46bff03b202000000ffffffff01005504790a0000001976a914627777996288556166614462639988446255776688ac000000000000000001000000000000000000000000ffffffff6b483045022100dced4d67dd74647d0036077ee5b435838934377b1d296dd9da852772911e3be2022063dd346bd812a894968b8acacead7e7beff48947657a82f1e8f9c38876d4c905012103aba0a09f5b44138a46a2e5d26b8659923d84c4ba9437e22c3828cac43d0edb49 true

```
