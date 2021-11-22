---
title: getMainChainHeight
weight: 1
---

### getMainChainHeight 
Return the current height of DAG main chain

#### Parameters
None

#### Returns
##### `(array of string, verbose=true)`
  1. `(hex string)` block height
  2. `(hex string)` nonce
  3. `(hex string)` custom data 1, filled by miner, ASCII string
  4. `(hex string)` custom data 2
  5. ...

##### `(array of string, verbose=false)` total number 
  1. `(hex string)` custom data 1, filled by miner, ASCII string
  2. `(hex string)` custom data 2
  3.  ...

#### Example

##### Request
```bash
curl --data '{"method":"getMainChainHeight","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
32522
```

