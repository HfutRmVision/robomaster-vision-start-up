---
icon: camera-retro
---

# 相机基本参数

在 RoboMaster 视觉系统中，相机是机器人"看"赛场的唯一窗口。理解相机的基本参数，是后续标定、坐标变换、目标测距等所有视觉任务的前提。

## 相机的成像原理

相机通过镜头将外部光线汇聚到图像传感器（CMOS/CCD）上，传感器将光信号转换为电信号，最终生成数字图像。整个过程可以简化为一个小孔成像模型：

1. 外部光线通过镜头（透镜组）进入相机
2. 光线汇聚到图像传感器上
3. 传感器将光信号转化为像素阵列

其中，镜头负责"聚光"，传感器负责"光电转换"，两者共同决定了成像质量。

## 关键参数

### 1. 焦距（Focal Length）

焦距是镜头光学中心到传感器的距离，单位为毫米（mm）。

* **短焦距**（如 6mm）：视野大（广角），但远处物体小
* **长焦距**（如 35mm）：视野窄（长焦），但远处物体大

在 RoboMaster 中，步兵自瞄通常用 6-8mm 镜头（需要宽视野覆盖赛场），能量机关击打可能用更长焦距镜头（需要看清远处目标）。

### 2. 视野角（Field of View, FOV）

视野角决定了相机能"看到"多宽的范围，分为水平 FOV 和垂直 FOV。FOV 与焦距和传感器尺寸有关：

$$
\text{FOV} = 2 \arctan\left(\frac{\text{传感器尺寸}}{2f}\right)
$$

其中 $f$ 为焦距。焦距越短，FOV 越大。

### 3. 分辨率与帧率

* **分辨率**：图像的像素数量，如 1280×1024。分辨率越高，细节越清晰，但数据量越大、处理越慢
* **帧率（FPS）**：每秒采集的图像帧数。RoboMaster 视觉通常要求 **90 FPS 以上**，才能保证自瞄的实时性

### 4. 曝光与增益

* **曝光时间（Shutter）**：传感器每次采集光线的时间。曝光时间越长，图像越亮，但高速运动物体会模糊。比赛中通常用**短曝光**（如 1-3ms）来"冻结"运动目标
* **增益（Gain）**：放大传感器信号的强度。增益越高画面越亮，但噪声也越多。一般在调好曝光后尽量用低增益

### 5. 传感器尺寸

传感器物理尺寸（如 1/2.8 英寸、2/3 英寸）。尺寸越大，单位像素感光面积越大，低光环境下表现更好。传感器尺寸也影响实际 FOV。

## 相机内参与外参

### 内参（Intrinsic Parameters）

内参描述相机自身的光学属性，与相机位置无关，主要包括：

* **焦距** $f_x, f_y$（像素单位）
* **主点坐标** $c_x, c_y$（光轴与图像平面的交点，通常接近图像中心）
* **畸变系数**（Distortion Coefficients）：描述镜头造成的图像变形

内参矩阵通常表示为：

$$
K = \begin{bmatrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{bmatrix}
$$

### 畸变

实际镜头并非理想的小孔模型，会产生两种主要畸变：

* **径向畸变**：光线弯曲导致图像边缘呈桶形或枕形变形
* **切向畸变**：镜头组装偏心导致的变形

畸变可以通过标定获取畸变系数后，用 OpenCV 的 `undistort()` 函数校正。

### 外参（Extrinsic Parameters）

外参描述相机在世界坐标系中的位置和朝向，包括：

* **旋转矩阵** $R$（3×3）
* **平移向量** $t$（3×1）

外参会随相机移动而变化，需要通过标定板或已知参照物确定。

## 相机标定

相机标定就是通过拍摄已知图案（通常是棋盘格），求解内参和畸变系数的过程。

### 标定步骤（使用 OpenCV）

1. 打印棋盘格标定板（如 9×6 内角点）
2. 从不同角度拍摄 15-20 张棋盘格照片
3. 使用 `cv2.findChessboardCorners()` 检测角点
4. 使用 `cv2.calibrateCamera()` 求解内参和畸变系数
5. 使用 `cv2.undistort()` 校正图像

```python
import cv2
import numpy as np
import glob

# 棋盘格规格
chessboard_size = (9, 6)
square_size = 25.0  # mm

# 准备物体点坐标
objp = np.zeros((chessboard_size[0] * chessboard_size[1], 3), np.float32)
objp[:, :2] = np.mgrid[0:chessboard_size[0], 0:chessboard_size[1]].T.reshape(-1, 2)
objp *= square_size

objpoints = []  # 3D 点
imgpoints = []  # 2D 点

for fname in glob.glob('calib_images/*.jpg'):
    img = cv2.imread(fname)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    ret, corners = cv2.findChessboardCorners(gray, chessboard_size, None)
    if ret:
        objpoints.append(objp)
        corners2 = cv2.cornerSubPix(gray, corners, (11, 11), (-1, -1),
            (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 30, 0.001))
        imgpoints.append(corners2)

# 标定
ret, mtx, dist, rvecs, tvecs = cv2.calibrateCamera(
    objpoints, imgpoints, gray.shape[::-1], None, None)

print("内参矩阵:\n", mtx)
print("畸变系数:\n", dist)
```

## RoboMaster 常见相机

| 相机型号 | 类型 | 特点 |
| --- | --- | --- |
| 迈德威视 | 工业相机 | 高帧率、全局快门、支持外部触发 |
| 海康威视 | 工业相机 | 帧率高、SDK 完善 |
| ZED | 双目深度相机 | 可直接输出深度图，适合 SLAM |
| OpenMV | 嵌入式视觉模块 | 集成 MCU，适合简单任务（颜色识别等） |

> 全局快门（Global Shutter）vs 卷帘快门（Rolling Shutter）：全局快门同时曝光所有像素，适合拍摄高速运动目标；卷帘快门逐行曝光，高速运动目标会变形。RoboMaster 比赛中**必须使用全局快门相机**。

## 学习资源

* OpenCV 官方相机标定教程：[Camera Calibration](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html)
* B 站搜索："OpenCV 相机标定"
* 《学习 OpenCV 4》——第 18 章详细讲解了相机模型与标定

## Checkpoint

学完本节后，试试能否完成以下任务：

* [ ] 说出焦距、FOV、帧率各影响什么
* [ ] 解释径向畸变和切向畸变的区别
* [ ] 用 OpenCV 完成一次完整的棋盘格标定
* [ ] 理解内参矩阵中每个参数的物理含义
