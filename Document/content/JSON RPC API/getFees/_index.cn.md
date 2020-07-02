---
title: getFees
weight: 1
---


## getFees
### 函数名：getFees {blockhash}
### 说明：得到区块的交易手续费
- blockhash : 256位区块hash

#### 实例1
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getFees","params":["00001ae85f5c90cc2f1f9ae5b1ac148145555d884f2c7d986cb3df250c8c3ecc"],"id":1}' https://127.0.0.1:18131

```

输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 0
}
```

#### 实例2
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getFees","params":["0001e69751e25747286d905964ed3c838b63e185074405eb2a7121cf0a72e259"],"id":1}' https://127.0.0.1:18131
```

输出
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 49000
}
```

