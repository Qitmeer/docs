
---
title: txSign
weight: 1
---

### test_txSign
sign raw transactions

#### Prerequisite
test module enabled
```sh
modules=test
```


#### Parameters
1. `privkeyStr: (hex string)` private key 
2. `rawTxStr: (hex string)` raw transaction

#### Returns
##### `(array of string)` list of tip hashes

#### Example

##### Request
```bash
curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"test_txSign","params":["ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff", "0100000001f9802e5923afe50cbde3514c4169a8e84f83770c22e994cffb3c0a59e433d9cf01000000ffffffff01804a5d05000000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac00000000000000001141cb5f0100"],"id":1}' http://127.0.0.1:18131 | jq
```

##### Response
```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0100000001f9802e5923afe50cbde3514c4169a8e84f83770c22e994cffb3c0a59e433d9cf01000000ffffffff01804a5d05000000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac00000000000000001141cb5f016b483045022100b8ab0acf7f282e167669e3f20920c81b06554bc1fd5b41c4dd44ab4f3319a92f02200b664f920c77a7d8ac695380c22ec3131e2bd8f27617f84883fe9cf6d6bea0a1012102e8d120c3c729e636fe2909b02c65c025cb7f3f57d9891f4f566dd4724e82eb92"
}
```
