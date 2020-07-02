---
title: isBlue
weight: 1
---

### isBlue
Return the color of give block. Once block confirmed by main block, it is colored in line with consensus algorithm

#### Parameters
1. `hash (string)` block hash

#### Returns
##### `block color: (numeric)`
  - *Options*
     - `0 ` red: malfunctioning block, no block reward
     - `1 ` blue: honest block, reward granted
     - `2 ` cannot confirm: wait for confirmation by main block

#### Example

##### Request
```bash
curl --data '{"method":"GetOrphansTotal","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
0
```

