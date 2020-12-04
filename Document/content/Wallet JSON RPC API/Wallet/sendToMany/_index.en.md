---
title: sendToMany 
weight: 3
---

## wallet_sendToMany
sends multiple amounts to multiple addresses using the provided account as a source of funds in a single transaction.  Only funds with the default number of minimum confirmations will be used.

### NOTE
* This function requires to the wallet to be unlocked.  See [wallet_unlock](../wallet_unlock/)
* The amount cannot exceed 21,000,000

### Parameters
`addAmounts: (map[address:string]amount:numeric)`  address to amount pairs

### Returns
#### Success
`TxID: (hex string)` the TxID for the created transaction

#### Error 
 `-32000` 
    `-13` Enter the wallet passphrase with walletpassphrase first


### Example
#### Request
```sh
$ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_sendToMany","params":[{"TmVLfSPy3NZY1uDjJka92hqpPJR9k2XztQb":0.9, "TmR1kwdfb6pyQRNoJJMU2M62qEqJzqXPNBw":0.99} ],"id":1}' http://127.0.0.1:8130/api |jq .

```

#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "75ea0ca21e7626941574df0d0d64e69793e806216d34cfd8400ef09249fc44c7"
}
```