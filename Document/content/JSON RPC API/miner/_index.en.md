---
title: The `Miner` Module
---

## JSON-RPC methods

- [getBlockTemplate](#getBlockTemplate)
- [submitBlock](#submitBlock)

## JSON-RPC API Reference

### GetBlockTemplate
Gets a block template for use with mining software.

#### Parameters
1. `capabilities: (array of enum)`:  client side supported feature. Note: 
coinbasetxn and coinbasevalue are mutually exclusive.
    - *coinbasetxn* information for coinbase transaction, miningaddr is required in node config.
    - *coinbasevalue* maximum allowable input to coinbase transaction 

#### Returns
##### `(object, capabilities=["coinbasetxn"])`
- `stateroot: (string)` the root of the final state trie of the block.
- `curtime: (numeric)` current timestamp in seconds since epoch (Jan 1 1970 GMT).
- `height: (numeric)` the height of the block in the block DAG.
- `blues: (numeric)` blue set size of block's past set,
- `previousblockhash: (string)` The merkle root of the previous parent blocks (the dag layer)
- `sigoplimit: (numeric)` limit of sigops in blocks 
- `sizelimit: (numeric)` limit of block size 
- `weightlimit: (numeric)` limit of block weight
- `parents: (array of object)` list of parent hashes
    - `data: (string)` parent hash encoded in hexadecimal (byte-for-byte)
    - `hash: (string)` parent hash encoded in little-endian hexadecimal
- `transactions: (array of object)` list of transaction 
    - `data: (string)` transaction data encoded in hexadecimal (byte-for-byte)
    - `hash: (string)` hash encoded in little-endian hexadecimal (including witness data)
    - `depends: (array of numeric)` transactions before this one (by 1-based index in 'transactions' list) that must be present in the final block if this one is  
    - `fee: (numeric)` difference in value between transaction inputs and outputs (in QITs); for coinbase transactions, this is a negative Number of the total collected block fees (ie, not including the block subsidy); if key is not present, fee is unknown and clients MUST NOT assume there isn't one 
    - `sigops: (numeric)` total SigOps cost, as counted for purposes of block limits; if key is not present, sigop cost is unknown and clients MUST NOT assume it is zero 
    - `weight: (numeric)` total transaction weight, as counted for purposes of block limits
- `version: (numeric)` The preferred block version
- `coinbaseaux: (object)` data that should be included in the coinbase's scriptSig content
    - `flags: (string)` key name is to be ignored, and value included in scriptSig
- `coinbasevalue: (numeric)` maximum allowable input to coinbase transaction, including the generation award and transaction fees (in QITs) 
- `longpollid: (string)` template ID, the format is "parent root - generate time"
- `pow_diff_reference: (object)` - mining difficulty
  - `blake2bd_bits: (string)`: double blake2b compressed target of next block,
  - `blake2bd_target: (string)`: double blake2b hash target of next block,
  - `cuckaroo_min_diff: (numeric)`: cuckaroo min difficulty
  - `cuckatoo_min_diff: (numeric)`: cuckatoo min difficulty
- `maxtime: (numeric)` The maximum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
- `mintime: (numeric)` The minimum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
- `mutable: (array of string)` list of ways the block template may be changed, including 'time', 'transactions/add', 'prevblock', "coinbase/append"
- `noncerange :(string)` A range of valid nonces
- `capabilities :(array of string)` list of capabilities, not implemented yet, only 'proposal' always listed 

##### `(object, capabilities=["coinbasevalue"])` - best block hash
almost identical to result of capabilities = coinbasevalue, just coinbasevalue and coinbaseaux substituted with coinbasetxn 
- `coinbasetxn: (object)` information for coinbase transaction, data structure is identical to transactions field

#### Example

##### Request
```bash
curl --data '{"method":"getBestBlockHash","params":[],"jsonrpc":"2.0","id":1}' -s -k -u "rpcuser:rpcpass"  -H 'Content-Type: application/json' http://127.0.0.1:18131 
```

##### Response
```js
{
    "stateroot": "0000000000000000000000000000000000000000000000000000000000000000",
    "curtime": 1578717731,
    "height": 34902,
    "blues": 37478,
    "previousblockhash": "000028f561e25022c4c0bbf1b08943da39ef1a134556c742a5b2c8accd3d3fd6",
    "sigoplimit": 80000,
    "sizelimit": 1048576,
    "weightlimit": 4000000,
    "parents": [
      {
        "data": "d63f3dcdacc8b2a542c75645131aef39da4389b0f1bbc0c42250e261f5280000",
        "hash": "000028f561e25022c4c0bbf1b08943da39ef1a134556c742a5b2c8accd3d3fd6"
      }
    ],
    "transactions": [],
    "version": 11,
    "coinbasetxn": {
      "data": "0100000001905e3ac0bc4050ce1ba4c4b4fc6cef8f2d6a8e1e3b49917ca65641b0feb21c20ffffffffffffffff01007841cb020000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac0000000000000000011703568800082ad99948a98c989f092f7169746d6565722f",
      "hash": "fcb7e486a557dbe69b8bd0bf2f5602fb8c22ee2ddc6ad4a5070a8c261f182ede",
      "depends": [],
      "fee": 0,
      "sigops": 1,
      "weight": 0
    },
    "longpollid": "000028f561e25022c4c0bbf1b08943da39ef1a134556c742a5b2c8accd3d3fd6-1578717731",
    "pow_diff_reference": {
      "blake2bd_bits": "1c1fffff",
      "blake2bd_target": "000000001fffff00000000000000000000000000000000000000000000000000",
      "cuckaroo_min_diff": 12718848,
      "cuckatoo_min_diff": 1856
    },
    "maxtime": 1578724931,
    "mintime": 1578717707,
    "mutable": [
      "time",
      "transactions/add",
      "prevblock",
      "coinbase/append"
    ],
    "noncerange": "00000000ffffffff",
    "capabilities": [
      "proposal"
    ]
  }

```

***

### SubmitBlock 
Attempts to submit new block to network. 

#### Parameters
1. `hexBlock: (string)` hex-encoded block data to submit. Refer to https://github.com/qitmeer/qitmeer-miner to investigate how to construct a block

#### Returns
##### `(string)` submit message

#### Example

##### Request
```bash
curl --data '{"method":"submitBlock","params":["0b0000009b324c447c093502bd2928251c7a76bd66fac662f4535130c512a52ff27c9ac291db77e47c8b7fb1199192e813698abd42ceae44c6f6cd7bb3bfee442b105079000000000000000000000000000000000000000000000000000000000000000000000000d998195eba6acfb00118539c0100c3b203006b871000627a170066122400e7a933007cfb3b00ed393d00b9a63e00fcad4d0083c954004b6c5c007ac77300db1b7a0025f27c00540e7d0015018300a40084000bc28900d0f38f002b8592007e759300195a9900a2529b002356a1004b86a2008affb300f5a3ba001b05bb00dc52bf006528c1008fa1c20058a4c8000ca3cc002ff1cc00e4e8d10052cfd400e063dd00612fdf007a7ee5001d93ea00c093fc00019b324c447c093502bd2928251c7a76bd66fac662f4535130c512a52ff27c9ac2010100000001b3e2498b9592e6871e1a02a23a32988495b0c3da449f1cb3f1389013d044713bffffffffffffffff01007841cb020000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac000000000000000001455a08ec92282d01baa3be153131333933333038383330373933383831353235322435633739303233612d653130642d343631622d613438662d356563343961316233353330"],"jsonrpc":"2.0","id":1}' -s -k -u "test:test"  -H 'Content-Type: application/json' http://127.0.0.1:38131 |jq .
```

##### Response
```js
"Block submitted accepted  hash fcd2fe6a284e46d4fb7893e84bbcc58ca96e020be1e57b5c1b2c45929cca8dee, height 10, order 10 amount 12000000000"
```