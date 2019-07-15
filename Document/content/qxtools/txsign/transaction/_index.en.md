---
title: transaction
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

### tx-encode

encode a unsigned transaction.

```bash
~ qx ec-to-addr --help

Usage: qx tx-encode [ec_public_key]
    -i value
        The set of transaction input points encoded as TXHASH:INDEX:SEQUENCE.
        TXHASH is a Base16 transaction hash. INDEX is the 32 bit input index in the context of the transaction. SEQUENCE is the optional 32 bit input sequence and defaults to the maximum value.
    -l value
        the transaction lock time
    -o value
        The set of transaction output data encoded as TARGET:NOX.
        TARGET is an address (pay-to-pubkey-hash or pay-to-script-hash).
        NOX is the 64 bit spend amount in nox.
    -v value
        the transaction version (default 1)
```

#### Example

```bash
~ qx tx-encode -i 1b99ad8f271124533bf49cd943124d65a24de3266078391a6e6e92bae42849c8:2 -l 0 -o RmCYoUMqKZopUkai2YhUFHR9UeqjeyjTAgW:1 -o RmRYWLhtA3dkgd3vF3bEqZvsriTufMFPBRK:30

0100010001c84928e4ba926e6e1a39786026e34da2654d1243d99cf43b532411278fad991b02000000ffffffff0200e1f505000000001976a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac005ed0b2000000001976a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688ac0000000000000000
```

#### Set Locktime

If nLocktime is not zero and is less than 500 million, it is interpreted as block height, which means that the trade is invalid and is not relayed or included in the block chain before the specified block height.

If it exceeds 500 million, it is interpreted as a Unix era timestamp (the number of seconds since jan-1-1970), and the transaction is not valid until the specified time. The nLocktime transaction that specifies the future block or time must be held by the originating system and sent to the qitmeer network only after it is valid. If the transaction is transmitted to the network before the specified nLocktime, the first node rejects the transaction and is not relayed to other nodes. Using nLocktime is equivalent to a deferred check.

```bash
~ qx tx-encode -i 1b99ad8f271124533bf49cd943124d65a24de3266078391a6e6e92bae42849c8:2 -l 1562904504 -o RmCYoUMqKZopUkai2YhUFHR9UeqjeyjTAgW:1 -o RmRYWLhtA3dkgd3vF3bEqZvsriTufMFPBRK:30

0100010001c84928e4ba926e6e1a39786026e34da2654d1243d99cf43b532411278fad991b02000000feffffff0200e1f505000000001976a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac005ed0b2000000001976a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688acb807285d00000000
```

---

### tx-decode

decode a transaction in base16 to json format.

```bash
~ qx tx-decode --help

Usage: qx tx-decode [base16_string]
    -n string
        decode rawtx for the target network. (mainnet, testnet, privnet) (default "privnet")
```

#### decode testnet rawtx

```bash
~ qx tx-decode -n testnet 0100010001c84928e4ba926e6e1a39786026e34da2654d1243d99cf43b532411278fad991b02000000feffffff0200e1f505000000001976a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac005ed0b2000000001976a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688acb807285d00000000
```

```json
{
	"txid": "d0f1d098c2076c149a8bf3c650f56ce0b485c268e668aa7e79aea37454f3093d",
	"txhash": "f546294b0449f658596d93c7de02c769b6064e9b8b05f6b9b4060d396325dcf5",
	"version": 1,
	"locktime": 1562904504,
	"expire": 0,
	"vin": [{
		"txid": "1b99ad8f271124533bf49cd943124d65a24de3266078391a6e6e92bae42849c8",
		"vout": 2,
		"sequence": 4294967294,
		"amountin": 0,
		"blockheight": 0,
		"txindex": 0,
		"scriptSig": {
			"asm": "",
			"hex": ""
		}
	}],
	"vout": [{
		"amount": 100000000,
		"scriptPubKey": {
			"asm": "OP_DUP OP_HASH160 44d959afb6db4ad730a6e2c0daf46ceeb98c53a0 OP_EQUALVERIFY OP_CHECKSIG",
			"hex": "76a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac",
			"reqSigs": 1,
			"type": "pubkeyhash",
			"addresses": ["TmVE82jyakwjh6r14cwjMReoqYdCGUZcxTC"]
		}
	}, {
		"amount": 3000000000,
		"scriptPubKey": {
			"asm": "OP_DUP OP_HASH160 d364af39e59cea1488a25e3cfcc48e20f31a7b16 OP_EQUALVERIFY OP_CHECKSIG",
			"hex": "76a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688ac",
			"reqSigs": 1,
			"type": "pubkeyhash",
			"addresses": ["TmiDpu62REmftyKDH7qVwiAYDcFNGkE5HQv"]
		}
	}]
}
```

---

### tx-sign

sign a transactions using a private key.

```bash
~ qx tx-sign --help

Usage: qx tx-sign [raw_tx_base16_string]
    -k string
        the ec private key to sign the raw transaction
```

#### Example

{{% notice tip %}}
The column rawtx is not send to the node and is used as an instance only.
{{% /notice %}}

```bash
~ qx tx-sign -k 3f2314d615696244ea14e46e43322842b3e09333e62c59c4160220a52bdf6239 0100010001c84928e4ba926e6e1a39786026e34da2654d1243d99cf43b532411278fad991b02000000feffffff0200e1f505000000001976a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac005ed0b2000000001976a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688acb807285d00000000

0100000001c84928e4ba926e6e1a39786026e34da2654d1243d99cf43b532411278fad991b02000000feffffff0200e1f505000000001976a91444d959afb6db4ad730a6e2c0daf46ceeb98c53a088ac005ed0b2000000001976a914d364af39e59cea1488a25e3cfcc48e20f31a7b1688acb807285d0000000001000000000000000000000000000000006b483045022100bd22c1b3c92d3131440c8582222b123a7fca7bfec68738bbb7423ba93f483de1022079d8180e9a4d53bfd23d9286b17261f15e71336e82f2c1cef6cab2e1f0675eaf0121034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70
```
