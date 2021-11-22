---
title: getTips
weight: 1
---

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


