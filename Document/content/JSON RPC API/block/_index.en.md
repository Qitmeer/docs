---
title: The `Block` Module
---

## JSON-RPC methods

- [getBestBlockHash](#getBestBlockHash)
- [getBlock](#getBlock)
- [getBlockByID](#getBlockByID)
- [getBlockByOrder](#getBlockByOrder)
- [getBlockCount](#getBlockCount)
- [getBlockhash](#getBlockhash)
- [getBlockhashByRange](#getBlockhashByRange)
- [getBlockHeader](#getBlockHeader)
- [getBlockTotal](#getBlockTotal)
- [getBlockWeight](#getBlockWeight)
- [getCoinbase](#getCoinbase)
- [getMainChainHeight](#getMainChainHeight)
- [getOrphansTotal](#getOrphansTotal)
- [isBlue](#isBlue)
- [isCurrent](#isCurrent)
- [isOnMainChain](#isOnMainChain)
- [tips](#tips)

## JSON-RPC API Reference

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

***

### getBlock
Returns information about a block given its hash.

#### Parameters

1. `hash: (string)` the hash of the block.
2. `verbose: (boolean, optional, default=false)` specifies the block is returned as a JSON object instead of hex-encoded string.
3. `inclTx: (boolean, optional, default=true)` whether or not include transactions.
4. `fullTx: (boolean, optional, default=true)` specifies that each transaction is returned as a JSON object .

#### Returns
##### `(object,inclTx=false)` not show
  - `hash, confirmations, version, parentsroot, difficulty, pow`
    - reference [getBlockHeader](#getBlockHeader)


  - `weight: (numeric)` the weight of the block.
  - `height: (numeric)` the height of the block in the block DAG.
  - `order: (numeric)` the global order of the block.
  - `bits: (numeric)` the bits which represent the block difficulty.
  - `timestamp: (string)` block created time (ISO 8601 format).
  - `parents: (string)` blocks that are referenced from this block
  - `children: (string)` blocks that reference to this block

##### `(object, inclTx=true, fullTx=false)` show hash list of transactions
  - all fields with inclTx=false
  - `transactions: (array of string)`  transaction hashes
##### `(object, inclTx=true, fullTx=true)` transaction details
  - all fields with inclTx=false
  - `transactions: (array of object)`  transaction object
    - `hex: (string)`  hex-encoded transaction / hex-encoded bytes of the script. 
    - `txid: (string)`  the hash of the transaction WITHOUT signature. 
    - `txhash: (string)`  the hash of the transaction WITH signature. 
    - `size: (numeric)`  transaction size. 
    - `version: (enum)`  transaction version. 
      - `1` coinbase transaction
      - `2` ordinary transaction 
    - `locktime: (numeric)` the transaction lock time, cannot be spent before lock time.
    - `expire: (numeric)`  expired block height, tx cannot be spent after it.
    - `vin: (array of json objects)` the transaction inputs as json objects.
      - `coinbase: (string)` the hex-encoded bytes of the signature script.
      - `sequence: (numeric)` the script sequence number.
    - `vout: (array of json objects)` the transaction outputs as json objects.
      - `amount: (numeric)` the value in QIT.
      - `scriptPubKey: (json object)` the public key script used to pay coins.
        - `asm: (string)` disassembly of the script.
        - `hex: (string)` hex-encoded bytes of the script.
        - `reqSigs: (numeric)` the number of required signatures.
        - `type: (string)` the type of the script (e.g. 'pubkeyhash').
        - `addresses: (json array of string)` the  addresses associated with this output.

#### Example

##### Request
```bash
 curl --data '{"method":"getBlock","params":["11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3", true, true, false],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```
##### Response
```js
{
 "hash": "11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3",
 "txsvalid": true,
 "confirmations": 31785,
 "version": 11,
 "weight": 474,
 "height": 1,
 "txRoot": "7b73360b8099c1c4e91ab63ee71210202a802592491a90f0fd5c1275a5556d3d",
 "order": 1,
 "transactions": [
   {
     "hex": "010000000152868a9025d93bfa3948f8396c4779f735dcae7940d9e648555349c854c85cf8ffffffffffffffff01007841cb020000001976a9143be2e1e7eaffe6ee4c90d5db043576df7f2e174b88ac00000000000000000144510852fdfc072182654d1430353537373030363739313934373737393431302465316438316561652d313263662d343932302d623735312d323833383336616333306265",
     "txid": "7b73360b8099c1c4e91ab63ee71210202a802592491a90f0fd5c1275a5556d3d",
     "txhash": "e67a6d03533120d6fb280620caadcf3a47dee028d8ede9dbb6eef91b06bb336d",
     "size": 158,
     "version": 1,
     "locktime": 0,
     "expire": 0,
     "vin": [
       {
         "coinbase": "510852fdfc072182654d1430353537373030363739313934373737393431302465316438316561652d313263662d343932302d623735312d323833383336616333306265",
         "sequence": 4294967295
       }
     ],
     "vout": [
       {
         "amount": 12000000000,
         "scriptPubKey": {
           "asm": "OP_DUP OP_HASH160 3be2e1e7eaffe6ee4c90d5db043576df7f2e174b OP_EQUALVERIFY OP_CHECKSIG",
           "hex": "76a9143be2e1e7eaffe6ee4c90d5db043576df7f2e174b88ac",
           "reqSigs": 1,
           "type": "pubkeyhash",
           "addresses": [
             "TmUQjNKPA3dLBB6ZfcKd4YSDThQ9Cqzmk5S"
           ]
         }
       }
     ],
     "blockhash": "11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3",
     "confirmations": 31785
   }
 ],
 "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
 "bits": "2018000",
 "difficulty": 33652736,
 "pow": {
   "pow_name": "cuckaroo",
   "pow_type": 1,
   "nonce": 526,
   "proof_data": {
     "edge_bits": 24,
     "circle_nonces": "7a8e09004e040a00f6850e00582a1200d96613006fc91a000ca11c00f78124001b613600c266370037ef430073915000bbf85500b0795600691e5d00c7b35f0048bc670048897c00c50a7d006f22820038029100f4819a005864a6000aa9a600b5f0aa008169b200d1b4bb004cbfc100a32ac3001d6ac70045a1c900a95ecc002e55d70077ffd800a451d9007b38db00ab79e100dc14e600c5b6e9000efff0006821fa007650fb00"
   }
 },
 "timestamp": "2019-12-30T15:55:42+08:00",
 "parentroot": "caf26cf7705c0917bfb157150ab29f196465daf83c8ac1c82553aa9f207bd584",
 "parents": [
   "caf26cf7705c0917bfb157150ab29f196465daf83c8ac1c82553aa9f207bd584"
 ],
 "children": [
   "0ea57734fc4baeb7fb8669a7e52b948fb94277a3f0a08caaf25592c7fef7c965"
 ]
}
```

***

### getBlockByID
Returns information about a block given its local resource ID.

#### Parameters

1. `block ID: (numeric, required)` the local resource ID of the block, resource ID doesn't reach consensus on the network, it is generated by each node when accepting a new block. 
2. `verbose: (boolean, optional, default=false)` reference [getBlock](#getBlock).
3. `inclTx: (boolean, optional, default=true)` reference [getBlock](#getBlock).
4. `fullTx: (boolean, optional, default=true)` reference [getBlock](#getBlock).

#### Returns
reference [getBlock](#getBlock)

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockByID","params":[2, true, true, false],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response

reference [getBlock](#getBlock)

***

### getBlockByOrder
Returns information about a block given its global order.

#### Parameters

1. `block ID: (numeric, required)` the local resource ID of the block, resource ID doesn't reach consensus on the network, it is generated by each node when accepting a new block. 
2. `verbose: (boolean, optional, default=false)` reference [getBlock](#getBlock).
3. `inclTx: (boolean, optional, default=true)` reference [getBlock](#getBlock).
4. `fullTx: (boolean, optional, default=true)` reference [getBlock](#getBlock).

#### Returns
reference [getBlock](#getBlock)

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockByID","params":[2, true, true, false],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response

reference [getBlock](#getBlock)

***

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

***

### getBlockhash
Returns hash of the block  at the given order.

#### Parameters
1. block order (numeric, required)

#### Returns
- `(string)` block hash 

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockhash","params":[2],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
0ea57734fc4baeb7fb8669a7e52b948fb94277a3f0a08caaf25592c7fef7c965

***

### getBlockhashByRange
Returns hash of the block  at the given order.

#### Parameters
1. start order (numeric, required)
1. end order (numeric, required)

#### Returns
- `(array of string)` list of block hashes 

#### Example

##### Request
```bash
 curl --data '{"method":"getBlockhashByRange","params":[1, 9],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
[
  "11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3",
  "0ea57734fc4baeb7fb8669a7e52b948fb94277a3f0a08caaf25592c7fef7c965",
  "03879bf60c08cca7885790661e0e96147fc0012428d6b326eb5ffb2eb0f3b073",
  "18917e39ec36a68843024b9212934a3a8b23d3f5629987d0565fb74c7683f13b",
  "0385e16851b36983a1110e8cbf9885005e76a38be0983a2520e72c06da98f590",
  "030fcf757bef879016095dd6ef40503418758632d4817ef5a20fd7ab87c427c7",
  "1f876a43c630c3f0e065668ff12b88a0403bd8f9aa790b39f6982428c7c46272",
  "1cdcbe73bfc539086296df62a92cd027b89d01d370826b2ac763fc3997dc7e8a"
]
```

***

### GetBlockHeader
Returns hex-encoded bytes of the serialized block header.

#### Parameters
1. `block hash: (string)` the hash of the block.
2. `verbose: (boolean)` specifies the block header is returned as a JSON object instead of a hex-encoded string.

#### Returns
##### `(object)` deserialized block data
- hash: (string) the hash of the block (same as provided).
- confirmations: (numeric) the number of confirmations.
- version: (numeric) the block version.
- parentsroot: (string) The merkle root of the previous parent blocks (the dag layer)
- txRoot: (string) the root of the transaction trie of the block.
- stateRoot: (string) the root of the final state trie of the block.
- difficulty: (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.
-  pow: (object) mining info
  - pow_name: (string)  mining algorithm name. 
    - *Options*
      - blak2bd: double blak2b, CPU based 
      - cuckroo: ASIC proof, GPU based 
      - cucktoo: ASIC friendly, GPU based
  - pow_type: (numeric) mining algorithm type. 
    - *Options*
      - 0: blake2bd
      - 1: cuckroo
      - 2: cucktoo
  - nonce: (numeric) - the block nonce.
  - proof_data: (object) - cuckroo algorithm proof
     - "edge_bits": (numeric) - number of edge bit, the bigger the harder
     - "circle_nonces": (string) - circle nonces, raw proof data 
- hash: (string) the hash of the block (same as provided).
- confirmations: (numeric) the number of confirmations.
- version: (numeric) the block version.

- layer: (string) length of the longest path from genesis to this block
- time: (string) the block time in seconds since 1 Jan 1970 GMT.

##### `(string)` hex-encoded bytes of the serialized block 

#### Example

##### Request
```bash
curl --data '{"method":"getBlockHeader","params":["11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3", true],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
{
  "hash": "11dbd3e6202f41eba102277bdb65adff82899219a870295ed8424b7c035af0f3",
  "confirmations": 32263,
  "version": 11,
  "parentroot": "caf26cf7705c0917bfb157150ab29f196465daf83c8ac1c82553aa9f207bd584",
  "txRoot": "7b73360b8099c1c4e91ab63ee71210202a802592491a90f0fd5c1275a5556d3d",
  "stateRoot": "0000000000000000000000000000000000000000000000000000000000000000",
  "difficulty": 33652736,
  "layer": 1,
  "time": 1577692542,
  "pow": {
    "pow_name": "cuckaroo",
    "pow_type": 1,
    "nonce": 526,
    "proof_data": {
      "edge_bits": 24,
      "circle_nonces": "7a8e09004e040a00f6850e00582a1200d96613006fc91a000ca11c00f78124001b613600c266370037ef430073915000bbf85500b0795600691e5d00c7b35f0048bc670048897c00c50a7d006f22820038029100f4819a005864a6000aa9a600b5f0aa008169b200d1b4bb004cbfc100a32ac3001d6ac70045a1c900a95ecc002e55d70077ffd800a451d9007b38db00ab79e100dc14e600c5b6e9000efff0006821fa007650fb00"
    }
  }
}
```

***

### GetBlockTotal
Return the total number blocks that this dag currently owned

#### Parameters
None

#### Returns
##### `(numeric)` total number 

#### Example

##### Request
```bash
curl --data '{"method":"getBlockTotal","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
34970
```

***

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

***

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

***

### GetOrphansTotal 
Return the total of orphans. Orphans are blocks with parents missing.

#### Parameters
None

#### Returns
##### `(numeric)` number of orphans

#### Example

##### Request
```bash
curl --data '{"method":"getOrphansTotal","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq .
```

##### Response
```js
0
```

***

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

***

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

*** 
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

*** 
### tips
None

#### Parameters

#### Returns
##### `(array of string)` list of tip hashes

#### Example

##### Request
```bash
 curl --data '{"method":"tips","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 |jq . 
```

##### Response
```js
[
  "00001a78e4405cf0b1eeebf4c707bbbeea3fbad53dd60718092b08c6fb1cb95f"
]
```