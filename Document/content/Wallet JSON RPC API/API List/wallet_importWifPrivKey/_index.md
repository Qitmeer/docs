---
title: wallet_importWifPrivKey
weight: 3
---

## wallet_importWifPrivKey 
### info: 导入wif格式私钥
### args：
- accountName 导入账户,目前只支持imported
- privKey 私钥
- rescan  bool,是否重新扫描交易记录
### example:
```json
{"id":1574750774018,"method":"wallet_importWifPrivKey","params":["imported","xxxxx",false]}
```