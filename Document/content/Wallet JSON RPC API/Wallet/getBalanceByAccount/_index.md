---
title: getBalanceByAccount
weight: 3
---

### wallet_getBalanceByAccount
Get balance by account

#### Parameters
1. `account: (string)` account name

#### Returns
1. `TotalAmount: (numeric)`  Total amount, spend amount+ spendable amount + frozen amount
2. `SpendAmount: (numeric)` spent amount, already confirmed
3. `UnspendAmount: (numeric)` spendable amount, not including frozen amount
4. `ConfirmAmount: (numeric)` frozen amount, waiting for conformation
5. `LockAmount: (numeric)` locked amount, waiting for unlock

#### Example
##### Request
```sh
 $ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getBalanceByAccount","params":["test", "MEER"],"id":1}' http://127.0.0.1:8130/api |jq .
```
##### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "TotalAmount": 900000000,
    "SpendAmount": 0,
    "LockAmount": 0,
    "UnspendAmount": 900000000,
    "ConfirmAmount": 0
  }
}

```