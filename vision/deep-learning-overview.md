---
icon: camera-polaroid
---

# 基于深度学习的计算机视觉概述

随着深度学习的发展，计算机视觉在图像识别、目标检测、分割等任务上取得了巨大突破。相较传统算法，深度学习方法具有**自动特征提取、适应性强、精度高**等优势，已成为 RoboMaster 等机器人平台上视觉识别任务的主流选择。

## 图像分类（Image Classification）

**目标**：判断整张图像属于哪一类别。

* **典型应用**：判断符号图像属于哪种能量机关符号；根据装甲板形状或颜色分类
* **代表模型**：
  * **LeNet**（最早的 CNN）
  * **VGG**（深层网络）
  * **ResNet**（引入残差连接，解决深层网络退化问题）

> 在 RoboMaster 比赛中，图像分类用于装甲板颜色识别、符号识别等任务。

## 目标检测（Object Detection）

**目标**：识别图像中**所有目标的位置与类别**，即输出边界框 + 类别标签。

* **典型应用**：检测图像中多个装甲板，获取其位置和所属机器人编号
* **主流方法**：
  * **两阶段检测器**：
    * R-CNN、Faster R-CNN（精度高但速度较慢）
  * **一阶段检测器**：
    * **YOLO（You Only Look Once）**：速度快、精度高，适合实时任务
    * SSD（Single Shot MultiBox Detector）

> RoboMaster 中多使用 YOLO 系列（如 YOLOv5、YOLOv8、YOLOv11）来实现装甲板检测。

## 图像分割（Image Segmentation）

**目标**：对图像进行像素级分类，每个像素都标注属于哪个类别或实例。

* **语义分割**：每个像素标注类别（如道路、天空、障碍物）
  * 代表模型：FCN、U-Net、DeepLab
* **实例分割**：不仅标注类别，还区分不同实例
  * 代表模型：Mask R-CNN

> 在 RoboMaster 中，图像分割可用于敌方区域分割、装甲板边界提取等任务。

## 目标跟踪（Object Tracking）

**目标**：在视频序列中持续追踪目标的位置。

* **应用场景**：跟踪装甲板，预测其运动轨迹以实现提前量打击
* **主流算法**：
  * **Siamese 网络**（如 SiamFC、SiamRPN）
  * **基于检测 + 关联的跟踪框架**（如 Deep SORT）

> 深度学习跟踪方法可结合检测结果与运动信息，提高稳定性与鲁棒性。详见 [目标追踪与预测](../tracking/tracking-and-prediction-intro.md) 章节。

## 动作识别与时序预测

**目标**：从图像序列中识别行为、预测未来状态。

* **代表方法**：
  * RNN / LSTM：处理时间序列
  * Transformer：建模长时间依赖，表现优于传统 RNN
  * 3D CNN：直接处理视频帧数据

> 可用于预测能量机关转动模式、敌方装甲板下一帧状态等高级任务。

## 推荐学习资源

**学习书籍**

* 《深度学习》（Ian Goodfellow）
* 《深度学习与计算机视觉实战》
* 《动手学深度学习》（李沐）

**视频教程**

* B 站搜索：
  * "计算机视觉基础教程"
  * "YOLOv5 实战"
  * "图像分类 / 跟踪 / 分割项目实战"

**实战平台**

* Kaggle（分类 / 检测 / 分割挑战）
* Ultralytics YOLO：[https://github.com/ultralytics/yolov5](https://github.com/ultralytics/yolov5)

## Checkpoint

* [ ] 说出图像分类和目标检测的区别
* [ ] 理解 YOLO 为什么适合 RoboMaster（速度快 + 精度够用）
* [ ] 了解语义分割和实例分割的区别
* [ ] 能用 YOLOv5/v8 跑一个简单的目标检测 demo
