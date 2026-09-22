---
description: 下载并安装 MSYS2
icon: download
---

# 安装 MSYS2

MSYS2 是一个 Windows 上的软件发行与构建平台，提供接近 Linux 的命令行环境和 `pacman` 包管理器。视觉组的 C/C++ 入门开发都建立在它上面。

## 1. 下载

打开 MSYS2 官网：[https://www.msys2.org/](https://www.msys2.org/)，下载最新版安装包。

* 绝大多数电脑选 **x86\_64** 版本（文件名类似 `msys2-x86_64-latest.exe`）
* 只有 ARM 架构的电脑（极少数）才需要 ARM64 版本

## 2. 安装

双击运行安装包，一路下一步即可，只有一点要注意：

* **安装路径用默认的 `C:\msys64`**。如果一定要改，确保路径**短、纯英文、无空格、无中文**，否则会引发各种诡异问题。

> 如果 Windows 弹出 SmartScreen 安全警告，点击「更多信息」→「仍要运行」。

安装完成后，开始菜单里会出现一组 MSYS2 快捷方式，分别对应不同的"环境"。

## 3. MSYS2 的几种环境

安装后你会看到好几个快捷方式（MSYS2 MSYS、MSYS2 UCRT64、MSYS2 MINGW64、MSYS2 CLANG64……），它们是不同的编译环境：

| 环境         | 说明                                                | 我们要用吗        |
| ---------- | ------------------------------------------------- | ------------ |
| **UCRT64** | 使用现代 Windows 运行时的 64 位环境，支持最新的 C++ 标准库            | ✅ **我们用它入门** |
| MSYS       | 类 Unix 基础环境，编译出的程序依赖 MSYS2 的 DLL，不适合发布 Windows 程序 | ❌            |
| MINGW64    | 旧版运行时，已逐步淘汰                                       | ❌            |
| CLANG64    | 使用 Clang 编译器的环境                                   | ❌（进阶再了解）     |

> **记住：以后每次说"打开 MSYS2 终端"，指的都是打开 UCRT64 那个。**&#x20;

## 4. 第一次更新

从开始菜单打开 **MSYS2 UCRT64**，你会看到一个命令行窗口。输入以下命令并回车：

```bash
pacman -Suy
```

`pacman` 是 MSYS2 的包管理器（类似手机上的应用商店），这条命令会把系统更新到最新。

更新过程中可能会出现提示：

> To complete this update all MSYS2 processes including this terminal will be closed.

意思是它需要**关闭终端来完成更新**。照做：关掉窗口，重新从开始菜单打开 UCRT64 终端，再次运行 `pacman -Suy`。**重复这个过程，直到它不再提示有新的更新为止。**

> **为什么必须更新？** MSYS2 是滚动更新的发行版，不先更新就安装软件包，很容易出现依赖错乱或签名错误。以后每次安装新包之前，也建议先 `pacman -Suy`。

## 5. 可选：更换国内镜像源

如果下载速度很慢，可以把软件源换成清华大学镜像。在 UCRT64 终端里执行：

```bash
sed -i "s#https\?://mirror.msys2.org/#https://mirrors.tuna.tsinghua.edu.cn/msys2/#g" /etc/pacman.d/mirrorlist*
```

然后再运行一次 `pacman -Suy` 刷新即可。

## Checkpoint

* [ ] 能从开始菜单区分并打开 **UCRT64** 终端
* [ ] 完成了首次更新（`pacman -Suy` 运行到无更新为止）
* [ ] 能说出为什么我们用 UCRT64 而不是 MSYS / MINGW64
