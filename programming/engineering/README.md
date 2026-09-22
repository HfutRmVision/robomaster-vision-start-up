---
description: 工程化开发能力
icon: hammer-brush
---

# 项目工程化

在 RoboMaster 视觉组的项目开发中，工程化能力是保障代码质量、提升协作效率的核心。写出一个能跑的 demo 只是起点，让代码可维护、可协作、可部署，才是工程化的意义。

## 重点学习内容

### 代码版本控制（Git）

* 掌握 Git 的基础操作：克隆、提交、分支管理、合并
* 理解团队协作中的分支策略（主分支、开发分支、功能分支的划分）
* 学会通过 Pull Request 进行代码审查与合并
* 能解决代码冲突

> → 详见 [Git 与 GitHub](git-and-github.md) 章节

### 构建工具（CMake）

* 掌握 CMake 的基本语法和项目构建流程
* 学会编写 CMakeLists.txt 管理多模块项目
* 能配置第三方库依赖和编译选项
* 实现跨平台构建

> → 详见 [Makefile 与 CMake](makefile-and-cmake.md) 章节

### 调试技能

* **GDB**：C/C++ 程序调试利器，能设断点、查看变量、单步执行
* **printf 大法**：最朴素但最有效的调试方式——在关键位置打印变量值

GDB 文档：[https://www.gnu.org/software/gdb/documentation/](https://www.gnu.org/software/gdb/documentation/)

### 设计模式与代码复用

* 学习常用设计模式的应用场景（单例、工厂、观察者等）
* 掌握代码复用技巧：封装通用模块、设计清晰接口
* 提升代码的可维护性和扩展性

推荐资料：

* 《设计模式：可复用面向对象软件的基础》
* GitHub 上的设计模式示例代码库：[https://github.com/faif/python-patterns](https://github.com/faif/python-patterns)

## RoboMaster 视觉项目结构参考

一个典型的视觉项目目录结构：

```
rm_vision/
├── CMakeLists.txt
├── src/
│   ├── detector/        # 目标检测模块
│   ├── tracker/         # 目标追踪模块
│   ├── communicator/    # 上下位机通信
│   └── utils/           # 工具函数
├── config/              # 配置文件
├── models/              # 训练好的模型
├── scripts/             # 辅助脚本
├── launch/              # ROS 2 launch 文件
└── README.md
```

## Checkpoint

* [ ] 能用 Git 完成克隆、提交、推送、分支切换
* [ ] 能用 CMake 构建一个包含 OpenCV 依赖的 C++ 项目
* [ ] 能用 GDB 调试一个 segfault 程序
* [ ] 理解为什么大型项目要用分支策略而不是所有人改 main 分支
