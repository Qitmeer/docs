---
title: ui_createWallet 
weight: 3
---

## CreateWallet
create wallet by seed

### Parameters
1. `name: (string)` account name

### Returns
#### Success
`null`

#### Error 
`-32000` Creating an account requires the wallet to be unlocked. Enter the wallet passphrase with walletpassphrase to unlock

### Example
#### Request
```shell
curl -k -u "test:test" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_createAccount","params":["test_account"],"id":1}' http://127.0.0.1:8130/api
```

#### Response
```sh
{"jsonrpc":"2.0","id":1,"result":null}
```


