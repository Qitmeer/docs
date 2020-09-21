---
title:  Instruction
weight: 1
---

## Build 
```shell
git clone https://github.com/qitmeer/qitmeer-wallet ~/github.com/qitmeer/qitmeer-wallet
 cd ~/github.com/qitmeer/qitmeer-wallet
make build
```

## Config
```
vi config.toml

# make sure ui=false

```

## Run

```sh
./qitmeer-wallet web
```
## Call API

### Command
```shell
# by cURL
curl -k -u "${USER}:${PASSWORD}" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"${METHOD}","params":[${PARAMS}],"id":1}' ${API_URL} | jq
```
### Parameters
1. `USER: (string)` rpcUser in the config
2. `PASSWORD: (string)` rpcPass in the config
3. `API_URL: (string)` listeners in the config
4. `METHOD: (string)` RPC call name
5. `PARAMS: (array)` RPC call parameters 

### Example
```sh
curl -k -u "user:password" -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"1.0","method":"wallet_createAccount","params":["account"],"id":1}' http://127.0.0.1:38130/api | jq
```