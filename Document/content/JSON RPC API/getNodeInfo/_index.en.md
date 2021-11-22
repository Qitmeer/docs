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
    - `ID: (string)` -  mutipleaddress ID 
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
        - `current_diff: (numeric)`  - current difficulty 
    - `confirmations: (numeric)` - number of blocks to wait for safe confirmation
    - `coinbasematurity: (numeric)` - number of blocks to wait for coinbase to be spent
    - `modules: (array)` - loaded modules; qitmeer, miner, test by default
    - `network: (string)` - current network
    - `connections: (numeric)` - current connections 

#### Example

Request
```bash
curl --data '{"method":"getNodeInfo","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' https://127.0.0.1:18131 | jq
```

Response
```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "ID": "16Uiu2HAmJq8eGgj7aUE9DANQUssg6b4T1jRJDq4tvwKjnCZKk1cE",
    "address": [
      "/ip4/10.0.0.6/tcp/18150/p2p/16Uiu2HAmJq8eGgj7aUE9DANQUssg6b4T1jRJDq4tvwKjnCZKk1cE",
    ],
    "version": 100300,
    "buildversion": "0.10.3+dev-1742484",
    "protocolversion": 33,
    "totalsubsidy": 991716000000000,
    "graphstate": {
      "tips": [
        "e6787427f5f4704eed0651181c4f3341fb1acaf1cbc63b215865da22ea6442b6 main",
        "3b7b986370bc4cf5d6c14102ef2c198ff23e1e5b8e883208a0c1c8440e9f04f9"
      ],
      "mainorder": 114143,
      "mainheight": 48694,
      "layer": 49908
    },
    "timeoffset": -1,
    "pow_diff": {
      "current_diff": 2933.93160025
    },
    "confirmations": 10,
    "coinbasematurity": 720,
    "modules": [
      "qitmeer",
      "miner",
      "test",
      "log"
    ],
    "network": "testnet",
    "connections": 21
  }
}
```

