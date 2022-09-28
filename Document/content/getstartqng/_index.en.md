---
title: Getting Started QNG
weight: 6
#pre: "<b>1. </b>"
# chapter: true
---

## Prerequisites
### Introduction

The Qitmeer network implementation with the plug-able VMs under the MeerDAG consensus.

## Run QNG

### Install
* Build from source
```bash
~ git clone https://github.com/Qitmeer/qng.git
~ make
```

or
* Install the latest qng available here:
  https://github.com/Qitmeer/qng/releases

or
* Build with Docker:
```bash
~ docker build -t qng .
```

### Run
* We take the construction of network nodes as an example:
```
~ cd ./build/bin
~ ./qng 
or
~ docker run --rm -it --name qng qng:latest ./build/bin/qng --acceptnonstd --modules=qitmeer --modules=p2p
``` 

### MeerEVM
* If you want to use our MeerEVM function, the required interface information can be queried in this RPC:
```
~ cd ./script
~ ./cli.sh vmsinfo
``` 
* If you don't need the default configuration, we provide an environment configuration parameter to meet your custom configuration for MeerEVM:
```
~ ./qng --evmenv="--http"
or
~ ./qng --evmenv="--http --http.port=8545 --ws --ws.port=8546"
or
~ ./qng --evmenv="--syncmode=full --gcmode=archive --http --http.addr=0.0.0.0 --http.port=8545 --ws --ws.port=8546 --ws.addr=0.0.0.0 --http.api=eth,web3,net,debug,txpool --ws.api=eth,web3,net,debug,txpool"
``` 
