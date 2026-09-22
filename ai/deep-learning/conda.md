---
icon: c
---

# Conda 环境管理

## 什么是 Conda？

**Conda** 是一个**跨平台的包管理和环境管理工具**，支持 Python、C++ 等多种语言的依赖管理。它最初由 Anaconda 公司推出，常用于科学计算、数据分析和人工智能项目的环境构建。

Conda 能帮助开发者轻松解决"包冲突""依赖混乱"等问题，是部署 RoboMaster 视觉模块和深度学习模型时非常重要的工具。

## Conda 的主要功能

### 1. 虚拟环境管理

通过 Conda 可以为不同项目创建独立的 Python 环境，互不干扰。每个环境可指定 Python 版本，避免系统环境混乱。

常用命令：

```bash
# 创建环境
conda create -n rm_vision python=3.10

# 激活环境
conda activate rm_vision

# 退出环境
conda deactivate

# 删除环境
conda remove -n rm_vision --all

# 查看所有环境
conda env list
```

### 2. 包管理与安装依赖

Conda 可以安装、更新、卸载各种科学计算与机器学习相关库（如 OpenCV、PyTorch、Numpy 等），自动处理依赖关系。

```bash
# 安装包
conda install opencv
conda install pytorch torchvision torchaudio -c pytorch

# 也可以用 pip（推荐先尝试 conda，conda 没有再用 pip）
pip install some-package

# 查看已安装的包
conda list
```

## Conda vs pip vs venv

| 工具 | 环境管理 | 包管理 | 适合场景 |
| --- | --- | --- | --- |
| Conda | ✅ | ✅ | 科学计算、深度学习（推荐） |
| pip | ❌ | ✅ | 纯 Python 包安装 |
| venv | ✅ | ❌（配合 pip） | 轻量级 Python 虚拟环境 |

> 建议：深度学习项目用 Conda，普通 Python 项目用 venv + pip。

## 安装 Conda

推荐安装 **Miniconda**（体积小，只包含 Conda 和 Python）：

* Miniconda 下载地址：[https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
* 安装后运行 `conda --version` 验证

## 推荐学习资源

* **Conda 官方文档**：[https://docs.conda.io/](https://docs.conda.io/)
* B 站搜索 "conda 虚拟环境配置"
* 菜鸟教程 Anaconda 入门：[https://www.runoob.com/python-qt/anaconda-tutorial.html](https://www.runoob.com/python-qt/anaconda-tutorial.html)

## Checkpoint

* [ ] 能用 Conda 创建、激活、删除虚拟环境
* [ ] 能在指定环境中安装 OpenCV 和 PyTorch
* [ ] 理解为什么不同项目需要不同的虚拟环境
