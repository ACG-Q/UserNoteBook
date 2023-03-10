---
title: 连接EV3设备成功
date created: 星期一, 一月 30日 2023, 8:53:55 早上
date modified: 星期二, 二月 7日 2023, 2:20:10 下午
---

# 连接 EV3 设备成功

![[Pasted image 20230112141004.png]]

# 模拟 Scratch 连接

```javascript
new WebSocket("wss://device-manager.scratch.mit.edu:20110/scratch/ble").close()
var ws = new WebSocket("ws://127.0.0.1:20111/scratch/ble")
ws.onmessage = (v)=> {
    console.log(v.data)
    let d = JSON.parse(v.data)
    try {
        if(d.method === "didDiscoverPeripheral"){
            ws.send(JSON.stringify({"jsonrpc":"2.0","method":"connect","params":{"peripheralId":d.params.peripheralId},"id":1}))
        }
    }catch {}
}

ws.onopen = () => {
    ws.send(JSON.stringify({"jsonrpc":"2.0","method":"discover","params":{"filters":[{"services":["00001523-1212-efde-1523-785feabcd123"]}],"optionalServices":["00004f0e-1212-efde-1523-785feabcd123"]},"id":0}))
}
```

## 测试结果

| 系统      | scratch-link 版本 | 测试次数 | 成功次数 |比例|失败原因|
| --------- | ----------------- | -------- | -------- | ---- | ---------------- |
| Windows10 | 1.4.3.0           | 3        | 2        |      | wedo 熄灯了       |
| Windows11 | 1.4.3.0           | 3        | 1        |      | 忘了插蓝牙接收器 |
| Windows7  | 1.4.3.0           | 0        | 0        |      |  |

> [!tip] 排除操作问题

| 系统      | scratch-link 版本 | 测试次数 | 成功次数 | 比例 | 失败原因     |
| --------- | ----------------- | -------- | -------- | ---- | ------------ |
| Windows10 | 1.4.3.0           | 4        | 4        | 100% |              |
| Windos11  | 1.4.3.0           | 4        | 3        | 100% |              |
| Windows7  | 1.4.3.0           |          |          |      |无法连接 BLE <br>原因协议版本不统一|

> [!tip] Scratch 官方的 Scratch-link 已经不允许 Windows 10 以下的用户安装

