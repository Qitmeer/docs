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
 curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getUtxo","params":          ["cfd933e4590a3cfbcf94e9220c77834fe8a869414c51e3bd0ce5af23592e80f9", 0],"id":1}' http://127.0.0.1:18131 | jq


```
#### Response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "bestblock": "6161b884e8ceaab14f23906a6ad3b86598dfaecbd805507ae4af302b85a95b10",
    "confirmations": 143935,
    "amount": 0.999326,
    "scriptPubKey": {
      "asm": "OP_DUP OP_HASH160 844d0a82845bccd469afc5cb78d8ffaa3142edea OP_EQUALVERIFY OP_CHECKSIG",
      "hex": "76a914844d0a82845bccd469afc5cb78d8ffaa3142edea88ac",
      "reqSigs": 1,
      "type": "pubkeyhash",
      "addresses": [
        "Tmb1dCAB8ixNC6d2VtdCYZuhXBVPbnRVi7y"
      ]
    },
    "version": 0,
    "coinbase": false
  }
}

```

