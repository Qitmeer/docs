---
title: getBlockTotal
weight: 1
---

### GetBlockTotal
Return the total number blocks that this dag currently owned

#### Parameters
None

#### Returns
##### `(numeric)` total number 

#### Example

##### Request
```bash
curl --data '{"method":"getBlockTotal","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
34970
```

