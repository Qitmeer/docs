---
title: getBlock
weight: 1
---

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


