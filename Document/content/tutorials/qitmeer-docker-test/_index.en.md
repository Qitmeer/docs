---
title: Qitmeer Testing Guide
weight: 31
#pre: "<b>1. </b>"
# chapter: true
---

## Testing Qitmeer Using Docker Image

Here is the step by step guide to show to how setup the testing Qitmeer network by using the Qitmeer docker image.

### Prerequisites
Before we go with the experiment, we need to ensure the system and qitmeer suite are ready. Since the following experiment pertains two nodes, so we need to perform theses steps on each node.

#### System

##### Hardware and OS
* Memory: >= 2G
* Storage: >= 10G
* OS: >= Ubuntu 16.04
* Network: >= 2M b/s bandwidth, with PUBLIC IP

**Note:** currently, Qitmeer's seeder is not open-sourced and the nodes need to connect with each other directly, thus PUBLIC IP is an obligation. Late on, once seeder is ready, this requirement will be removed.

##### Golang
Most of Qitmeer Suite are golang projects and using go modules. 

```shell
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```

##### Docker
Install docker on ubuntu:
```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
```

If you are already a root user, you can ignore next step
```
# Add docker user group and add the logged-in user to the docker user group.

sudo groupadd docker
sudo gpasswd -a $USER docker
newgrp docker
docker ps
```
 You can use `docker -v` to test whether the installation is successful or not.
Other systems platforms are similar.You can go [docker](https://www.docker.com/get-started)


#### Qitmeer Suite
Qitmeer Suite consists of qitmeer Docker, qx, cli

##### Qitmeer Docker image

* Installation
```shell
docker pull halalchain/qitmeer
```

* Usage
```shell
docker run -it -p 18130:18130 -p 18131:18131 halalchain/qitmeer --miningaddr=[Your mining address] --addpeer=[peer1 IP:PORT] [--addpeer=[peer2 IP:PORT]] --httpmodules=miner --httpmodules=nox 
```
| Field | Explain |
| --- | --- |
| -p 18130:18130 | P2P port mapping, used for nodes to communicate with each other|
| -p 18131:18131 | PRC port mapping, used for clients to call  services  remotely|
| miningaddr | Miner account address |
| debuglevel | Logging level {trace, debug, info, warn, error, critical} |
| addpeer | Add a peer to connect with at startup |
| generate | Generate (mine) coins using the CPU |
| connect | Connect only to the specified peers at startup |
| httpmodules | It is a list of API modules to expose via the HTTP RPC interface. (Current valid values:nox,miner)|


#####  Qitmeer-cli
qitmeer cli is a RPC tool for the qitmeer network

* Installation
```shell
git clone https://github.com/HalalChain/qitmeer-cli ~/github.com/HalalChain/qitmeer-cli
cd ~/github.com/HalalChain/qitmeer-cli
go build
./cli
```

* Usage
```plain
qitmeer cli is a RPC tool for the qitmeer network

Usage:
  qitmeer-cli [command]

Available Commands:
  createrawtransaction createRawTransaction
  decoderawtransaction decodeRawTransaction
  generate             generate {n}, cpu mine n blocks
  getUtxo              getUtxo tx_hash vout include_mempool,
  getblock             get block by number or hash
  getblockcount        get block count
  getblockhash         get block hash by number
  getblocktemplate     getblocktemplate
  getmempool           get mempool
  getrawtransaction    getrawtransaction
  help                 Help about any command
  sendrawtransaction   sendRawTransaction
  txSign               txSign private_key raw_tx

Flags:
      --cert string        RPC server certificate file path
  -c, --config string      config file path (default "config.toml")
      --debug              debug print log
  -h, --help               help for qitmeer-cli
      --notls              Do not verify tls certificates (not recommended!) (default true)
  -P, --password string    RPC password
      --proxy string       Connect via SOCKS5 proxy (eg. 127.0.0.1:9050)
      --proxypass string   Password for proxy server
      --proxyuser string   Username for proxy server
  -s, --server string      RPC server to connect to (default "127.0.0.1:18131")
      --simnet             Connect to the simulation test network
      --skipverify         Do not verify tls certificates (not recommended!) (default true)
      --testnet            Connect to testnet
      --timeout string     rpc timeout,s:second h:hour m:minute (default "30s")
  -u, --user string        RPC username

Use "qitmeer-cli [command] --help" for more information about a command.
```

##### qx tool
qx is a command-line tool that provides a variety of commands for key management and transaction construction. 

* Installation
```shell
git clone https://github.com/HalalChain/qx ~/github.com/HalalChain/qx
cd ~/github.com/HalalChain/qx
go build
alias qx=~/github.com/HalalChain/qx/qx
qx
```

* Usage
```plain
Usage: qx [--version] [--help] <command> [<args>]

encode and decode :
    base58-encode         encode a base16 string to a base58 string
    base58-decode         decode a base58 string to a base16 string
    base58check-encode    encode a base58check string
    base58check-decode    decode a base58check string
    base64-encode         encode a base16 string to a base64 string
    base64-encode         encode a base64 string to a base16 string
    rlp-encode            encode a string to a rlp encoded base16 string
    rlp-decode            decode a rlp base16 string to a human-readble representation

hash :
    blake2b256            calculate Blake2b 256 hash of a base16 data.
    blake2b512            calculate Blake2b 512 hash of a base16 data.
    sha256                calculate SHA256 hash of a base16 data.
    sha3-256              calculate SHA3 256 hash of a base16 data.
    keccak-256            calculate legacy keccak 256 hash of a bash16 data.
    blake256              calculate blake256 hash of a base16 data.
    ripemd160             calculate ripemd160 hash of a base16 data.
    bitcion160            calculate ripemd160(sha256(data))
    hash160               calculate ripemd160(blake2b256(data))

entropy (seed) & mnemoic & hd & ec
    entropy               generate a cryptographically secure pseudorandom entropy (seed)
    hd-new                create a new HD(BIP32) private key from an entropy (seed)
    hd-to-ec              convert the HD (BIP32) format private/public key to a EC private/public key
    hd-to-public          derive the HD (BIP32) public key from a HD private key
    hd-decode             decode a HD (BIP32) private/public key serialization format
    hd-derive             Derive a child HD (BIP32) key from another HD public or private key.
    mnemonic-new          create a mnemonic world-list (BIP39) from an entropy
    mnemonic-to-entropy   return back to the entropy (the random seed) from a mnemonic world list (BIP39)
    mnemonic-to-seed      convert a mnemonic world-list (BIP39) to its 512 bits seed
    ec-new                create a new EC private key from an entropy (seed).
    ec-to-public          derive the EC public key from an EC private key (the compressed format by default )
    ec-to-wif             convert an EC private key to a WIF, associates with the compressed public key by default.
    wif-to-ec             convert a WIF private key to an EC private key.
    wif-to-public         derive the EC public key from a WIF private key.

addr & tx & sign
    ec-to-addr            convert an EC public key to a paymant address. default is nox address
    tx-encode             encode a unsigned transaction.
    tx-decode             decode a transaction in base16 to json format.
    tx-sign               sign a transactions using a private key.
    msg-sign              create a message signature
    msg-verify            validate a message signature
    signature-decode      decode a ECDSA signature

```


### Step-by-Step Guide
This experiment demostrates a typical transfer process. The network consists of two nodes, a miner and a recipient. The miner mines a block and receives mining rewards; then he will transfer 2 Qitmeer Coins to the recipient.

#### Recipient Node
This node is playing the role of transfer recipient, it starts with a normal full node setting, that's to say that it has no mining functionality.

##### Launch
```shell
docker run -it -p 18130:18130  halalchain/qitmeer 
```

##### Generate Recipient Address
```shell
 qx ec-new $(qx entropy) > ~/recipient_key.txt
 qx ec-to-addr $(qx ec-to-public $(cat ~/recipient_key.txt)) > ~/recipient_address.txt 
```

##### Save IP address
```shell
 curl ipinfo.io/ip > ~/recipient_ip.txt 
```

 Share recpient's address and IP
Share recipient_address.txt and recipient_ip.txt with the miner.

#### Miner Node
This node is playing the role of miner and transfer originator, it starts with a full miner setting .

##### Generate Minning address
```shell
 qx ec-new $(qx entropy) > ~/miner_key.txt
 qx ec-to-addr $(qx ec-to-public $(cat ~/miner_key.txt)) > ~/miner_address.txt 
```

##### Launch Node
```shell
 alias qitmeer=docker run -it -p 18130:18130 -p 18131:18131 halalchain/qitmeer
 qitmeer --miningaddr=$(cat ~/miner_address.txt) --addpeer=$(cat ~/recipient_ip.txt):18130 --httpmodules=miner --httpmodules=nox  --testnet --rpcuser=test --rpcpass=test --generate
```
 Now observe the log of Node Recipient, if the connection is OK, a new log like following should display
```plain
2019-07-06|00:20:45.627 [INFO ] New valid peer                      module=blockchain peer="IP_OF_MINER:53962 (inbound)" user-agent=/noxd:0.0.1/nox:0.3.0/
Qitmeer's RPC is encrypted, to call RPC service, you should obtain the RPC certificate first; also, the working home of cli must be changed to where it is located.
```

```shell
 cd ~/github.com/HalalChain/qitmeer-cli/
 docker cp $(docker ps -q --filter ancestor=halalchain/qitmeer):/qitmeer/rpc.cert ~/
 alias cli="./qitmeer-cli --notls=false --password=test --skipverify=false --testnet=true --user=test --cert=$HOME/rpc.cert  --server=127.0.0.1:18131"
```

##### Generate Block

watch the log window until we find a new block is mining and the log would be like:
```plain
2019-07-06|04:23:36.760 [INFO ] Block submitted accepted            module="cpu miner" hash=BLOCK_HASH height=BLOCK_HEIGHT amount=2500000000
why [MINER_ADDRESS], 1
```
In this case, BLOCK_HASH is 00000012524082d9144908e28eddb9e8a971c1b220b5301afa3e4f1597413294 and BLOCK_HEIGHT is 1000

##### Get UTXO 
```
 cli getblock BLOCK_HASH |jq '.transactions[0].vout' 
```
```JSON
[
  {
    "amount": 250000000,
    "scriptPubKey": {
      "asm": "",
      "type": "nonstandard"
    }
  },
  {
    "amount": 0,
    "scriptPubKey": {
      "asm": "OP_RETURN e803000067e7a740bf8fdd3a",
      "hex": "6a0ce803000067e7a740bf8fdd3a",
      "type": "nulldata"
    }
  },
  {
    "amount": 2250000000,
    "scriptPubKey": {
      "asm": "OP_DUP OP_HASH160 f3f61ce15d8b686f2b29d268a901b9d8beef3d3a OP_EQUALVERIFY OP_CHECKSIG",
      "hex": "76a914f3f61ce15d8b686f2b29d268a901b9d8beef3d3a88ac",
      "reqSigs": 1,
      "type": "pubkeyhash",
      "addresses": [
        "TmmC2jmGKUbnhjjhBtRFfJ7m2tRPVvoaXnM"
      ]
    }
  }
]
```
From the result, we could get the index and the amount of the UTXO, in this case it is the third UTXO, so the index is **2**.; besides, we could know the miner reward is *22.5* Qitmeer Coin (2250000000).

##### Get coinbase transaction ID
```shell
 cli getblock BLOCK_HASH |jq '.transactions[0].txid'| tr -d '"' > ~/tx_id.txt
```
##### Transaction maturity
A coinbase transaction can be spent only with at least 16 blocks confirmation. From the the log, we know that the transacation is created at block height 1000, so we wait until the block height is greater than 1016.

```shell
 cli getblockcount 
```
```plain
1017
```
Note: this operation may be slow because this is CPU mining, anyway, Qitmeer GPU Miner will be ready soon and will make this process really fast.

Currently the miner node  has enabled auto mining by adding \--generate parameter. If we remove it, the node will retuen to the default manual mining mode. So we can control how many blocks to be mined accurately, for example:

```shell
# this command may be slow, please increate timeout if got timeout error
$ cli --timeout=9m generate 16
```


##### Build Transaction
Qitmeer doesn't accept zero fee transaction to prevent sybli-attack, so we send 2 coins to the reciepient and 2 coins back to the miner as change, leaving the 0.5 difference as the miner fee.
```shell
# Usage: qitmeer-cli createrawtransaction {inTxid:vout}... {toAddr:amount}... [flags]

 cli createrawtransaction $(cat ~/tx_id.txt):2 $(cat ~/recipient_address.txt):2 $(cat ~/miner_address.txt):20 | tr -d '"'> ~/tx.txt
```

##### Sign Transaction
```shell
# Usage: qitmeer-cli txSign {private_key} {raw_tx} [flags] 

 cli txSign $(cat ~/miner_key.txt) $(cat ~/tx.txt) | tr -d '"' > ~/tx.txt
```
##### Send Transcation
```shell
# Usage: qitmeer-cli sendrawtransaction {raw_tx} {allow_high_fee bool,defalut false} [flags]
 cli sendRawTransaction $(cat ~/tx.txt) true 
"12844dbc6b829ee021a9a9772c97efbb4afd410698775363be95786c39585bfc"
```
##### Verify Transcation
Wait for the coming block generated, then check if this transaction is packed inside. It is a unspent transaction, so we should find its UTXO.

``` shell
  cli getUtxo 12844dbc6b829ee021a9a9772c97efbb4afd410698775363be95786c39585bfc 0 |jq
```
```JSON
 {
  "bestblock": "0000000f9cfb63585fcce7df4e10ead67f27ae330d61643d640916fff5e3fe3b",
  "confirmations": 9,
  "amount": 20,
  "scriptPubKey": {
    "asm": "OP_DUP OP_HASH160 f3f61ce15d8b686f2b29d268a901b9d8beef3d3a OP_EQUALVERIFY OP_CHECKSIG",
    "hex": "76a914f3f61ce15d8b686f2b29d268a901b9d8beef3d3a88ac",
    "reqSigs": 1,
    "type": "pubkeyhash",
    "addresses": [
      "TmmC2jmGKUbnhjjhBtRFfJ7m2tRPVvoaXnM"
    ]
  },
  "version": 1,
  "coinbase": false
}
```

The UXTO is found, thus this transfer is done succesfully.


