---
description: 安装并配置 VS Code，接入 MSYS2 环境
icon: code
---

# 配置 VS Code

VS Code 是我们的主力代码编辑器。这一页把它和 MSYS2 打通：在 VS Code 里直接打开 MSYS2 终端、让代码补全和跳转正常工作。

## 1. 安装 VS Code

从官网下载安装：[https://code.visualstudio.com/](https://code.visualstudio.com/)

安装时建议勾选「添加到右键菜单」相关选项，以后可以在文件夹上右键直接"通过 Code 打开"。

## 2. 安装必装插件

打开 VS Code，点击左侧扩展图标（或按 `Ctrl+Shift+X`），搜索并安装：

1. **Chinese (Simplified)** —— 中文界面语言包
2. **C/C++**（Microsoft）—— 代码补全、跳转、调试
3. **CMake Tools**（Microsoft）—— CMake 项目配置和一键构建
4. **CMake**（twxs）—— CMakeLists.txt 语法高亮

## 3. 把 MSYS2 终端搬进 VS Code（关键一步）

在 VS Code 里按 `Ctrl+Shift+P` 打开命令面板，输入 `settings json`，选择「首选项：打开用户设置 (JSON)」，在配置中加入：

```json
"terminal.integrated.profiles.windows": {
    "MSYS2 UCRT": {
        "path": "C:\\msys64\\msys2_shell.cmd",
        "args": [
            "-defterm",
            "-here",
            "-no-start",
            "-ucrt64"
        ]
    }
},
"terminal.integrated.defaultProfile.windows": "MSYS2 UCRT"
```

保存后，按 `` Ctrl+` ``（反引号，Tab 键上方）打开终端，应该直接进入 UCRT64 环境——提示符里能看到 `UCRT64` 字样。

> 参数解释：`-defterm` 使用当前终端窗口；`-here` 终端起始目录定位到当前文件夹；`-no-start` 不再额外弹窗；`-ucrt64` 使用 UCRT64 环境。知道含义即可，不用背。

## 4. 让代码补全和跳转正常工作

刚装好时，VS Code 不认识 MSYS2 的编译器，打开 `.cpp` 文件可能会在 `#include <iostream>` 下面画红线。

两种解决办法，任选其一：

**方法一（推荐）**：把鼠标悬停在红线上，点击「快速修复」，选择「编辑 includePath 设置」，在编译器路径里选 `C:/msys64/ucrt64/bin/g++.exe`。

**方法二（手动）**：在工作区的 `.vscode/settings.json`（没有就新建）中加入：

```json
{
    "C_Cpp.default.compilerPath": "C:/msys64/ucrt64/bin/g++.exe"
}
```

配置后红线会消失，`Ctrl+点击` 就能跳转到标准库头文件了。

## 5. 配置 CMake Tools

第一次打开带 `CMakeLists.txt` 的项目文件夹时，CMake Tools 会引导你：

1. 底部状态栏点「No Kit Selected」，选择 **GCC for x86\_64-w64-mingw32（UCRT64）** 对应的 kit
2. 生成器选 **Ninja**（如果询问的话）

以后每次打开项目，点底部状态栏的 **Build** 即可编译，**运行/调试图标**即可执行。具体怎么写 `CMakeLists.txt`，见 [Makefile 与 CMake](../programming/engineering/makefile-and-cmake.md) 章节。

## 6. 可选进阶：clangd 与 clang-format（初学者可跳过）

C/C++ 插件自带的补全能力有限。如果之后想要更强的代码补全和统一格式化，可以在 UCRT64 终端安装：

```bash
pacman -S mingw-w64-ucrt-x86_64-clang-tools-extra
```

然后在 VS Code 安装 **clangd**、**Clang-Format** 插件，并在设置中指定路径：

```json
"C_Cpp.intelliSenseEngine": "disabled",
"clangd.path": "C:\\msys64\\ucrt64\\bin\\clangd.exe",
"clang-format.executable": "C:\\msys64\\ucrt64\\bin\\clang-format.exe"
```

> 初学阶段用默认的 C/C++ 插件完全够用，这节可以先跳过，遇到补全不够用时再回来。

## Checkpoint

* [ ] VS Code 终端能打开并进入 UCRT64 环境
* [ ] 写一个 `hello.cpp`，`#include <iostream>` 不报红线
* [ ] 知道 CMake Tools 的 kit 选 GCC、生成器选 Ninja
