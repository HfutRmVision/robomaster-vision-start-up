---
icon: penguin
---

# WSL2 / 实体 Ubuntu：Linux 环境分支

视觉组的入门路线在 Windows + MSYS2 上就能走完，但最终程序要跑在机器人上的 Linux 系统里。这页讲清楚两件事：**什么时候需要从 MSYS2 切到 Linux**，以及**怎么切**。

## 什么时候需要 Linux 环境？

继续留在 MSYS2 就好的情况：

* 学习 C/C++、CMake、Git
* 用 OpenCV 做图像处理实验
* 写不依赖 Linux 特性的算法原型

需要切到 Linux 的情况：

* **学习或使用 ROS 2** —— ROS 2 官方主要支持 Linux，Windows 支持不完善
* **部署到 Jetson / 机器人上位机** —— 它们是 Ubuntu 系统
* 用到 Linux 特有的 API（epoll、特定驱动 SDK 等）

> 简单记法：**算法入门在 MSYS2，上真机前切 Ubuntu。** 不用一开始就纠结，需要时自然会切。

## 三种获得 Linux 环境的方式

| 方式 | 适合场景 | 说明 |
| --- | --- | --- |
| **WSL2** | 在 Windows 上学习 ROS 2 / Linux（推荐） | 微软官方方案，与 Windows 共存，启动快，VS Code 可直连 |
| 实体 Ubuntu（双系统） | 长期主力开发 | 性能最好，但切换麻烦，日常软件生态差 |
| 虚拟机 | 临时体验 | 隔离安全，性能损耗大，不推荐做开发主力 |

**系统版本统一用 Ubuntu 22.04** —— 这是 ROS 2 Humble（LTS）的推荐系统，也是 Jetson 上常见的系统版本，学一次到处通用。

## WSL2 安装要点

1. 管理员身份打开 PowerShell，执行 `wsl --install -d Ubuntu-22.04`
2. 重启电脑，首次启动设置用户名和密码
3. VS Code 安装 **WSL** 插件，在 WSL 终端里输入 `code .` 即可让 VS Code 直接开发 Linux 里的项目

详细教程可参考微软官方文档：[https://learn.microsoft.com/zh-cn/windows/wsl/install](https://learn.microsoft.com/zh-cn/windows/wsl/install)

> WSL2 与 MSYS2 不冲突，可以共存：MSYS2 用于 Windows 下的 C/C++ 入门，WSL2 用于 ROS 2 和 Linux 学习。

## Linux 常用命令速查

切到 Linux 后，这些命令必须熟练：

```bash
# 文件操作
ls -la          # 查看文件列表（含隐藏文件）
cd /path        # 切换目录
cp -r src dst   # 复制文件/目录
mv old new      # 移动/重命名
rm -rf dir      # 删除（谨慎使用！）
find . -name "*.cpp"  # 查找文件
chmod +x script.sh    # 添加执行权限

# 文本处理
cat file        # 查看文件内容
grep "keyword" file  # 搜索关键词
nano / vim file  # 编辑文件

# 系统监控
top             # 查看进程和资源占用
htop            # top 的增强版
df -h           # 查看磁盘空间
nvidia-smi      # 查看 GPU 状态（如有 NVIDIA 显卡）

# 网络
ip addr             # 查看 IP 地址
ping 192.168.1.1    # 测试网络连通性
ssh user@host       # 远程登录（调试机器人上位机必备）
scp file user@host:/path  # 远程复制文件
```

包管理用 `apt`：

```bash
sudo apt update          # 更新软件源
sudo apt install build-essential  # 安装编译工具链
sudo apt install cmake   # 安装 CMake
sudo apt install libopencv-dev  # 安装 OpenCV
```

## 操作系统概念（进阶理论）

等你开始写多线程视觉程序（相机采集、算法推理、通信发送同时跑），这些概念会变成真问题：

* **进程与线程**：区别、创建、通信方式——多线程抢同一个相机会崩
* **同步与互斥**：互斥锁、条件变量、信号量——竞态条件、死锁的根源
* **内存管理**：虚拟内存、内存映射——算法把内存吃满会卡死系统
* **IO 模型**：阻塞 IO、非阻塞 IO、IO 多路复用——通信延迟优化的基础

不需要现在就啃操作系统原理，**用到再回来补**。

## 推荐学习资源

* **Linux 基础教程**：[https://www.runoob.com/linux/linux-tutorial.html](https://www.runoob.com/linux/linux-tutorial.html)
* **《鸟哥的 Linux 私房菜》**：Linux 入门经典，通读基础篇
* **操作系统原理**（选学）：《Operating System Concepts》或 MIT 6.828 课程

## Checkpoint

* [ ] 能说出什么情况下需要从 MSYS2 切到 Linux
* [ ] 能装好 WSL2 + Ubuntu 22.04 并用 VS Code 连接
* [ ] 能在 Linux 下完成文件的增删改查，用 `apt` 安装软件
* [ ] 能用 `ssh` 远程登录另一台机器并用 `scp` 传文件
