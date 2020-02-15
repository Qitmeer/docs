---
title: The `Transaction` Module
---

## JSON-RPC methods

- [CreateRawTransaction](#CreateRawTransaction)
- [DecodeRawTransaction](#DecodeRawTransaction)
- [GetRawTransactionByHash](#GetRawTransactionByHash)
- [GetUtxo](#GetUtxo)
- [SendRawTransaction](#SendRawTransaction)

## JSON-RPC API Reference

### CreateRawTransaction
Returns a new transaction spending the provided inputs and sending to the provided addresses.The transaction inputs are not signed in the created transaction.

#### Parameters
1. `inputs: (array of object)` transaction inputs.
    - `txid: (string)` The transaction id
    - `vout: (numeric)` The output number
2. `amounts: (object)`  addresses as keys and output amounts as values.
3. `lockTime: (numeric, optional, default=0)` Raw locktime. Non-0 value also locktime-activates inputs

#### Returns
##### `(string)` hex-encoded bytes of the serialized transaction

#### Example

##### Request
```bash
curl --data '{"method":"createRawTransaction","params":[[{"Txid":"ddf99e004ed24d641ddc942272ed174b1c2ae0fb27cc0ed7e858e0a451e27633", "Vout":0}], {"RmG6xQsV7gnS4JZmoq5FgmyEbmUQRenrTCo":10000000000}],"jsonrpc":"2.0","id":1}' -s -k -u "test:test"  -H 'Content-Type: application/json' http://127.0.0.1:1234 |jq .
```

##### Response
```js
"01000000013376e251a4e058e8d70ecc27fbe02a1c4b17ed722294dc1d644dd24e009ef9dd00000000ffffffff0100e40b54020000001976a9146bd68046854813036fa042958e7f5ca29606e8d088ac00000000000000000100"
```

*** 

### DecodeRawTransaction 
Returns a JSON object representing the provided serialized, hex-encoded transaction.

#### Parameters
1. `hexTx: (string)` serialized, hex-encoded transaction.

#### Returns
##### `(object)` 
- `txid: (string)` the transaction id.
- `txhash: (string)` the hash of the transaction.
- `locktime: (numeric)` the transaction lock time.
- `version: (numeric)` the block version.
- `vin: (array of objects, coinbase)` the transaction inputs .
    - `coinbase: (string)` the hex-encoded bytes of the signature script.
    - `sequence: (numeric)` the script sequence number.
- vin (array of objects, coinbase, non-coinbase)
(json object)
{"coinbase": "data", "sequence": n, ...}
- `vout: (array of objects)` the transaction outputs .

#### Example

##### Request
```bash
curl --data '{"method":"decodeRawTransaction","params":["01000000013376e251a4e058e8d70ecc27fbe02a1c4b17ed722294dc1d644dd24e009ef9dd00000000ffffffff0100e40b54020000001976a9146bd68046854813036fa042958e7f5ca29606e8d088ac00000000000000000100"],"jsonrpc":"2.0","id":1}' -s -k -u "test:test"  -H 'Content-Type: application/json' http://127.0.0.1:1234 |jq .
```

##### Response
```js
{
  "txid": "0d21c787536b02e3df82bd72c8dceb525049013cb249eee1d73090183c9a8965",
  "txhash": "b718e91241840992175195758628f3b6ec61019be0fa202d9b4b4652a6b96fd7",
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "ddf99e004ed24d641ddc942272ed174b1c2ae0fb27cc0ed7e858e0a451e27633",
      "vout": 0,
      "sequence": 4294967295,
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "amount": 10000000000,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 6bd68046854813036fa042958e7f5ca29606e8d0 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a9146bd68046854813036fa042958e7f5ca29606e8d088ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "RmG6xQsV7gnS4JZmoq5FgmyEbmUQRenrTCo"
        ]
      }
    }
  ]
}
```