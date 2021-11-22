---
title: getBlockCount
weight: 1
---

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

