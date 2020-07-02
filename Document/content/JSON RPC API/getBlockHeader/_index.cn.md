---
title: getBlockHeader
weight: 1
---

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

