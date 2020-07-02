---
title: getBlockhashByRange
weight: 1
---

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

