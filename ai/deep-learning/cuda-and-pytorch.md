---
icon: fire
---

# CUDA 与 PyTorch

## CUDA：让程序"跑在显卡上"的加速引擎

### 什么是 CUDA？

**CUDA（Compute Unified Device Architecture）** 是 NVIDIA 提供的**通用 GPU 并行计算平台**。它允许开发者用 C/C++、Python 等语言，**直接调用显卡资源进行大规模并行计算**。

### 为什么要用 CUDA？

* **加速深度学习训练**：大多数深度学习模型参数众多，训练过程计算量极大。借助 CUDA 可以让神经网络在显卡上运行，速度提升数十倍
* **支持主流深度学习框架**：如 PyTorch、TensorFlow 都可以自动调用 CUDA 来实现 GPU 加速

### 注意事项

* CUDA 只能在 **NVIDIA 显卡** 上运行
* 使用 CUDA 需要配套安装 **NVIDIA 驱动 + CUDA Toolkit + cuDNN**
* PyTorch 等框架通常提供**预编译好的 CUDA 版本**，建议通过 `conda` 安装对应版本以避免配置问题

### 验证 CUDA 是否可用

```python
import torch
print(torch.cuda.is_available())       # True 表示 CUDA 可用
print(torch.cuda.get_device_name(0))    # 打印 GPU 名称
```

## PyTorch：深度学习的强大框架

### 什么是 PyTorch？

**PyTorch** 是由 Meta AI（原 Facebook AI 研究院 FAIR）开发的**开源深度学习框架**，特点：

* 使用**动态图机制**，调试灵活，语法贴近 Python
* 支持**自动求导**，适合研究与原型开发
* 社区活跃，文档齐全，支持大多数深度学习任务
* 与 **CUDA 深度集成**，支持 GPU 加速

### PyTorch 基础用法

```python
import torch
import torch.nn as nn
import torch.optim as optim

# 创建张量并放到 GPU 上
inputs = torch.randn(32, 3, 224, 224).cuda()
labels = torch.randint(0, 2, (32,)).cuda()

# 定义简单模型
model = nn.Sequential(
    nn.Conv2d(3, 16, 3, padding=1),
    nn.ReLU(),
    nn.AdaptiveAvgPool2d(1),
    nn.Flatten(),
    nn.Linear(16, 2)
).cuda()

# 损失函数与优化器
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters())

# 训练一步
outputs = model(inputs)
loss = criterion(outputs, labels)
loss.backward()
optimizer.step()
```

### PyTorch 在 RoboMaster 中的应用

* **目标检测模型训练**：如训练 YOLO、Faster R-CNN 等识别装甲板
* **图像分类模型训练**：如识别能量机关符号类别
* **轨迹预测**：结合时间序列数据、RNN/Transformer 模型
* **部署到嵌入式设备**：模型训练后可转换为 ONNX 或 TensorRT 格式部署到 Jetson 平台

## 推荐学习资源

**官方文档**

* [PyTorch 官方教程](https://pytorch.org/tutorials/)（英文，质量最高，建议优先看）
* [PyTorch 中文文档](https://pytorch.apachecn.org/)（第三方社区翻译，可能更新不及时，遇到不一致以官方英文文档为准）

**学习视频**

* B 站搜索 "李沐 PyTorch"，推荐结合《动手学深度学习》一起学习

**实战项目平台**

* Kaggle / Colab（免费 GPU）
* HuggingFace、Ultralytics（YOLO 系列开源项目）
* Jetson Nano / Xavier：可部署轻量模型至边缘设备

## Checkpoint

* [ ] 能用 `conda` 安装指定 CUDA 版本的 PyTorch
* [ ] 能用 `torch.cuda.is_available()` 验证 GPU 是否可用
* [ ] 能用 PyTorch 定义一个简单的 CNN 模型并跑一次前向传播
* [ ] 理解 `.cuda()` 的作用——把张量/模型搬到 GPU 上
