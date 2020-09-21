---
title: wallet_importPrivKey
weight: 3
---

## ImportPrivKey
imports a private key to the wallet and writes the new wallet to disk.

### Parameters
1. `accountName: (string)` name of the imported account. MUST be: "imported"
2. `privKey: (hex string)` private key

### Returns
#### Success
`null`

#### Error 
`-32000 -4` imported addresses must belong to the imported account

### Example
#### Request
```sh
curl --location --request POST 'http://127.0.0.1:8130/api/'  -u test:test -H 'Content-Type: application/json'  -d '{"id":1, "jsonrpc":"2.0","method":"wallet_importPrivKey","params":["imported", "9999999999999999999999999999999999999999999999999999999999999999"]}'
```
#### Response
```json
{"jsonrpc":"2.0","id":1,"result":null}
```
