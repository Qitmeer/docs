---
title: wallet_sendToAddressByAccount
weight: 3
---

### wallet_sendToAddressByAccount 
发送交易

#### Parameters
1. `fromAccount: (string)` from account
2. `toAccount: (string)` to address
3. `amount: (string)` send amount coin
4. `comment: (string)` 
5. `commentTo: (string)` 

#### Returns


#### Example
##### Request
```json
{"id":1574828051839,"method":"wallet_sendToAddressByAccount","params":["default","TmZu8zU1i6xbZMpLQZLMAJsyWHanZXUZtiV",800,"",""]}
```
##### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1574828051839,
    "result": "b1ff3645c374992313e66d504fdf4fd3f2006f9414b97a7e1f6382328cc74fb1"
}
```
