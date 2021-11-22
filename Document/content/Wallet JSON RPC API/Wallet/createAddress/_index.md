---
title: createAddress
weight: 3
---

## wallet_createAddress 
returns the next external chained address for a wallet.

### Parameters
1. `accountName: (string)` name of the account on which the address created

### Returns
### Success
new address (base58)

### Error
`-32000` account name '*test_account*' not found


### Example
#### Request
```sh
curl -k -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_createAddress","params":["test_account"],"id":1}' http://127.0.0.1:8130/api
```
#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "Tmdy4W4FeDD2M8Tm8syZJmR2BPdug4Zeozj"
}

```
