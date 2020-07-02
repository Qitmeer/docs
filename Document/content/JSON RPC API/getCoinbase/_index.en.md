---
title: getCoinbase
weight: 1
---

### GetCoinbase 
Return the coin base data of given block

#### Parameters
1. `block hash: (string)`  block hash
2. `verbose: (bool, default: false)` whether or not show mining info 

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
curl --data '{"method":"getCoinbase","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
[
  "01",
  "52fdfc072182654d",
  "3035353737303036373931393437373739343130", # "05577006791947779410"
  "65316438316561652d313263662d343932302d623735312d323833383336616333306265" # "e1d81eae-12cf-4920-b751-283836ac30be"
]
```

