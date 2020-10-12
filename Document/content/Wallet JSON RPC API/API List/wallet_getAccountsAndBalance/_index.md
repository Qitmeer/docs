---
title: wallet_getAccountsAndBalance
weight: 3
---

### wallet_getAccountsAndBalance
list balance of all accounts

#### Parameters
None

#### Returns
`[account name]:(account)`

`account`
1. `TotalAmount: (numeric)`  Total amount, spend amount+ spendable amount + frozen amount
2. `SpendAmount: (numeric)` spent amount, already confirmed
3. `UnspendAmount: (numeric)` spendable amount, not including frozen amount
4. `ConfirmAmount: (numeric)` frozen amount, waiting for conformation
...

#### Example
##### Request
```sh
 $ curl -sk -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_getAccountsAndBalance","params":[],"id":1}' http://127.0.0.1:8130/api |jq .
```
##### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "default": {
      "TotalAmount": 0,
      "SpendAmount": 0,
      "UnspendAmount": 0,
      "ConfirmAmount": 0
    },
    "imported": {
      "TotalAmount": 676444792042,
      "SpendAmount": 1366909827084,
      "UnspendAmount": 676444792042,
      "ConfirmAmount": 0
    },
    "test": {
      "TotalAmount": 900000000,
      "SpendAmount": 0,
      "UnspendAmount": 900000000,
      "ConfirmAmount": 0
    },
    "test_account": {
      "TotalAmount": 0,
      "SpendAmount": 0,
      "UnspendAmount": 0,
      "ConfirmAmount": 0
    }
  }
}

