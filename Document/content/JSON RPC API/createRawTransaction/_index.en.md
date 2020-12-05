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

 curl -sku "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"createRawTransaction","params":[   [{"Txid":"cfd933e4590a3cfbcf94e9220c77834fe8a869414c51e3bd0ce5af23592e80f9", "Vout":1}], {"Tme9dVJ4GeWRninBygrA6oDwCAGYbBvNxY7":90000000}],"id":1}' http://127.0.0.1:18131 | jq

```

##### Response
```js
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0100000001f9802e5923afe50cbde3514c4169a8e84f83770c22e994cffb3c0a59e433d9cf01000000ffffffff01804a5d05000000001976a914a6b8fe2348fad076b7fd1b34b7e5b35db96dc2a088ac00000000000000001141cb5f0100"
}

```


