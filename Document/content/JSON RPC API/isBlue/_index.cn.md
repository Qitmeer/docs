---
title: isBlue
weight: 1
---


## isBlue
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


