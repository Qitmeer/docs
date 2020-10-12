
---
title: wallet_getBalanceByAddr
weight: 3
---

### wallet_getBalanceByAddr
Get balance by address

#### Parameters
1. `addr: (string)` address

#### Returns
1. `TotalAmount: (numeric)`  Total amount, spend amount+ spendable amount + frozen amount
2. `SpendAmount: (numeric)` spent amount, already confirmed
3. `UnspendAmount: (numeric)` spendable amount, not including frozen amount
4. `ConfirmAmount: (numeric)` frozen amount, waiting for conformation


#### Example
##### Request
```sh
$ curl -k -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getBalanceByAddr","params":["TmbC1Fx1UXNt7D6zpaj83UrAEW7MbcUWuQz"],"id":1}' http://127.0.0.1:8130/api

```
##### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "TotalAmount": 900000000,
    "SpendAmount": 0,
    "UnspendAmount": 900000000,
    "ConfirmAmount": 0
  }
}

```