---
icon: usb
---

# 上下位机通信

在 RoboMaster 系统中，视觉算法跑在上位机（如 MiniPC、NX、NUC），而电机控制由下位机（如 STM32）负责。两者之间必须建立可靠的数据通道，视觉识别结果才能转化为机器人的实际动作。

## 什么是上位机和下位机？

* **上位机**：负责高层逻辑的计算单元，运行视觉算法、路径规划、决策系统等。通常是运行 Linux 的嵌入式 PC 或 NVIDIA Jetson 系列
* **下位机**：负责底层硬件控制的微控制器（如 STM32），直接控制电机、读取传感器、执行运动控制

两者的分工：上位机"想"，下位机"做"。

## 常见通信协议

### 1. 串口通信（UART）

最常用的上下位机通信方式。

* 点对点通信，成本低，可靠性高
* 适用于传输命令、控制量、坐标数据等小数据量场景
* 常见波特率：115200、921600（RoboMaster 中常用 115200）
* 传输距离短，适合机内通信

### 2. USB（虚拟串口）

将串口通信封装在 USB 协议中，操作方式与 UART 类似，但传输速度更高。很多工业相机和下位板通过 USB 虚拟串口与上位机通信。

### 3. CAN 总线

* 多节点通信协议，一条总线上可挂多个设备
* 抗干扰能力强，实时性高
* 适合多板协同控制的场景（如底盘电控板、云台电控板之间的通信）

### 4. 以太网（TCP/UDP）

* 适用于需要高速传输大数据量的场景（如图像流）
* **TCP**：可靠、面向连接，适合不允许丢数据的场景
* **UDP**：速度快、不保证可靠性，适合实时性要求高、偶尔丢包可接受的场景

### 5. SPI / I2C

常用于嵌入式设备内部或板间短距离通信，不常用于上位机与下位机之间。

## 通信协议设计

在实际开发中，需要设计自己的通信协议——定义数据帧的格式，确保上下位机能正确解析。

### 帧结构示例

一个典型的数据帧结构：

```
| 帧头(2B) | 数据长度(1B) | 命令类型(1B) | 数据内容(NB) | 校验(2B) |
```

* **帧头**：固定标识（如 0xAA 0xBB），用于同步
* **数据长度**：数据内容的字节数
* **命令类型**：区分不同数据（如 0x01=目标位置，0x02=云台角度）
* **数据内容**：实际数据，通常用结构体打包
* **校验**：CRC16 或校验和，防止传输错误

### Python 示例：发送目标位置

```python
import struct
import serial

ser = serial.Serial('/dev/ttyUSB0', 115200, timeout=0.5)

def send_target(x, y, z):
    # 帧头 + 命令类型 + 三个float + CRC
    header = b'\xAA\xBB'
    cmd = b'\x01'
    data = struct.pack('<fff', x, y, z)  # 小端序，3个float
    length = len(data).to_bytes(1, 'little')
    crc = b'\x00\x00'  # 实际应计算CRC
    frame = header + length + cmd + data + crc
    ser.write(frame)
```

### C++ 示例：接收数据帧

```cpp
#include <serial/serial.h>
#include <cstring>

serial::Serial ser("/dev/ttyUSB0", 115200, serial::Timeout::simpleTimeout(500));

struct TargetInfo {
    float x, y, z;
};

TargetInfo receive_target() {
    uint8_t buffer[20];
    // 查找帧头 0xAA 0xBB
    // ...（省略帧头搜索逻辑）
    ser.read(buffer, sizeof(TargetInfo) + 5);
    TargetInfo target;
    memcpy(&target, buffer + 4, sizeof(TargetInfo));
    return target;
}
```

## 常用通信库

### Python

| 库 | 用途 |
| --- | --- |
| `pyserial` | 串口通信，简单易用 |
| `socket` | TCP/UDP 网络通信 |
| `pyusb` | USB 设备通信 |
| `python-can` | CAN 总线通信 |

### C++

| 库 | 用途 |
| --- | --- |
| `boost::asio` | 异步串口与网络通信，稳定高效 |
| `serial` | 轻量级串口库，适用于 ROS 环境 |
| `socket API`（`<sys/socket.h>`） | C/C++ 标准网络编程接口 |
| `libusb` | 跨平台 USB 通信 |

## RoboMaster 中的实际应用

### 视觉 → 电控数据流

1. 视觉算法检测装甲板位置（像素坐标）
2. 通过 PNP 解算得到相机坐标系下的 3D 位置
3. 坐标变换到枪口坐标系
4. 通过串口发送目标角度（yaw, pitch）和距离给下位机
5. 下位机控制云台电机转向目标

### 注意事项

* **数据对齐**：上下位机字节序（大端/小端）必须一致，否则数据会错乱
* **帧率匹配**：视觉输出帧率（如 90fps）和电控接收频率需要协调，避免数据堆积或丢失
* **超时处理**：通信中断时，上位机应有超时检测机制，避免电控使用过时数据
* **CRC 校验**：比赛中电磁环境复杂，必须加校验防止误判

## 推荐学习资源

* Python `pyserial` 文档：[https://pyserial.readthedocs.io/](https://pyserial.readthedocs.io/)
* B 站搜索："STM32 串口通信 上位机"
* RoboMaster 开源社区中的通信协议设计帖子：[https://bbs.robomaster.com/](https://bbs.robomaster.com/)

## Checkpoint

* [ ] 设计一个简单的数据帧格式，包含帧头、数据、校验
* [ ] 用 Python 的 `pyserial` 实现串口数据的收发
* [ ] 理解大端序和小端序的区别，以及为什么通信时要统一
* [ ] 思考：为什么视觉和电控之间用串口而不是直接共享内存？
