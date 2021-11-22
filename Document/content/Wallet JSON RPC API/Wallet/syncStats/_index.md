
---
title: syncStats
weight: 3
---

### wallet_syncStats
查看当前钱包同步高度

#### Parameters

#### Returns


#### Example
##### Request
```json
{"jsonrpc":"1.0","method":"wallet_syncStats","params":[],"id":1}
```
##### Response
```json
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"Height": 20460
	}
}
```