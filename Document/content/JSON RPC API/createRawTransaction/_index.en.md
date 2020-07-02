---
title: createRawTransaction
weight: 3
---

### createRawTransaction
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


