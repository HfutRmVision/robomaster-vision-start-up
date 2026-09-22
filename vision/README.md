---
icon: head-side-goggles
---

# OpenCV 简介

## 什么是 OpenCV？

**OpenCV（Open Source Computer Vision Library）** 是一个开源的、跨平台的计算机视觉和图像处理库，由 Intel 于 2000 年发起，目前已广泛应用于学术研究、工业开发和机器人竞赛中。

在 RoboMaster 比赛中，OpenCV 是最常用的图像处理工具，配合 C++ 或 Python 编程语言，可以快速实现图像采集、处理、目标检测、特征提取等任务。

## OpenCV 的主要功能模块

* **图像处理**：滤波、边缘检测、形态学操作、直方图处理等
* **几何变换**：旋转、缩放、仿射变换、透视变换
* **特征提取与匹配**：SIFT、ORB、FAST 等
* **摄像头操作**：图像/视频读取、实时视频流处理
* **相机标定与三维重建**：畸变矫正、姿态估计、投影模型
* **GUI 工具**：图像显示、轨迹条调参、鼠标交互等

大部分传统的计算机视觉算法都可借助 OpenCV 提供的功能模块实现。

## OpenCV 的优点

* **开源免费**，文档丰富
* **跨平台支持**（Windows、Linux、macOS、Raspberry Pi）
* **接口语言多样**：支持 C++、Python、Java 等
* **高性能**：大量函数使用底层 SIMD 优化，可用于实时处理任务

## 推荐学习资源

**官方资料**

* [OpenCV 官方文档（英文）](https://docs.opencv.org/master/)
* [OpenCV-Python 教程](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html)

有能力的同学可以直接尝试阅读官方的 OpenCV 教程（英文）。

**中文学习资料**

* 《OpenCV 4 应用开发：入门进阶与工程化实践》— 适合初学者系统入门，含大量实例代码
* B 站搜索 "OpenCV 入门教程"
* 菜鸟教程：[https://www.runoob.com/opencv/opencv-tutorial.html](https://www.runoob.com/opencv/opencv-tutorial.html)
* CSDN 博客与知乎专栏：搜索 "OpenCV 入门"，社区资源丰富

## 建议学习路线

1. 学会使用摄像头读取图像并显示
2. 掌握图像预处理方法（灰度化、滤波、边缘检测）
3. 学会基本几何变换与图像操作
4. 进阶学习特征提取、轮廓分析、颜色分割

## Checkpoint

* [ ] 能用 OpenCV 读取图片并显示
* [ ] 能用 OpenCV 读取摄像头实时画面
* [ ] 能做灰度化、高斯滤波、Canny 边缘检测
* [ ] 能用 `cv2.findContours` 找到图像中的轮廓
* [ ] 能用颜色阈值（HSV 空间）分割特定颜色区域
