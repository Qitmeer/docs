---
title: getBlockHeader
weight: 1
---

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

