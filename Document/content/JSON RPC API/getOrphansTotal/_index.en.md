---
title: getOrphansTotal
weight: 1
---

### GetOrphansTotal 
Return the total of orphans. Orphans are blocks with parents missing.

#### Parameters
None

#### Returns
##### `(numeric)` number of orphans

#### Example

##### Request
```bash
curl --data '{"method":"getOrphansTotal","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
0
```

