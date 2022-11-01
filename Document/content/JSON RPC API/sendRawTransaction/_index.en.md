---
title: sendRawTransaction
weight: 3
---

### sendRawTransaction
send raw transactions

#### Parameters
1. `hexTx: (hex string)`  hex string of signed transaction
2. `allowHighFees: (bool, default=false)` if allows high fee

Note: The second parameter "allowHighFees" will allow high fee which means that the full balance in addition to the amount transferred out is treated as fees when the value is true. Please use the default value "false".

#### Returns
##### `(hex string)` 

#### Errors

1. Signature failed
    * Example
```json
{
   "code": -32000,
   "message": "Rule Error : Rejected transaction c69ea9d7457379984d5a0af0568f296289ec791bbd522d2f6057924ed12b8089: failed to validate input c69ea9d7457379984d5a0af0568f296289ec791bbd522d2f6057924ed12b8089:0 which references output {cfd933e4590a3cfbcf94e9220c77834fe8a869414c51e3bd0ce5af23592e80f9 0} - verify failed (input script bytes 47304402203aa2f8bcfac55e76b84320a119dcd73955e2c644abe590b8ce99abaf7bf51f5902205e973da66669d80009d6f5d848dd0bed50abf1b69acd43eda02bdb6cfdd0157f012102e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92, prev output script bytes 76a914844d0a82845bccd469afc5cb78d8ffaa3142edea88ac)"
}

```

2. exceed high fee
    * example
```json
 {
    "code": -32000,
    "message": "Deserialization Error : rejected: failed to process transaction 0766b6dfd578952f52842cc4fb72f95f40258ee8aadff41897567a82c2b92e71: transaction 0766b6dfd578952f52842cc4fb72f95f40258ee8aadff41897567a82c2b92e71 has 420995400 fee which is above the allowHighFee check threshold amount of 20100000 (= 201 byte * 10000 AtomMEER/kB * 10000)"
  }

```


#### Example

##### Request
```bash
curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"sendRawTransaction","params":["0100000001f9802e5923afe50cbde3514c4169a8e84f83770c22e994cffb3c0a59e433d9cf01000000ffffffff01804a5d05000000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac00000000000000001141cb5f016b483045022100b8ab0acf7f282e167669e3f20920c81b06554bc1fd5b41c4dd44ab4f3319a92f02200b664f920c77a7d8ac695380c22ec3131e2bd8f27617f84883fe9cf6d6bea0a1012102e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92", false],"id":1}' http://127.0.0.1:18131 | jq

```

##### Response
```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0766b6dfd578952f52842cc4fb72f95f40258ee8aadff41897567a82c2b92e71"
}


```

