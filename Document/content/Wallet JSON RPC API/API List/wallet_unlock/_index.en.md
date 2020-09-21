---
title: wallet_unlock
weight: 3
---

## Unlock 
 unlocks the wallet's address manager and relocks it after timeout has
 expired.  If the wallet is already unlocked and the new passphrase is
 correct, the current timeout is replaced with the new one.  The wallet will
 be locked if the passphrase is incorrect or any other error occurs during the
 unlock.

### Parameters
1. `passphrase: (string)` wallet private password
2. `timeout: (numeric)` unlock duration, unit second

### Returns
#### Success
```sh
null
```

#### Error 
 `-32000` invalid passphrase for master private key



### Example
#### Request
```json
curl -k -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_unlock","params":["password", 999999999],"id":1}' http://127.0.0.1:8130/api

```
#### Response
```json
{"jsonrpc":"2.0","id":1,"result":null}
```

