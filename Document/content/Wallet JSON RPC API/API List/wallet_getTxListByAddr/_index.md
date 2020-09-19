---
title: wallet_getTxListByAddr
weight: 3
---

### wallet_getTxListByAddr 
创建地址

#### Parameters
1. `addr: (string)` 地址
1. `type: (number)` 0: in tx; 1: out tx; 2: all tx 
1. `page  : (number)` 页号
1. `pageSize`: (string)` 页大小


#### Returns


#### Example
##### Request
```json
{"id":1574750774018,"method":"wallet_getTxListByAddr","params":["TmhJcjphz3Y3jRysKT56JaH8m9pzAzsFMu7",2,-1,100]}
```
##### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1574750774018,
    "result": {
        "Total": 1,
        "Page": 1,
        "PageSize": 1000000000,
        "transactions": [
            {
                "hex": "",
                "txid": "47879fb9dea684e4ce6f24f30812d3832d11fee34400754c6d8b34cd7d7eba8f",
                "txhash": "937de7e15ec48e9cd58d79c594e7395015d5c663924ab5af929a9ef5e5f2e446",
                "size": 377,
                "version": 1,
                "locktime": 0,
                "expire": 0,
                "vin": [
                   ...
                ],
                "vout": [
                   ...
                ],
                "blockhash": "026c6c85a1ae0183fe2e8bfda3450b9990acf9b8c4af3e995f9e361c7bb3d4cd",
                "confirmations": 0
            }
        ]
    }
}