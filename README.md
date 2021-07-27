# Gree Air Conditioner Platform

## Installation

```
npm install homebridge-gree-air-conditioner -g
```

## Configuration (mininal)

```
{
    "platforms": [
        {
            "platform": "GreeAirConditioner",
            "scanAddress": "192.168.1.255",
        }
    ]
}
```

## Configuration (optional)

```
{
    "platforms": [
        {
            "platform": "GreeAirConditioner",
            "name": "My Gree",
            "port": 7002,
            "scanCount": 10,
            "scanTimout": 3000,
            "scanAddress": "192.168.1.255",
            "defaultValue": {
                "minimumTargetTemperature": 16,
                "maximumTargetTemperature": 30,
                "sensorOffset": 40,
                "defaultSpeed": 3,
                "statusUpdateInterval": 3,
            },
            "devices": [
                { 
                    "mac": "c8f742xxxxxx",
                    "sensorOffset": 40,
                    "defaultSpeed": 3,
                    "disabled": false,
                }
            ]
        }
    ]
}
```

**GET MAC ADDRESS**

From Home App Accessory

![mac_address](./device_mac.jpeg)

From Gree+ App

![mac_address2](./device_mac2.jpeg)

## Features/TODO

- [x] 设备独立设置

- [x] 电源控制
- [x] 温度调节
- [x] 模式调节 （不支持 送风，除湿）
- [x] 静音模式
- [x] 强劲模式
- [x] 左右扫风
- [x] 上下扫风
- [x] 指示灯控制
## Developing

```
npm run watch
```

## 空调遥控器按键功能整理

### 开关

控制电源开关

| label | code         |
| ----- | ------------ |
| 开    | `{ Pow: 1 }` |
| 关    | `{ Pow: 0 }` |

### 模式

模式切换按钮，会保存有 `SetTem`, `TemSen`, `WdSpd` 的数据

| label | code |
| ----- | ---- |
| 自动 | `{ Mod: 0, SetTem: 25, TemSen: 67, WdSpd: 3 }` |
| 制冷 | `{ Mod: 1, SetTem: 28, TemSen: 68, WpSpd: 0 }` |
| 除湿 | `{ Mod: 2, SetTem: 25, TemSen: 67, WpSpd: 3 }` |
| 送风 | `{ Mod: 3, SetTem: 26, TemSen: 67, WpSpd: 3 }` |
| 制热 | `{ Mod: 4, SetTem: 27, TemSen: 64, WpSpd: 3 }` |

### 风速

| label | code                             |
| ----- | -------------------------------- |
| 自动  | `{ Quiet: 0, Tur: 0, WdSpd: 0 }` |
| 静音  | `{ Quiet: 2, Tur: 0, WdSpd: 1 }` |
| 1 级  | `{ Quiet: 0, Tur: 0, WdSpd: 1 }` |
| 2 级  | `{ Quiet: 0, Tur: 0, WdSpd: 2 }` |
| 3 级  | `{ Quiet: 0, Tur: 0, WdSpd: 3 }` |
| 4 级  | `{ Quiet: 0, Tur: 0, WdSpd: 4 }` |
| 5 级  | `{ Quiet: 0, Tur: 0, WdSpd: 5 }` |
| 强劲  | `{ Quiet: 0, Tur: 1, WdSpd: 5 }` |


- 自动模式下，风速在 “自动”，“1 级”，“2 级”，“3 级”，“4 级”，“5 级” 之间循环
- 制冷模式下，风速在 “自动”，“静音”，“1 级”，“2 级”，“3 级”，“4 级”，“5 级”，“强劲” 之间循环
- 除湿模式下，风速只能停留在“1 级”
- 送风模式下，风速在 “自动”，“1 级”，“2 级”，“3 级”，“4 级”，“5 级” 之间循环
- 制热模式下，风速在 “自动”，“静音”，“1 级”，“2 级”，“3 级”，“4 级”，“5 级”，“强劲” 之间循环

### 凉感

凉感对应的 ColCode 不明

### 上下扫风

| label | code            |
| ----- | --------------- |
| 开    | `{ SwUpDn: 1 }` |
| 关    | `{ SwUpDn: 0 }` |

### 左右扫风

| label | code                |
| ----- | ------------------- |
| 开    | `{ SwingLfRig: 1 }` |
| 关    | `{ SwingLfRig: 0 }` |

### 定向导风

| label | code            | 遥控 | app |
| ----- | --------------- | ---- | --- |
| 上    | `{ SwUpDn: 2 }` | x    | x   |
| 中上  | `{ SwUpDn: 3 }` | o    | x   |
| 中    | `{ SwUpDn: 4 }` | x    | x   |
| 中下  | `{ SwUpDn: 5 }` | o    | x   |
| 下    | `{ SwUpDn: 6 }` | x    | x   |

### 制冷、制热

模式切换按钮，分别与模式中的 “制冷”， “制热” 对应
[参考](https://github.com/tomikaa87/gree-remote#scheduling)

### 定时

定时开关机，与 APP 上的“预约”为同一个功能
### 睡眠

睡眠模式的切换

| label | code                |
| ----- | ------------------- |
| 开    | `{ SwhSlp: 1 }` |
| 关    | `{ SwhSlp: 0 }` |

睡眠模式下的四个档位，具体对应的 ColCode 不明

- 睡眠1 - 舒睡模式
- 睡眠2 - 舒醒模式
- 睡眠3 - 自定义模式
- 睡眠4 - 午睡模式

### 灯光

面板灯光显示

| label | code                |
| ----- | ------------------- |
| 开    | `{ Lig: 1 }` |
| 关    | `{ Lig: 0 }` |
### 辅热

制热模式下的功能。


## Refs & Credits

- [gree-remote](https://github.com/tomikaa87/gree-remote)
- [homebridge-gree-heatercooler-v2](https://github.com/Elethom/homebridge-gree-heatercooler-v2)
- [Homebridge YeeLight Wi-Fi](https://github.com/vieira/homebridge-yeelight-wifi)
