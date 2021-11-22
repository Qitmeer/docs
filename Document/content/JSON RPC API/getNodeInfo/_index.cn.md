---
title: getNodeInfo
weight: 1
---

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



