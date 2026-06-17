---
icon: hammer
---

# Makefile 与 CMake

在 RoboMaster 视觉组中，我们常使用 C/C++ 编写图像处理、通信、硬件控制等模块。为了高效管理这些源文件及其依赖关系，需要使用**构建系统（Build System）**，最常见的工具就是 Makefile 与 CMake。

## Makefile：传统的自动构建工具

**Makefile** 是指导 `make` 工具如何编译工程文件的脚本，定义了编译规则、依赖关系与构建方式。

### 结构示例

```makefile
# 编译器
CC = g++
CFLAGS = -Wall -g

# 源文件与目标文件
SRC = main.cpp camera.cpp detect.cpp
OBJ = $(SRC:.cpp=.o)
TARGET = vision_app

# 默认构建目标
# 注意：下面的缩进必须是 Tab，不能用空格！
$(TARGET): $(OBJ)
	$(CC) $(OBJ) -o $(TARGET)

# 编译每个源文件
%.o: %.cpp
	$(CC) $(CFLAGS) -c $< -o $@

# 清除构建文件
clean:
	rm -f $(OBJ) $(TARGET)
```

> **重要**：Makefile 中命令行前必须使用 **Tab** 缩进，不能用空格，否则 `make` 会报错。

**优点**：简洁、灵活，适合小型工程；可完全控制每一步构建流程。

**局限**：跨平台困难；难以管理大型项目的依赖关系。

## CMake：现代构建系统

**CMake** 是一个跨平台的构建系统生成器——它不直接编译代码，而是根据 `CMakeLists.txt` 生成对应平台的构建文件（如 Linux 下的 Makefile、Windows 下的 VS 工程文件）。

### CMakeLists.txt 示例

```cmake
cmake_minimum_required(VERSION 3.10)
project(rm_vision)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 查找 OpenCV
find_package(OpenCV REQUIRED)

# 包含头文件目录
include_directories(${OpenCV_INCLUDE_DIRS})

# 添加可执行文件
add_executable(vision_app main.cpp camera.cpp detect.cpp)

# 链接库
target_link_libraries(vision_app ${OpenCV_LIBS})
```

### 构建流程

```bash
mkdir build
cd build
cmake ..
make
```

### 常用 CMake 命令

| 命令 | 作用 |
| --- | --- |
| `cmake_minimum_required(VERSION 3.10)` | 指定最低 CMake 版本 |
| `project(name)` | 定义项目名称 |
| `set(CMAKE_CXX_STANDARD 17)` | 设置 C++ 标准 |
| `find_package(OpenCV REQUIRED)` | 查找第三方库 |
| `include_directories(dir)` | 添加头文件搜索路径 |
| `add_executable(name src...)` | 添加可执行文件 |
| `add_library(name src...)` | 添加库 |
| `target_link_libraries(name lib...)` | 链接库 |

## Makefile vs. CMake

| 比较维度 | Makefile | CMake |
| --- | --- | --- |
| 跨平台 | 否（需手动处理） | 自动生成不同平台构建系统 |
| 适合项目规模 | 小型项目 | 中大型项目，模块化、可扩展 |
| 易用性 | 需要手写依赖关系 | 自动依赖管理，结构清晰 |
| 主流支持 | 被支持 | 被广泛使用，ROS、OpenCV 等都用 CMake |

> 在 RoboMaster 中，**推荐使用 CMake** 管理项目。ROS 2 的构建工具 `colcon` 也是基于 CMake 的。

## 推荐学习资源

* **CMake 官方教程**：[https://cmake.org/cmake/help/latest/guide/tutorial/index.html](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
* **CMake 官方文档**：[https://cmake.org/documentation/](https://cmake.org/documentation/)
* **Makefile 教程（廖雪峰）**：[https://www.liaoxuefeng.com/wiki/897692888725344](https://www.liaoxuefeng.com/wiki/897692888725344)
* **《CMake Cookbook》**— 实战导向，覆盖常见 CMake 场景
* B 站搜索："CMake 教程"

## Checkpoint

* [ ] 能手写一个简单的 Makefile 编译单个 C++ 文件
* [ ] 能编写 CMakeLists.txt 构建一个包含 OpenCV 依赖的项目
* [ ] 理解 `cmake ..` 和 `make` 各自做了什么
* [ ] 知道 Makefile 中 Tab 和空格的区别
