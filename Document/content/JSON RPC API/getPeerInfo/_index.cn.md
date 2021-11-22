---
title: getPeerInfo
weight: 1
---

## getPeerInfo
### 函数名：getPeerInfo 
### 说明：无参数，取邻近节点信息

#### 实例
```
curl -s -k -u test:test -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"getPeerInfo","params":[],"id":null}' https://127.0.0.1:18131
```

输出:
```
[
  {
    "uuid": "f280f357-ee4a-4958-90bf-685d24129703",
    "id": 5,
    "addr": "103.1.154.227:18130",
    "addrlocal": "10.198.1.66:56261",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576243,
    "lastrecv": 1593576298,
    "bytessent": 5029,
    "bytesrecv": 7315,
    "conntime": 1593575403,
    "timeoffset": 0,
    "pingtime": 371602,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "b0c3462f-328d-45ba-8e3f-490c205eec85",
    "id": 6,
    "addr": "47.103.61.128:18130",
    "addrlocal": "10.198.1.66:56262",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576298,
    "lastrecv": 1593576299,
    "bytessent": 2941,
    "bytesrecv": 16892,
    "conntime": 1593575403,
    "timeoffset": 0,
    "pingtime": 871878,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "349a58ee-3537-4576-ba8a-925a27725070",
    "id": 7,
    "addr": "106.15.102.183:18130",
    "addrlocal": "10.198.1.66:56284",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576254,
    "lastrecv": 1593576298,
    "bytessent": 1471,
    "bytesrecv": 7965,
    "conntime": 1593575414,
    "timeoffset": 0,
    "pingtime": 485255,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "400176fd-8155-405c-ae4f-032948581558",
    "id": 8,
    "addr": "148.70.34.136:18130",
    "addrlocal": "10.198.1.66:56413",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576307,
    "lastrecv": 1593576308,
    "bytessent": 1757,
    "bytesrecv": 11162,
    "conntime": 1593575465,
    "timeoffset": 0,
    "pingtime": 830143,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "1df6c4ca-dae0-4632-bdb2-d9ef916b7580",
    "id": 1,
    "addr": "104.224.174.141:18130",
    "addrlocal": "10.198.1.66:56182",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576333,
    "bytessent": 4259,
    "bytesrecv": 1214,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 244235,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "3b3b4e71e7ab837635da8442afb98ba4092a2df62cf25e59a58bda518ce81fca main"
      ],
      "mainorder": 21065,
      "mainheight": 20597,
      "layer": 20597
    }
  },
  {
    "uuid": "a8383106-45dc-4028-ae04-74d25ad09f7d",
    "id": 2,
    "addr": "144.202.90.65:18130",
    "addrlocal": "10.198.1.66:56177",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576333,
    "bytessent": 5178,
    "bytesrecv": 8411,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 259579,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": true,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "277d5f3f-3af3-486e-92ca-8da59eaa6db9",
    "id": 4,
    "addr": "122.112.245.133:18130",
    "addrlocal": "10.198.1.66:56180",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576334,
    "bytessent": 1692,
    "bytesrecv": 9459,
    "conntime": 1593575373,
    "timeoffset": 0,
    "pingtime": 414095,
    "version": 20,
    "subver": "qitmeer:0.9.0",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  },
  {
    "uuid": "38d8647f-371d-47c6-924b-ddfe32391a83",
    "id": 3,
    "addr": "103.29.70.78:18130",
    "addrlocal": "10.198.1.66:56175",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1593576333,
    "lastrecv": 1593576334,
    "bytessent": 2421,
    "bytesrecv": 6656,
    "conntime": 1593575373,
    "timeoffset": -1,
    "pingtime": 345824,
    "version": 21,
    "subver": "qitmeer:0.9.1",
    "inbound": false,
    "banscore": 0,
    "syncnode": false,
    "graphstate": {
      "tips": [
        "0002cf49681506f5b9915c4fa199e76abc8a7d7ade9cafbe1cd1f84ec89e0704 main"
      ],
      "mainorder": 21199,
      "mainheight": 20730,
      "layer": 20730
    }
  }
]

```

