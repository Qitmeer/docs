---
title: getBestBlockHash
weight: 1
---

## getBestBlocktHash
### 函数名：getBestBlockHash
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



