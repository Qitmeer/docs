---
title: getBlockhash
weight: 1
---

### getBlockhash
Returns hash of the block  at the given order.

#### Parameters
1. block order (numeric, required)

#### Returns
- `(string)` block hash 

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockhash","params":[2],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```
