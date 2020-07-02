---
title: isOnMainChain
weight: 1
---

### isOnMainChain
Query whether or not a given block is on the main chain.

#### Parameters
1. `hash (string)` block hash

#### Returns
##### `(bool)` whether or not on the main chain

#### Example

##### Request
```bash
curl --data '{"method":"isOnMainChain","params":["11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3"],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
true
```

