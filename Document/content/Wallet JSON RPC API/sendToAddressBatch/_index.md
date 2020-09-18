
---
title: wallet_sendToAddressBatch
weight: 3
---

### wallet_sendToAddressBatch
单地址批量交易

#### Parameters
1. `addr: (string)` 地址
1. `amount: (string)` 金额

#### Returns


#### Example
##### Request
```json
{
	"id": 1578639635748,
	"method": "wallet_sendToAddressBatch",
	"params": [{
		"TmeUg4pxc14y64J5BQj4M7jKEryeYfJ4APh": 0.1,
		"TmU3Xwo1rnh4hTKBwifDYAccDrF3kxXaEFe": 0.2,
		"TmjbGfbcMN1nVVHdcvzmPA4ksKqGq4eEkXu": 0.3,
		"TmmWRCMcRZ1ZGdQEw2BwZ3ibsobATw4KTrw": 0.4
	}]
}
```
##### Response
```json
{
    "jsonrpc": "2.0",
    "id": 1578639635748,
    "result": "d7a7d24d47bb66ad3d3185764808af730c9a9dbb5970686cf6e5a1d5f249923c"
}
```