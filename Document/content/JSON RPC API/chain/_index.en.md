---
title: The `blockchain` Module
---

## JSON-RPC methods

- [getNodeInfo](#getNodeInfo)
- [getPeerInfo](#getPeerInfo)

## JSON-RPC API Reference

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

***

### getPeerInfo

Returns data about each connected network peer as an array of json objects.

#### Parameters

None

#### Returns

- `result: array` 
    - `uuid: (string)` -  global peer ID 
    - `id: (numeric)` -  local peer ID 
    - `addr: (string)` the ip address and port of the peer.
    - `addrlocal: (string)` -  local IP address and port bound to connect peer
    - `services: (string)` the services supported by the peer.
    - `relaytxes: (bool)` - if relay transactions
    - `lastsend: (numeric)` - time the last message was sent in seconds since 1 Jan 1970 GMT. 
    - `lastrecv: (numeric)` -  time the last message was received in seconds since 1 Jan 1970 GMT. 
    - `bytessent: (numeric)` -  total bytes sent
    - `bytesrecv: (numeric)` - total bytes received 
    - `conntime: (numeric)` - time the connection was made in seconds since 1 Jan 1970 GMT.
    - `pingtime: (numeric)` number of microseconds the last ping took.
    - `version: (numeric)` the protocol version of the peer.
    - `subver: (string)` the user agent of the peer.
    - `inbound: (boolean)` whether or not the peer is an inbound connection.
    - `syncnode: (boolean)` whether or not the peer is the sync peer.
    - `graphstate: (object)`  - graph state of DAG
        - `tips: (array)`  - array of tips, no referenced blocks
        - `mainorder: (string)`  - order of main chain
        - `mainheight: (numeric)`  - height of main chain
        - `layer: (numeric)`  - max height of all blocks

startingheight: (numeric) the latest block height the peer knew about when the connection was established.
currentheight: (numeric) the latest block height the peer is known to have relayed since connected.


#### Example

Request
```bash
curl --data '{"method":"getPeerInfo","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 | jq
```

Response
```js
[
    {
      "uuid": "3917cbb8-a910-4bf6-b82e-dd9f191f9c20",
      "id": 218,
      "addr": "104.224.174.141:18130",
      "addrlocal": "192.168.50.170:58733",
      "services": "00000009",
      "relaytxes": true,
      "lastsend": 1578465326,
      "lastrecv": 1578465300,
      "bytessent": 58077,
      "bytesrecv": 39464,
      "conntime": 1578462700,
      "timeoffset": -291,
      "pingtime": 218202,
      "version": 19,
      "subver": "qitmeer:0.8.5",
      "inbound": false,
      "banscore": 0,
      "syncnode": false,
      "graphstate": {
        "tips": [
          "000060719d3b030a079daea3ae09f4317402df74af9a6520f9b54fa095cbd2fc main"
        ],
        "mainorder": 28867,
        "mainheight": 26478,
        "layer": 26479
      }
    }
]

```
