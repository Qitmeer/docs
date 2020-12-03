
---
title: ui_walletStatus
weight: 3
---

## WalletStatus 
 wallet info

### Parameters

### Returns
#### Success
1. `status: (string)` 
   1. err - error happened
   2. nil - wallet not exists
   3. closed - wallet closed
   4. lock - wallet locked
   5. unlock - wallet unlocked


### Example
#### Request
```sh
curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"ui_walletStatus","params":[],"id":1}' http://127.0.0.1:8130/api | jq

```
#### Response
```json
{                                                                                                                                       
  "jsonrpc": "2.0",                                                                                                                     
  "id": 1,                                                                                                                              
  "result": {                                                                                                                           
    "stats": "lock"                                                                                                                     
  }                                                                                                                                     
}
```


