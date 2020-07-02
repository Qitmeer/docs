---
title: getNodeInfo
weight: 1
---

### getNodeInfo
Return info of requested node

#### Parameters

None

#### Returns

- `result: object` 
    - `UUID: (string)` -  unique ID 
    - `version: (numeric)` - The version of the node as a numeric.
    - `buildversion: (string)` - build version 
    - `protocolversion: (numeric)` -  The protocol version of the node. 
    - `totalsubsidy: (numeric)` -  total subsidy to be mined
    - `graphstate: (object)`  - graph state of DAG
        - `tips: (array)`  - array of tips, no referenced blocks
        - `mainorder: (string)`  - order of main chain
        - `mainheight: (numeric)`  - height of main chain
        - `layer: (numeric)`  - max height of all blocks
    - `timeoffset: (numeric)`  - The node clock offset in seconds
    - `connections: (numeric)`  - number of connections
    - `pow_diff: (object)`  - difficulty of POW
        - `blake2bd_diff: (numeric)`  - difficulty of Blake2B, pure CPU mining
        - `cuckaroo_diff: (numeric)`  - difficulty of cuckaroo, anti-ASIC GPU mining
        - `cuckatoo_diff: (numeric)`  - difficulty of cuckatoo, ASIC friendly GPU mining 
    - `testnet: (boolean)` - launch test net
    - `mixnet: (boolean)` - launch mix net
    - `confirmations: (numeric)` - number of blocks to wait for safe confirmation
    - `coinbasematurity: (numeric)` - number of blocks to wait for coinbase to be spent
    - `error: (string)` - error message if happened
    - `modules: (array)` - loaded modules; qitmeer, miner, test by default

#### Example

Request
```bash
curl --data '{"method":"getNodeInfo","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 | jq
```

Response
```js
{
    "UUID": "2e3dddbe-2646-4964-b4ad-5a9b9fd83010",
    "version": 80500,
    "buildversion": "0.8.5+dev-30736c5",
    "protocolversion": 19,
    "totalsubsidy": 343068000000000,
    "graphstate": {
      "tips": [
        "00004d5e83f46cf14de8e4a8c76cf6831d1a294654076eabda19bf939a1e5786 main"
      ],
      "mainorder": 28656,
      "mainheight": 26284,
      "layer": 26285
    },
    "timeoffset": 0,
    "connections": 8,
    "pow_diff": {
      "blake2bd_diff": 1,
      "cuckaroo_diff": 23554,
      "cuckatoo_diff": 1
    },
    "testnet": true,
    "mixnet": false,
    "confirmations": 10,
    "coinbasematurity": 720,
    "errors": "",
    "modules": [
      "qitmeer",
      "miner",
      "test"
    ]
  }

```

