---
title: Qitmeer RPC
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# Qitmeer RPC 说明

## 以下rpc均可通过curl可进行调用

```

curl -k -u "admin:123" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getPeerInfo","params":null,"id":1}' http://127.0.0.1:1234 | jq
```

[点击下载java版rpc调用示例](https://github.com/qitmeers/files/blob/master/rpcdemo-java.zip)

### 1. getBlockByOrder
#### 函数名：getBlockByOrder {order} {fullTx}
#### 说明：
- order:区块orderid，由于qitmeer采用DAG算法，区块的orderid会发生变动，该值并非是区块高度
- fullTx: true/false,该值一般为true，

```
{
    "hash": "40f714e882292041d5a02bc5286fc465d04ae84e7a784debe8e93fef7f7e14f6",
    "txsvalid": true,
    "confirmations": 7784,
    "version": 8,
    "weight": 473,
    "height": 11,
    "txRoot": "e59a81ecd2d013adfb2c73068a672ef0805c0aa4877ef114b275829c863c5608",
    "order": 11,
    "transactions": [
        {
            "hex": "010000000139d821f342cd463794ea5a2ae70f1059124d6398caf4197d6dc13798574cdd42ffffffffffffffff010042dc06030000001976a914883e0d08cf453696b756baabadae1da8ab3f227888ac000000000000000001435b086c0dd1ff9a9c865213353934363631323534373532303130353833362430633136653839622d393438372d343865622d396536332d656130646430663735373236",
            "txid": "e59a81ecd2d013adfb2c73068a672ef0805c0aa4877ef114b275829c863c5608",
            "txhash": "aaf2a2357b41950f27403e6f5841cfcd894b80f18fc724a8d4155c7a4706066f",
            "size": 157,
            "version": 1,
            "locktime": 0,
            "expire": 0,
            "vin": [
                {
                    "coinbase": "5b086c0dd1ff9a9c865213353934363631323534373532303130353833362430633136653839622d393438372d343865622d396536332d656130646430663735373236",
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
            "blockhash": "40f714e882292041d5a02bc5286fc465d04ae84e7a784debe8e93fef7f7e14f6",
            "confirmations": 7784
        }
    ],
    "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "bits": "1600000",
    "difficulty": 23068672,
    "pow": {
        "pow_name": "cuckaroo",
        "pow_type": 1,
        "nonce": 3412159405,
        "proof_data": {
            "edge_bits": 24,
            "circle_nonces": "81de0400ce680600790822004fe43f000f934200a9ac4500cd695800689a5e00c9566100a46670001d7c7100820276007c6c770089f47b0039847c0069327e0085647e00caa07e009a508c001082950052979a00c717a1005827ab00975faf004c93b5000852b600a3dfb600d8f0c500a6b0c60074cbcf007ec7d3003a23db0099bce000d752f20027bff2003492f50011a1f600bde2f700de98f900afc6f900932ffd00ed89fe00"
        }
    },
    "timestamp": "2019-11-02T18:13:50+08:00",
    "parentroot": "5f852ecc306c4ec7f792fbfb8f9d4b1e15b7c80cc4a4678f7ea28e1d3edb98f6",
    "parents": [
        "5f852ecc306c4ec7f792fbfb8f9d4b1e15b7c80cc4a4678f7ea28e1d3edb98f6"
    ],
    "children": [
        "3df0e5bb739d7ac0e4d34f621514d485dff3a3c0be31c161cc891787172caade"
    ]
}

```

### 2.getBlockByID
#### 函数名：getBlockByID {blockid} {fullTx}
#### 说明：
- blockid：所请求节点接收的区块顺序，节点内置id，与全网其他节点无关
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