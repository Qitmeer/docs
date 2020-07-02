---
title: getMainChainHeight
weight: 1
---


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


