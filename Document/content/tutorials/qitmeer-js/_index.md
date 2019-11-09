---
title: Qitmeer JS
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

# qitmeer-js 说明

1. 安装

```bash
npm i qitmeer-js --save
```

2. 导入

```js
const qitmeer = require('qitmeer-js')
```

2. 如何生成地址（随机数（助记词），私钥，公钥，地址）

```js
const qitmeer = require('qitmeer-js')

// 生成 随机数 npm i randombytes --save
const randomBytes = require('randombytes')
const secretKey = randomBytes(32)
// <Buffer 3d 2b 7c e0 8b 12 be ed f3 12 88 2b bd fa 0d 58 22 ad 4c f2 b8 9a ad 84 24 2b 80 15 93 3d e6 16>

secretKey.toString('hex')
// 3d2b7ce08b12beedf312882bbdfa0d5822ad4cf2b89aad84242b8015933de616


// 生成公钥
const keyPair = qitmeer.ec.fromPrivateKey( secretKey )
const publicKey = keyPair.publicKey
// <Buffer 02 6c 21 c3 28 5b 26 be ed 8b 5c 8b f1 36 c4 9d fb bb 28 cf 6e b6 de a7 79 81 47 b8 98 93 8c 8f dc>

publicKey.toString('hex')
// 026c21c3285b26beed8b5c8bf136c49dfbbb28cf6eb6dea7798147b898938c8fdc

// 生成地址
// 设置网络 mainnet【主网】, testnet【测试】, privnet【私有】
const network = qitmeer.networks.mainnet

const hash160 = qitmeer.hash.hash160(keyPair.publicKey)

const p2pkhAddress = qitmeer.address.toBase58Check(hash160, network.pubKeyHashAddrId)
// NmcMJfyzyKbuD9Jy7ZPL6AGCUz5nfPaXBbx
```


3. 如何签名一个交易（单个utxo，多个utxo）

```js
const UTXO = {
    "vin": [
        {
          "txid": "d46a58fced5a05b1dc1f4450e1bdf09696291348a7eccec069ed59343ec35b4d",
          "vout": 2,
          "sequence": 4294967295,
          "amountin": 45000000000,
          "blockheight": 1,
          "txindex": 0,
          "scriptSig": {
            "asm": "3044022005422cf4f7a082fe931509b44aee54c3d3c80b1f0d43ed1483ffeb7248857fe402202b9c050ed0fbb9883c8ff98d8a48c33483b32ad776d6746365f9b8851e6dcda501 02abb13cd5260d3e9f8bc3db8687147ace7b6e5b63b061afe37d09a8e4550cd174",
            "hex": "473044022005422cf4f7a082fe931509b44aee54c3d3c80b1f0d43ed1483ffeb7248857fe402202b9c050ed0fbb9883c8ff98d8a48c33483b32ad776d6746365f9b8851e6dcda5012102abb13cd5260d3e9f8bc3db8687147ace7b6e5b63b061afe37d09a8e4550cd174"
          }
        },
        {
          "txid": "46a6d3d9e1ef552dc9b0eba147ea97e481654a2bccf59fd764652971cb4d9fdd",
          "vout": 2,
          "sequence": 4294967295,
          "amountin": 45000000000,
          "blockheight": 2,
          "txindex": 0,
          "scriptSig": {
            "asm": "3045022100be434e16f4c83947b1a19fefbf319b7170b280c9a0d89c0786624a83bda337910220395753153ab55b21d7041705c75f42778d7846a41ca5cbb5b033f875d20a9f1501 02abb13cd5260d3e9f8bc3db8687147ace7b6e5b63b061afe37d09a8e4550cd174",
            "hex": "483045022100be434e16f4c83947b1a19fefbf319b7170b280c9a0d89c0786624a83bda337910220395753153ab55b21d7041705c75f42778d7846a41ca5cbb5b033f875d20a9f15012102abb13cd5260d3e9f8bc3db8687147ace7b6e5b63b061afe37d09a8e4550cd174"
          }
        }
      ],
    "vout": [
        {
          "amount": 89000000000,
          "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 69570a6c1fcb68db1b1c50b34960e714d42c7b9c OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a91469570a6c1fcb68db1b1c50b34960e714d42c7b9c88ac",
            "reqSigs": 1,
            "type": "pubkeyhash"
          }
        },
        {
          "amount": 990000000,
          "scriptPubKey": {
            "asm": "OP_DUP OP_HASH160 c693f8fbfe6836f1fb55579b427cfc4fd2014953 OP_EQUALVERIFY OP_CHECKSIG",
            "hex": "76a914c693f8fbfe6836f1fb55579b427cfc4fd201495388ac",
            "reqSigs": 1,
            "type": "pubkeyhash"
          }
        }
      ],
    "blockheight": 101,
    "confirmations": 1
}

const qitmeer = require('qitmeer-js')

// 设置网络 mainnet【主网】, testnet【测试】, privnet【私有】
const network = qitmeer.networks.mainnet

// 私钥
const secretKey = '3d2b7ce08b12beedf312882bbdfa0d5822ad4cf2b89aad84242b8015933de616'
const keyPair = qitmeer.ec.fromPrivateKey( secretKey )

// 构造交易
const txb = qitmeer.txsign.newSigner( network );

// 设置打包时间，一般不用设置
txb.setLockTime(1573046495)
UTXO.vin.map( {txid,txindex} => {
    // txid: 交易id ， txindex: 交易序号
    txb.addInput( txid,txindex);
})

// 1 QIT = 100000000 MEER
// 输入的 amount 总数减去输出总数等于手续费
txb.addOutput( 'NmcMJfyzyKbuD9Jy7ZPL6AGCUz5nfPaXBbx', 89900000000);
txb.addOutput( 'NmbiHCrN796d74wXccqzqYHBLawn7NHyRX6', 80000000);
utxo.map( (v,i) => {
    txb.sign(i, keyPair);
})

// 获取 交易体
const newTransaction = txb.build().toBuffer().toString('hex');

// 计算收费
const BigNumber = require('bignumber.js')

function getFee( tx, speed = 'fast' ) {
    const size = tx.__tx.byteLength()
    const s = {
        fast: 2,
        normal: 1,
        slow: 0.6
    }
    return BigNumber( size ).div(2).multipliedBy(5000).multipliedBy(s[speed])
}
        
```
