---
title: getBlock
weight: 1
---

## getBlock
### 函数名：getBlock {blockhash} {verbose} {inclTx} {fullTx}
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

