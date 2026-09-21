---
description: 跑通第一个 C++ 程序，排查常见问题
icon: circle-check
---

# 验证与排坑

环境装好不算完，跑通代码才算。这一页用两个小程序验证整套环境，并整理了新手最高频的坑。

## 1. 验证一：用 g++ 编译 hello world

在 VS Code 里新建一个文件夹（比如 `hello`），创建 `hello.cpp`：

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, RoboMaster!" << std::endl;
    return 0;
}
```

在 MSYS2 UCRT 终端中编译并运行：

```bash
g++ hello.cpp -o hello.exe
./hello.exe
```

看到输出 `Hello, RoboMaster!`，说明编译器和终端都没问题。

> 📷 **截图占位**：终端中编译并运行 hello world 的输出（待补充）

## 2. 验证二：用 CMake 构建项目

实际项目不会手动敲 `g++`，而是用 CMake 管理。在刚才的文件夹里创建 `CMakeLists.txt`：

```cmake
cmake_minimum_required(VERSION 3.10)
project(hello)

set(CMAKE_CXX_STANDARD 17)

add_executable(hello hello.cpp)
```

然后在终端中执行：

```bash
mkdir build
cd build
cmake -G Ninja ..
cmake --build .
./hello.exe
```

同样输出 `Hello, RoboMaster!`，说明 CMake + Ninja 这条主线也通了。

> 这三条命令（`cmake` 配置 → `cmake --build` 构建 → 运行）是以后每个项目的固定流程，建议理解每一步在做什么，详见 [Makefile 与 CMake](../programming/engineering/makefile-yu-cmake.md)。

## 3. 常见坑自查表

遇到问题先对照这张表，90% 的新手问题都在这里：

| 症状 | 原因 | 解决 |
| --- | --- | --- |
| `gcc` / `cmake` 提示 `command not found` | 开错了终端（打开了 MSYS 而不是 UCRT64） | 关掉，从开始菜单打开 **MSYS2 UCRT64** |
| VS Code 终端里没有 gcc | 终端 profile 没配对 | 回到 [配置 VS Code](vscode-config.md) 第 3 节检查 settings.json |
| 装包报错、提示签名错误 | 装 MSYS2 后没做首次更新，或很久没更新 | 运行 `pacman -Suy`，提示关终端就关掉重开，直到无更新 |
| `cmake` 报错找不到 generator | 没装 Ninja | `pacman -S mingw-w64-ucrt-x86_64-ninja` |
| `#include <iostream>` 画红线 | VS Code 没配编译器路径 | 见 [配置 VS Code](vscode-config.md) 第 4 节 |
| 系统里装了多个 gcc，版本对不上 | 把 `ucrt64\bin` 加进了 Windows PATH，或装了其他软件自带的编译器 | 移除 Windows PATH 里的相关条目，只在 MSYS2 终端中使用工具链 |
| 安装/编译报路径相关错误 | 安装路径或项目路径有中文、空格 | 换到纯英文路径（如 `C:\msys64`、`D:\code\`） |
| 下载包特别慢 | 默认镜像源在国外 | 换清华镜像源，见 [安装 MSYS2](install-msys2.md) 第 5 节 |

## 4. 还是解决不了？

按这个顺序来：

1. **完整读一遍报错**——报错信息里往往直接写了原因，先自己翻译着看
2. **搜索报错关键词**——把报错粘到搜索引擎，加上 `MSYS2` 关键词
3. **群里提问**——提问时附上：① 你在哪一步；② 完整命令和完整报错截图；③ 你已经试过什么。只说"报错了"没人能帮你

## Checkpoint

* [ ] 能用 `g++` 手动编译并运行 hello world
* [ ] 能用 `cmake -G Ninja .. && cmake --build .` 构建并运行同一个程序
* [ ] 遇到 `command not found` 知道先检查什么
* [ ] 知道提问时应该附上哪些信息

🎉 到这里，你的开发环境就搭好了。接下来按路线图进入 [计算机基础知识](../basics/wei-shen-me-xue-ji-chu.md) 的学习。
