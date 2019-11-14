# <font color=Chocolate size=6>Mining Tutorial</font>

## Table of Contents

* [Prequisite](#prequisite)
    * [Common](#common)
    * [Linux](#linux)
        * [Ubuntu](#ubuntu)
        * [Centos](#centos)
    * [macOS](#macos)
    * [Windows](#windows)
* [Build](#build)
    * [Windows-additional step](#windows-additional-step)
    * [Linux-additional step](#Linux-additional step)
* [Usage](#build)
    * [Run with config file](#run-with-config-file)
    * [Command line usage](#command-line-usage)
* [FAQ](#build)
    * [How to create Qitmeer adderss](#how-to-create-qitmeer-adderss)
    * [Which POW algorithm I should choose to mine ?](#which-pow-algorithm-i-should-choose-to-mine-?)
    * [Where I can find more documentation ?](#where-i-can-find-more-documentation-?)
    
### Prequisite

### Common

1. [Git](https://git-scm.com/downloads) 
2. [Go](https://golang.org/dl/) version >= 1.12

### Linux


#### Ubuntu

```bash
$ sudo apt-get install beignet-dev nvidia-cuda-dev nvidia-cuda-toolkit
```
        
#### Centos 

```bash
$ sudo yum install opencl-headers
$ sudo yum install ocl-icd
$ sudo ln -s /usr/lib64/libOpenCL.so.1 /usr/lib/libOpenCL.so
```  
### MacOS

### Windows

Install [**Build Tools for Visual Studio**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
    
## Build 

### 1. Get Source code

```bash
$ git clone git@github.com:Qitmeer/qitmeer-miner.git
```

### 2. Build the curkoo library 

```bash
$ cd qitmeer-miner 
$ sh installLibrary.sh
```

### 3. Build qitmeer-miner  

```bash
//# mac
$ go build
//# linux apt install musl-tools g++ -y
$ CGO_ENABLED=1 CC=musl-gcc CXX=g++ GOOS=linux
//# windows 
$ CGO_ENABLED=1 GOOS=windows GOARCH=amd64 go build -ldflags '-extldflags "-static"' -o win-miner.exe main.go
```

### 4. Verify Build OK

```bash
$ ./qitmeer-miner --version
```

### Windows-additional step

Before step 3, do following 
```bash
$ copy lib/cuckoo/target/release/x86_64-pc-windows-gnu/cuckoo.lib to C:/mingw64/lib
$ copy lib/opencl/windows/libOpenCL.a to C:/mingw64/lib
```
### Linux-additional step

Before step 3, do following 
```bash
$ sudo copy lib/cuckoo/target/x86_64-unknown-linux-musl/release/libcuckoo.a /usr/lib/x86_64-linux-musl
$ sudo copy lib/opencl/linux/libOpenCL.a /usr/lib/x86_64-linux-musl
```
## Usage

### Run with config file 
1. go to your 
2. create a new config file by copying from the example config file. 
```bash
$ cp example.solo.conf qitmeer-miner.conf
```
3. edit the config file which your create, you might need to change the `mineraddress`. 
you need to create a Qitmeer address if you don't have it. Please see [FAQ](#FAQ)  
4. run miner with the config file

```bash
$ ./qitmeer-miner -C qitmeer-miner.conf
```

### Command line usage

The qitmeer-miner is a command line program. This means you can also launch it by provided valid command line options. For a full list of available command optinos, please run:

```bash
$ ./qitmeer-miner --help 
Debug Command:
  -l, --listdevices    List number of devices.

The Config File Options:
  -C, --configfile=    Path to configuration file
      --minerlog=      Write miner log file

The Necessary Config Options:
  -P, --pow=           blake2bd|cuckaroo|cuckatoo (blake2bd)
  -S, --symbol=        Symbol (PMEER)
  -N, --network=       network privnet|testnet|mainnet (mainnet)

The Solo Config Option:
  -M, --mineraddress=  Miner Address
  -s, --rpcserver=     RPC server to connect to (127.0.0.1)
  -u, --rpcuser=       RPC username
  -p, --rpcpass=       RPC password
      --randstr=       Rand String,Your Unique Marking. (Come from Qitmeer!)
      --notls          Do not verify tls certificates (true)
      --rpccert=       RPC server certificate chain for validation

The pool Config Option:
  -o, --pool=          Pool to connect to (e.g.stratum+tcp://pool:port)
  -m, --pooluser=      Pool username
  -n, --poolpass=      Pool password

The Optional Config Option:
      --cpuminer       CPUMiner (false)
      --proxy=         Connect via SOCKS5 proxy (eg. 127.0.0.1:9050)
      --proxyuser=     Username for proxy server
      --proxypass=     Password for proxy server
      --trimmerTimes=  the cuckaroo trimmer times (40)
      --intensity=     Intensities (the work size is 2^intensity) per device. Single global value or a comma separated list. (24)
      --worksize=      The explicitly declared sizes of the work to do per device (overrides intensity). Single global value or a comma separated list. (256)
      --timeout=       rpc timeout. (60)
      --use_devices=   all gpu devices,you can use ./qitmeer-miner -l to see. examples:0,1 use the #0 device and #1 device
      --max_tx_count=  max pack tx count (1000)
      --max_sig_count= max sign tx count (5000)
      --log_level=     info|debug|error|warn|trace (debug)
      --stats_server=  stats web server (127.0.0.1:1235)
      --edge_bits=     edge bits (24)
      --local_size=    local size (4096)
      --group_size=    work group size (256)

Help Options:
  -h, --help           Show this help message
 
```
Please see [Qitmeer-Miner User References](https://qitmeer.github.io/docs/en/reference/qitmeer-miner/) for more details

## FAQ

### How to create Qitmeer adderss
There are several ways to create a Qitmeer address. you can use [qx][Qx] command , [qitmeer-wallet][Qitmeer-wallet], etc.
The most easy way to download the [kafh wallet][kafh.io], which provide a more user friendly GUI to create your address/wallet step by step. 

### Which POW algorithm I should choose to mine ?
Qitmeer test network support mixing minning, which means your can choice from `Cuckaroo`, `Cuckatoo` and `Blake2bd` anyone you like. 
But the start difficulty targets are quite different. For the most case you might use `Cuckaroo` as a safe choice at the beginning. 

### Where I can find more documentation ? 
Please find more documentation from the [Qitmeer doc site at https://qitmeer.github.io](https://qitmeer.github.io/docs/en/reference/qitmeer-miner/)

[Releases]: https://github.com/Qitmeer/qitmeer-miner/releases
[Latest]: https://github.com/Qitmeer/qitmeer-miner/releases/latest
[Qx]: https://qitmeer.github.io/docs/en/reference/qxtools/
[Qitmeer-wallet]: https://github.com/Qitmeer/qitmeer-wallet
[Kafh.io]:https://www.kahf.io/
