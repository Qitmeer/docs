
---
title: wallet_importPrivKey
weight: 3
---

### wallet_importPrivKey
导入私钥 

#### Parameters
1. `accountName: (string)` 导入账户,目前只支持imported
2. `privKey: (string)` 私钥
3. `rescan: (bool)` 是否重新扫描交易记录

#### Returns

#### Example
##### Request
```json
{"jsonrpc":"1.0","method":"wallet_importPrivKey","params":["imported","xxxxxx",true],"id":1}
```
##### Response
