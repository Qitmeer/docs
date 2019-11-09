---
title: Getting Started
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

## Prerequisites

### Development Environment
Follow [Development Environment](../tutorials/development-environment)

## Run Qitmeer
Open a new terminal window

### Install
* Docker  
Follow [Qitmeer Installation](../tutorials/qitmeer-installation) to install docker

```bash
alias qitmeer="docker run -it -p 18130:18130 -p 18131:18131 qitmeer/qitmeerd"  
```

* Build from Source
```bash
export QITMEER_URI=github.com/Qitmeer/qitmeer

git clone https://${QITMEER_URI} ~/${QITMEER_URI} 
cd ~/${QITMEER_URI} 
go build

alias qitmeer="~/${QITMEER_URI}/qitmeer"
```

### Run
```shell
 qitmeer --notls 
```

## Run Wallet
Open a new terminal window

### Install
```bash
export WALLET_URI=github.com/Qitmeer/qitmeer-wallet
git clone https://${WALLET_URI} ~/${WALLET_URI} --depth=1
cd ~/${WALLET_URI}
go build

alias qc="~/${WALLET_URI}/qitmeer-wallet --qserver=127.0.0.1:18131 --qpass=test --quser=test qc"
alias qx="~/${WALLET_URI}/qitmeer-wallet qx"
```

### create wallet
```shell
$ wallet qc create
Enter the private passphrase for your new wallet: [WALLET_PASSWORD]
Confirm passphrase: [WALLET_PASSWORD]
Do you want to add an additional layer of encryption for public data? (n/no/y/yes) [no]:
pubPass: public
Do you have an existing wallet seed you want to use? (n/no/y/yes) [no]:
Your wallet generation seed is:
[GENERATION_SEED]
IMPORTANT: Keep the seed in a safe place as you
will NOT be able to restore your wallet without it.
Please keep in mind that anyone who has access
to the seed can also restore your wallet thereby
giving them access to all your funds, so it is
imperative that you keep it in a secure location.
Once you have stored the seed in a safe and secure location, enter "OK" to continue: OK
Creating the wallet...
pri:[PRIVATE_KEY]
The wallet has been created successfully.
createWallet succ
```

### get address
```bash
export PRIVATE_KEY=[PRIVATE_KEY]
export WALLET_PASSWORD=[WALLET_PASSWORD]
qx pritoaddr $PRIVATE_KEY testnet
```
This will return the corresponding address, assume it is [MINER_ADDRESS]


###  update db 
This process will last a little bit long time, you may  process the following steps
```bash
qc updateblock
```

### Run Miner
Open a new terminal window

#### Install  
Follow [Qitmeer Miner](../tutorials/qitmeer-miner) to install dependencies of Miner

```bash
# replace MINER_URI with your miner directory
export MINER_URI=github.com/qitmeer/qitmeer-miner
git clone https://${MINER_URI} ~/${MINER_URI} --depth=1
alias miner="~/${MINER_URI}/qitmeer-miner"
```

#### Run

```bash
# replace MINER_ADDRESS with your miner address
export MINER_ADDRESS=[MINER_ADDRESS]
miner --mineraddress=${MINER_ADDRESS} --network=testnet --rpcuser=test --rpcpass=test --rpcserver=127.0.0.1:18131
```

## Send Transaction
Switch to wallet terminal

```bash
export RECIPIENT_MNEMONIC=$(qx generatemnemonic)
export RECIPIENT_ADDRESS=$(qx mnemonictoaddr "${RECIPIENT_MNEMONIC}" testnet)
qc sendtoaddress $RECIPIENT_ADDRESS 9 $WALLET_PASSWORD
```
