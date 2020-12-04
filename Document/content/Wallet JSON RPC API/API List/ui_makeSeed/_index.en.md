
---
title: ui_makeSeed
weight: 3
---

## MakeSeed 
 make wallet HD seed and mnemonic

### Parameters

### Returns
#### Success
1. `seed: (hex string)` a cryptographically secure random seed
2. `mnemonic: (array of string)`  the mnemonic words for the given seed


### Example
#### Request
```sh
curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"ui_makeSeed","params":[],"id":1}' http://127.0.0.1:8130/api | jq
```
#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "seed": "0d82f3214e900c039c8e05c04bef5f22bdf5804344e69e8f7426e90fabb0eb178a8c4f99850c77be09f609b7145799fb0772c1c0c1087acd55868240755a437a",
    "mnemonic": "river immense robust crucial patrol kingdom trick enter jacket similar feed pitch juice focus ramp merry occur blast pepper case gentle left sea margin"
  }
}

```


