
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
```json
{"jsonrpc":"1.0","method":"wallet_getBalanceByAddr","params":["TmfDniZnvsjdH98GsH4aetL3XQKFUTWPp4e",1],"id":16}
```
##### Response
```json
{
	"jsonrpc": "2.0",
	"id": 16,
	"result": {
		"TotalAmount": 400000000,
		"SpendAmount": 0,
		"UnspendAmount": 400000000,
		"ConfirmAmount": 0
	}
}
```