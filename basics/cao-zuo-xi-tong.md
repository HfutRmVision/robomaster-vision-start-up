---
icon: computer
---

# 操作系统

操作系统是管理计算机硬件与软件资源的系统软件，核心功能包括进程管理、内存管理、文件系统管理、设备管理。在 RoboMaster 视觉组工作中，操作系统直接影响视觉算法的运行效率和稳定性。

## 为什么视觉组要学操作系统？

视觉程序通常需要同时处理多路任务：

* 相机采集线程持续读取图像
* 算法线程做目标检测
* 通信线程把结果发给下位机
* 可能有日志线程、心跳线程等

如果不理解进程/线程、同步互斥、调度优先级，你写的多线程程序很容易出现竞态条件、死锁、资源饥饿等问题。

你需要掌握的核心概念：

* **进程与线程**：区别、创建、通信方式
* **同步与互斥**：互斥锁、条件变量、信号量
* **内存管理**：虚拟内存、内存映射
* **IO 模型**：阻塞 IO、非阻塞 IO、IO 多路复用（select/epoll）— 进阶内容，用到再学，不用一上来就啃

## Linux

RoboMaster 视觉组的程序几乎都运行在 Linux（通常是 Ubuntu）上。你不需要精通操作系统原理，但必须熟练使用 Linux。

### Linux 环境搭建方式

| 方式 | 推荐场景 | 说明 |
| --- | --- | --- |
| 原生安装 | 不推荐主力机用 | 性能最好但日常软件兼容性差 |
| 虚拟机（VMware/VirtualBox） | 入门开发推荐 | 隔离安全，但性能有损耗 |
| WSL2 | Windows 用户推荐 | 微软官方方案，与 Windows 共存，体验好 |
| Docker | 环境隔离推荐 | 轻量，适合部署和团队环境统一 |

* 虚拟机安装教程：[https://blog.csdn.net/weixin\_74195551/article/details/127288338](https://blog.csdn.net/weixin_74195551/article/details/127288338)
* WSL2 安装教程：[https://blog.csdn.net/weixin\_44301630/article/details/122390018](https://blog.csdn.net/weixin_44301630/article/details/122390018)
* Docker 教程：[https://www.runoob.com/docker/docker-tutorial.html](https://www.runoob.com/docker/docker-tutorial.html)

### Linux 常用命令

必须熟练掌握的基本命令：

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
ifconfig / ip addr  # 查看 IP 地址
ping 192.168.1.1    # 测试网络连通性
ssh user@host       # 远程登录
scp file user@host:/path  # 远程复制文件
```

### 包管理

Ubuntu 使用 `apt` 管理软件包：

```bash
sudo apt update          # 更新软件源
sudo apt install build-essential  # 安装编译工具链
sudo apt install cmake   # 安装 CMake
sudo apt install libopencv-dev  # 安装 OpenCV
```

## 推荐学习资源

* **Linux 基础教程**：[https://www.runoob.com/linux/linux-tutorial.html](https://www.runoob.com/linux/linux-tutorial.html)
* **《鸟哥的 Linux 私房菜》**：Linux 入门经典，建议通读基础篇
* **B 站搜索**："Linux 基础入门"、"Ubuntu 教程"
* **操作系统原理**（选学）：《Operating System Concepts》或 MIT 6.828 课程
* **Linux 内核源码**：[https://github.com/torvalds/linux](https://github.com/torvalds/linux)（进阶选学）

## Checkpoint

* [ ] 能在 Linux 下完成文件的增删改查
* [ ] 理解进程和线程的区别
* [ ] 能用 `top` 或 `htop` 查看系统资源占用
* [ ] 能用 `ssh` 远程登录另一台机器并用 `scp` 传文件
* [ ] 能用 `apt` 安装软件包
