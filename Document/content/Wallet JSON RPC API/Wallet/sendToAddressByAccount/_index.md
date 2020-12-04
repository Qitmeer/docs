---
title: sendToAddressByAccount
weight: 3
---

## wallet_sendToAddressByAccount 
send passed amount using specific account

### NOTE
* This function requires to the wallet to be unlocked.  See [wallet_unlock](../wallet_unlock/)
* The amount cannot exceed 21,000,000

### Parameters
1. `accountName: (string)` from account
2. `addressStr: (string)` to address
3. `amount: (numeric)` send amount coin
4. `comment: (string)` not used, reserved for future use
5. `commentTo: (string)`  not used, reserved for future use

### Returns
#### Success
`TxID: (hex string)` the TxID for the created transaction

#### Error 
`-32000` 
1. `-13` Enter the wallet passphrase with walletpassphrase first
2. `-32603` transaction output amount exceeds maximum value
3. `-32603` balance is not enough,please deduct the service charge


### Example
#### Request
```sh
$  curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_sendToAddressByAccount","params":["test", "Tmb1dCAB8ixNC6d2VtdCYZuhXBVPbnRVi7y", 0.999, "", ""],"id":1}' http://127.0.0.1:8130/api |jq .
```
#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "cfd933e4590a3cfbcf94e9220c77834fe8a869414c51e3bd0ce5af23592e80f9"
}
```
