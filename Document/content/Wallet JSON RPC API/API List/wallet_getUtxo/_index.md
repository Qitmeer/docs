
---
title: wallet_getUtxo
weight: 3
---

### wallet_getUtxo
获取指定地址可用 UTXO

#### Parameters
1. `addr: (string)` 地址

#### Returns

#### Example
##### Request
```json
{"jsonrpc":"1.0","method":"wallet_getUTXO","params":["TmgD1mu8zMMV9aWmJrXqQYnWRhR9SBfDZG6"],"id":1}
```
##### Response
```json
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": [{
		"Txid": "54c47af3a17201c64a8f3b27164d4e09e8e38e05501b16bfd4f001caeddfa86a",
		"Index": 1,
		"Amount": 699925600
	}]
}}
```