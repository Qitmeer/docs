---
title: getUTXO
weight: 1
---

## getUTXO  
Returns information about an unspent transaction output

### Parameters
1. `txid           (string, required)`                The hash of the transaction
2. `vout           (numeric, required)`               The index of the output
3. `includemempool (boolean, optional, default=true)` Include the mempool when true

### Returns
```json
{
 "bestblock": "value",        (string)          The block hash that contains the transaction output
 "confirmations": n,          (numeric)         The number of confirmations
 "amount": n.nnn,             (numeric)         The transaction amount
 "scriptPubKey": {            (object)          The public key script used to pay coins as a JSON object
  "asm": "value",             (string)          Disassembly of the script
  "hex": "value",             (string)          Hex-encoded bytes of the script
  "reqSigs": n,               (numeric)         The number of required signatures
  "type": "value",            (string)          The type of the script (e.g. 'pubkeyhash')
  "addresses": ["value",...], (array of string) The qitmeer addresses associated with this script
 },
 "coinbase": true|false,      (boolean)         Whether or not the transaction is a coinbase
}
```

### Example
#### Request

```sh
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getRawTransaction","params":["c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32",true],"id":1}' https://127.0.0.1:18131

```
#### Response
```json
{
  "hex": "0100000001dc7d54db024a1ef06e38b85ab01af2d60043e3d36b5411691224c05dcf36f63c01000000ffffffff02659ca300000000001976a91406e2097d585337cdd10aefa09994b511127af0bb88acf0e8cd6f230200001976a914fe27c90d4ed4de3269c0bb9ae1d7639865e3bf2888ac00000000000000008015fc5e016b48304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a012103cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8",
  "txid": "c259a4dfb7eaaae92ab246f14762541581671135cd6030ac29d8c34cf77e9f32",
  "txhash": "9b603ba3b17fd8491749ac366a5064d8b7b70be02568e405406a9acd70e971a8",
  "size": 235,
  "version": 1,
  "locktime": 0,
  "timestamp": "2020-07-01T12:48:00+08:00",
  "expire": 0,
  "vin": [
    {
      "txid": "3cf636cf5dc024126911546bd3e34300d6f21ab05ab8386ef01e4a02db547ddc",
      "vout": 1,
      "sequence": 4294967295,
      "scriptSig": {
        "asm": "304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a01 03cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8",
        "hex": "48304502210090910aa0190a6571319b0b638bfbb593582575703abdd4f1a7f0da2812cda7d102205dae6fee28396bfeb8f1b814884d8d03ab0dd9f30b171d906c24914ba2f85b1a012103cd4fa2ea2688ac9e0a62584635244f572d22c13730d5576722d6571aabfddca8"
      }
    }
  ],
  "vout": [
    {
      "amount": 10722405,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 06e2097d585337cdd10aefa09994b511127af0bb OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a91406e2097d585337cdd10aefa09994b511127af0bb88ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "TmPaUYQuUtfCysrYVHc4AdhpVHxw7EskHTP"
        ]
      }
    },
    {
      "amount": 2351222876400,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 fe27c90d4ed4de3269c0bb9ae1d7639865e3bf28 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914fe27c90d4ed4de3269c0bb9ae1d7639865e3bf2888ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "Tmn7vzzSrvAPNLtwpD5YjiWwVUBD74Hjdww"
        ]
      }
    }
  ],
  "confirmations": 0
}

```

