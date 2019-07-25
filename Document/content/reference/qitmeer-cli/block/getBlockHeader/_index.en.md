---
title: "getBlockHeader"
date: 2019-07-25T10:02:56+08:00
weight: 0
---

## getBlockHeader

getBlockHeader {number|hash} [verbose];verbose:bool,show detail,defalut true; get block by number or hash

### Usage

```
qitmeer-cli block getBlockHeader {number|hash} [verbose] [flags]
```



### Alias

- getblockheader

- GetBlockHeader

### Examples

```

getBlockHeader 100 false

getBlockHeader 100

getBlockHeader 000000e4c6b7f5b89827711d412957bfff5c51730df05c2eedd1352468313eca

getBlockHeader 000000e4c6b7f5b89827711d412957bfff5c51730df05c2eedd1352468313eca true
	
```

### Options

```
  -h, --help   help for getBlockHeader
```

### SEE ALSO

* [qitmeer-cli block](/en/reference/qitmeer-cli/block/)	 

