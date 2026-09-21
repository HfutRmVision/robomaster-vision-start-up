---
description: Python 入门指南
icon: python
---

# Python 入门（选学）

> **本页是选学内容。** 视觉组新生路线直接从 C++ 开始，不要求先学 Python。当你进入深度学习阶段（需要训练模型、处理数据集）时，再回来按本页学习。

## 为什么视觉组要学 Python

Python 在 RoboMaster 视觉组的定位是**快速验证工具**——语法简洁、库丰富，能在短时间内搭建出算法原型。OpenCV、PyTorch 等核心库都有完善的 Python 接口。

典型工作流：先用 Python 跑通 demo 验证方案可行性，再把核心逻辑用 C++ 重写以提升性能。

> "人生苦短，我用 Python。"

## Python 的特点

* **语法简洁**：几行代码就能完成复杂操作，代码可读性接近伪代码
* **生态丰富**：NumPy（数值计算）、OpenCV（图像处理）、PyTorch（深度学习）、ROS 2（机器人通信）都有完善的 Python 接口
* **开发效率高**：不需要编译，改完直接跑，适合快速迭代
* **运行速度慢**：解释型语言，比 C++ 慢一个数量级。这是用 C++ 重写核心逻辑的原因

## 在 RoboMaster 中的应用

* **算法原型验证**：用 Python + OpenCV 快速实现颜色分割、模板匹配等传统算法
* **深度学习训练**：PyTorch 训练 YOLO 等目标检测模型
* **数据处理**：NumPy 处理图像矩阵数据
* **ROS 2 节点**：用 `rclpy` 编写 ROS 2 节点
* **工具脚本**：批量处理数据集、自动化测试等

## 学习路线

1. **基础语法**（1-2 周）：变量、数据类型、控制流、函数、列表/字典/元组
2. **面向对象**（3-5 天）：类、继承、封装
3. **常用库**（1 周）：NumPy、Matplotlib
4. **OpenCV-Python**（1 周）：图像读写、预处理、特征提取
5. **实战**：写一个读取摄像头并做颜色分割的小程序

## 推荐学习资源

**在线教程**

* 菜鸟教程：[https://www.runoob.com/python3/python3-tutorial.html](https://www.runoob.com/python3/python3-tutorial.html) — 大量实例，适合零基础
* 廖雪峰 Python 教程：[https://www.liaoxuefeng.com/wiki/1016959663602400](https://www.liaoxuefeng.com/wiki/1016959663602400) — 系统全面

**书籍**

* 《Python 编程：从入门到实践（第 2 版）》— 前半部分基础语法，后半部分项目实战，零基础首选

**视频课程**

* B 站黑马程序员 Python 入门教程（BV 号：BV1qW4y1a7fU）
* B 站搜索："Python 从入门到实践"

## 环境搭建

推荐使用 Anaconda 或 Miniconda 管理 Python 环境：

```bash
# 创建虚拟环境
conda create -n rm_vision python=3.10
conda activate rm_vision

# 安装常用库
pip install numpy opencv-python matplotlib
pip install torch torchvision  # PyTorch
```

> 详见 [Conda 环境管理](../ai/shen-du-xue-xi/conda.md) 章节

## Checkpoint

* [ ] 能用 Python 读写文件、处理字符串
* [ ] 能用 NumPy 创建数组、做矩阵运算
* [ ] 能用 OpenCV-Python 读取图片并显示
* [ ] 能写一个简单的函数并理解参数传递
* [ ] 理解列表推导式和文件操作
