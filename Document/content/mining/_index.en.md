---
title: "Mining"
date: 2019-07-11T21:56:43+08:00
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

## Qitmeer-Miner user guide
***qitmeer-miner*** is the miner tool for ***qitmeer*** network , it can get reward by generate block.

## Prerequisites

Update Go to version at least 1.12 (required >= **1.12**)

Check your golang version

```shell
$ go version
go version go1.12 darwin/amd64
```

## Compile

```bash
$ git clone git@github.com:HalalChain/hlc-miner.git
```

* Ubuntu ENV
```bash
$ sudo apt-get install beignet-dev nvidia-cuda-dev nvidia-cuda-toolkit
$ go build 
```
        
* Centos ENV
```bash
$ sudo yum install opencl-headers
$ sudo yum install ocl-icd
$ sudo ln -s /usr/lib64/libOpenCL.so.1 /usr/lib/libOpenCL.so
$ go build
```
        

* MAC

```bash
go build
```

* Windows ENV
```bash
$ go build 
```
any questions can see [issues](https://github.com/HalalChain/hlc-miner/issues?q=is%3Aissue+is%3Aclosed)
        
    
## Run
```bash
$ cp halalchainminer.conf.example halalchainminer.conf
```
- 1.run with the config file `halalchainminer.conf`
- 2.run with command
```bash
$ ./hlc-miner -h
Usage:
  hlc-miner [OPTIONS]

Debug Command:
  -l, --listdevices   List number of devices.
  -T, --testpow=      test pow blake2bd|cuckaroo|cuckatoo

The Config File Options:
  -C, --configfile=   Path to configuration file (/Users/fanxu/www/go/src/hlc-miner/halalchainminer.conf)
      --minerlog=     Write miner log file (/Users/fanxu/www/go/src/hlc-miner/miner.log)

The Necessary Config Options:
  -P, --pow=          blake2bd|cuckaroo|cuckatoo (cuckaroo)
  -S, --symbol=       Symbol (HLC)

The Solo Config Option:
  -M, --mineraddress= Miner Address (RmN4SADy42FKmN8ARKieX9iHh9icptdgYNn)
  -s, --rpcserver=    RPC server to connect to (127.0.0.1:1234)
  -u, --rpcuser=      RPC username (test)
  -p, --rpcpass=      RPC password
      --randstr=      Rand String,Your Unique Marking. (Come from halalchain!)
      --notls         Do not verify tls certificates (true)
      --rpccert=      RPC server certificate chain for validation (CA.cert)

The pool Config Option:
  -o, --pool=         Pool to connect to (e.g.stratum+tcp://pool:port)
  -m, --pooluser=     Pool username
  -n, --poolpass=     Pool password

The Optional Config Option:
      --trimmerTimes= the cuckaroo trimmer times (40)
      --proxy=        Connect via SOCKS5 proxy (eg. 127.0.0.1:9050)
      --proxyuser=    Username for proxy server
      --proxypass=    Password for proxy server
      --intensity=    Intensities (the work size is 2^intensity) per device. Single global value or a comma
                      separated list. (24)
      --worksize=     The explicitly declared sizes of the work to do per device (overrides intensity). Single
                      global value or a comma separated list. (256)

Help Options:
  -h, --help          Show this help message
```
