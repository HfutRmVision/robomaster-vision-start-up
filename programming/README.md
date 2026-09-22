---
description: C/C++ 入门指南
icon: copyright
---

# C/C++ 入门

## C 和 C++ 的区别

* **C 语言**：面向过程，语法简洁，适合底层驱动开发（电机控制、传感器读取）
* **C++**：在 C 基础上引入面向对象（类、继承、多态）和泛型编程（模板、STL），适合构建复杂的视觉算法框架

**两者语法兼容，组内主要使用C++，建议直接学习C++。**

## 在 RoboMaster 中的应用

* **自瞄算法**：C++ 实现 YOLO 推理 + 装甲板检测 + 弹道解算，满足实时性要求
* **ROS 2 节点**：用 `rclcpp` 编写高性能 ROS 2 节点
* **OpenCV C++**：`cv::Mat` 操作比 Python 版本快 5-10 倍
* **硬件通信**：串口、USB、CAN 等底层通信用 C/C++ 实现

## 核心知识点

### C 语言基础

* **基本语法**：变量、数据类型、运算符、控制流
* **指针与数组**：C 语言的灵魂——内存地址的直接操作
* **函数**：参数传递、返回值、函数指针
* **结构体**：自定义数据类型
* **内存管理**：`malloc` / `free`，动态内存分配

### C++ 进阶

* **面向对象**：类、构造/析构函数、继承、多态、虚函数
* **STL 标准模板库**：`vector`、`string`、`map`、`unordered_map`、`algorithm`
* **智能指针**：`unique_ptr`、`shared_ptr`，自动管理内存
* **模板**：泛型编程
* **Lambda 表达式**：匿名函数，配合 STL 算法使用

## 学习路线

1. **C 基础**（2-3 周）：语法、指针、数组、结构体
2. **C++ 面向对象**（2 周）：类、继承、多态
3. **STL**（1 周）：`vector`、`map`、`algorithm`，能熟练使用
4. **实战**：用 C++ + OpenCV 实现一个简单的图像处理程序

## 推荐学习资源

**在线教程**

* 菜鸟教程 C 语言：[https://www.runoob.com/cprogramming/c-tutorial.html](https://www.runoob.com/cprogramming/c-tutorial.html)
* CPlusPlus.com：[https://www.cplusplus.com/](https://www.cplusplus.com/) — C++ 标准库参考

**书籍**

* 《C Primer Plus》— C 语言入门，循序渐进
* 《C++ Primer（第 5 版）》— C++ 系统学习，经典教材
* 《C 和指针》— 深入理解指针，攻克 C 语言难点

**视频课程**

* B 站浙江大学翁恺 C 语言（BV 号：BV1dr4y1n7vA）
* B 站黑马程序员 C++ 教程（BV 号：BV1et411b73Z）

## 开发环境

* **Linux**：GCC + GDB + CMake（推荐），或 VS Code + C/C++ 插件。安装命令：`sudo apt install build-essential gdb cmake`
* **Windows**：MSVC 或 MinGW，建议用 WSL2 开发
* **构建工具**：CMake（必学），详见 [Makefile 与 CMake](engineering/makefile-yu-cmake.md) 章节

## Checkpoint

* [ ] 理解指针的概念，能正确使用指针操作数组
* [ ] 能用 C++ 定义类，理解构造函数和析构函数
* [ ] 能熟练使用 `std::vector`、`std::string`、`std::map`
* [ ] 理解虚函数和多态的用途
* [ ] 能用 CMake 构建一个包含多文件的 C++ 项目
