---
title: recoverWallet
weight: 3
---

## ui_recoverWallet
 Recover Wallet wallet by mnemonic

### Parameters
1. `mnemonic: (hex string)` the mnemonic words
2. `walletPass: (string)`   wallet password
3. `unlockPass: (string)` unlock password

### Returns
#### Success
`null`

#### Error 
`-32000`  
   1. seed hex err: Invalid menomic 
   2. wallet exist

### Example
#### Request
```sh
curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"ui_recoverWallet","params":["river immense robust crucial patrol kingdom trick enter jacket similar feed pitch juice focus ramp merry occur blast pepper case gentle left sea margin", "walletPass", "unlockPass"],"id":1}' http://127.0.0.1:8130/api | jq

```
#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": null
}

```


