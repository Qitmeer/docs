---
title: getBlockCount
weight: 1
---

### getBlockCount
Returns the number of stable blocks .

#### Parameters
None

#### Returns
- `(numeric)` number of blocks, the network should have reached consensus on this number

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockCount","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
34787

