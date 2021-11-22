---
title: getBestBlockHash
weight: 1
---

### getBestBlockHash
Returns the hash of the of the best (most recent) block in the longest block chain.

#### Parameters
None
#### Returns
##### `(string)` - best block hash

#### Example

##### Request
```bash
curl --data '{"method":"getBestBlockHash","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 
```

##### Response
```js
"000005c905e232a3320c35e38ec2a7f8f9d03e3cc28faef007cc46f273835f4b"
```



