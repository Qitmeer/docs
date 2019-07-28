---
title: "getUtxo"
date: 2019-07-29T00:38:09+08:00
weight: 0
---

## getUtxo

getUtxo {tx_hash} {vout} [include_mempool]; vout:index of the output; include_mempool: default=true,include the mempool , get information about an unspent transaction output

### Usage

```
qitmeer-cli getUtxo [flags]
```



### Alias

- getutxo

- GetUtxo

### Examples

```

getutxo a97cf4d67bbe5ce57d1d2f4fc18ae2ee19e1048cbb1a14d8d94273bfef83f371 0 true
	
```

### Options

```
  -h, --help   help for getUtxo
```

### SEE ALSO

* [qitmeer-cli blockChain](/en/reference/qitmeer-cli/blockchain/)	 

