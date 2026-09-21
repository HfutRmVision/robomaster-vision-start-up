---
description: 安装 GCC、CMake、GDB、Git 工具链
icon: screwdriver-wrench
---

# 安装工具链

MSYS2 装好后还是"空壳"，现在把开发要用的工具一次装齐。所有命令都在 **UCRT64 终端**里执行。

## 1. 一键安装

```bash
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
pacman -S mingw-w64-ucrt-x86_64-cmake \
          mingw-w64-ucrt-x86_64-ninja \
          mingw-w64-ucrt-x86_64-make \
          mingw-w64-ucrt-x86_64-gdb \
          mingw-w64-ucrt-x86_64-git
```

装的是什么：

| 包 | 提供什么 |
| --- | --- |
| `base-devel` + `toolchain` | GCC/G++ 编译器及基础开发工具 |
| `cmake` | CMake 构建工具（我们项目的主构建工具） |
| `ninja` | 快速的构建执行器，配合 CMake 使用 |
| `make` | 传统构建工具，部分老项目需要 |
| `gdb` | 调试器，程序崩溃时定位问题 |
| `git` | 版本控制工具，协作开发必备 |

> 📷 **截图占位**：`pacman` 安装工具链的终端输出（待补充）

## 2. 验证安装

逐个输入以下命令，每条都应该打印出版本号：

```bash
gcc --version
g++ --version
gdb --version
cmake --version
git --version
```

示例输出（版本号会随时间变化，不用对得上，能打印出来就行）：

```
gcc.exe (Rev1, Built by MSYS2 project) 14.2.0
cmake version 3.30.5
git version 2.47.0.windows.1
```

如果某条命令提示 `command not found`，先检查**你是不是开错了终端**（必须是 UCRT64），再重新执行安装命令。

## 3. pacman 常用命令速查

以后装软件都靠它，先把这几条存下来：

```bash
pacman -Suy              # 更新系统和所有已安装的包
pacman -S 包名            # 安装软件包
pacman -Ss 关键词         # 搜索软件包
pacman -R 包名            # 卸载软件包
pacman -Q                # 查看已安装的所有包
```

不确定包名时，去官网搜：[https://packages.msys2.org/](https://packages.msys2.org/)。注意 UCRT64 环境的包名前缀是 `mingw-w64-ucrt-x86_64-`。

## 4. 重要约定：不要把工具链加进 Windows 全局 PATH

网上很多教程会教你把 `C:\msys64\ucrt64\bin` 添加到 Windows 系统环境变量里，**我们明确不这么做**，原因：

1. **污染环境变量**：以后你可能还会安装其他软件自带的 gcc/git（比如 Git for Windows、Anaconda），多个同名工具混在 PATH 里，你根本分不清用的是哪一个，排查问题极其痛苦。
2. **没有必要**：VS Code 里配置好 MSYS2 终端后（下一页讲），所有工作都在 MSYS2 终端里完成，把 MSYS2 当作一个独立的类 Linux 开发环境用就好。

> 记住这个原则：**MSYS2 的东西只在 MSYS2 终端里用。**

## 5. 关于 Python

本章**不安装 Python**。视觉组的入门路线直接从 C++ 开始；Python 属于选学内容，等后面需要时（比如做深度学习）再单独配置，见 [Python 入门（选学）](../advanced/python.md)。

## Checkpoint

* [ ] `gcc --version` ~ `git --version` 五条命令都能正常打印版本
* [ ] 能用 `pacman -Ss` 搜索一个软件包
* [ ] 能说出为什么我们不把 `ucrt64\bin` 加进 Windows PATH

下一步 → [配置 VS Code](vscode-config.md)
