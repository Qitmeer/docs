
---
title: wallet_getBalanceByAddr
weight: 3
---

### wallet_getBalanceByAddr
获取地址余额

#### Parameters
1. `addr: (string)` 地址

#### Returns


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