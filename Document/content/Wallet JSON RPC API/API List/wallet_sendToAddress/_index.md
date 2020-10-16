---
title: wallet_sendToAddress
weight: 3
---

## wallet_sendToAddress
sends the passed amount to the given address.

**NOTE:** This function requires to the wallet to be unlocked.  See [wallet_unlock](../wallet_unlock/)

### Parameters
`address: (hex string)` the given address
`amount: (numeric)` passed amount

### Returns
#### Success
`TxID: (hex string)` the TxID for the created transaction

#### Error 
 `-32000` 
    `-13` Enter the wallet passphrase with walletpassphrase first


### Example
#### Request
```sh
$ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_sendToAddress","params":["Tmdcmmo7JqxxwHy6r46Sx2ZRbVF2dSjG9mm", 1 ],"id":1}' http://127.0.0.1:8130/api |jq .
```

#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "86140f1fa1e7d95707ec7e61748b91838e24a00ca8803f299c7caca591ff1af4"
}
```