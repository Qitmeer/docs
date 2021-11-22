---
title: isCurrent
weight: 1
---

### isCurrent
Returns if  we are synced with our peers

#### Parameters
None

#### Returns
##### `(bool)` whether or not synced 

#### Example

##### Request
```bash
curl --data '{"method":"isCurrent","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
true
```

