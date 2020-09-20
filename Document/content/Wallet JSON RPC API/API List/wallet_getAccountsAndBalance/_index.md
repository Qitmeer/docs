---
title: wallet_getAccountsAndBalance
weight: 3
---

### wallet_getAccountsAndBalance
获取所有的账号和余额

#### Parameters

#### Returns


#### Example
##### Request
```json
{"jsonrpc":"1.0","method":"wallet_getAccountsAndBalance","params":[],"id":1
```
##### Response
```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "account": {
            "TotalAmount": 0,
            "SpendAmount": 0,
            "UnspendAmount": 0,
            "ConfirmAmount": 0
        },
        "default": {
            "TotalAmount": 280000000000,
            "SpendAmount": 0,
            "UnspendAmount": 280000000000,
            "ConfirmAmount": 0
        },
        "imported": {
            "TotalAmount": 11172999678800,
            "SpendAmount": 325000000000,
            "UnspendAmount": 8754999678800,
            "ConfirmAmount": 2418000000000
        }
    }
}
