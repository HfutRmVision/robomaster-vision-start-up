---
icon: robot-astromech
---

# ROS 2 机器人操作系统

## 为什么我们需要 ROS 2？

在 RoboMaster 视觉系统中，往往涉及多个传感器（如相机、IMU）、多个处理模块（如图像处理、目标识别、定位预测），以及与底层控制模块的数据交互。为了让这些模块解耦且协同运行，我们使用 **ROS 2（Robot Operating System 2）**，它是现代机器人软件开发的标准通信中间件，具有以下优点：

* **模块化架构**：各个功能单元作为节点（Node）独立运行，方便复用、替换和并行开发
* **强大的通信机制**：支持发布/订阅、服务/响应、动作等通信模型，适用于传感器数据传输、状态同步与控制指令传递
* **良好的跨平台性能**：相比 ROS 1，ROS 2 更加适合嵌入式设备、RTOS 和多线程程序
* **社区与生态活跃**：提供众多可用组件，如导航、感知、仿真工具等

在 RoboMaster 项目中，ROS 2 是机器人软件开发的行业标准之一。并非所有战队都必须使用 ROS 2（有些队伍用纯 C++ + 自定义通信），但如果你的项目模块多、需要跨设备协作，ROS 2 是一个成熟可靠的选择。

## 安装 ROS 2

在动手写节点之前，首先需要安装 ROS 2。推荐安装 **ROS 2 Humble**（LTS 长期支持版）：

* **官方安装教程（英文）**：[https://docs.ros.org/en/humble/Installation.html](https://docs.ros.org/en/humble/Installation.html)
* **中文安装教程**（鱼香 ROS 一键安装）：[https://fishros.org.cn/docs/ros2/install.html](https://fishros.org.cn/docs/ros2/install.html)

安装完成后，验证是否成功：

```bash
ros2 --help          # 能看到帮助信息说明安装成功
ros2 topic list      # 列出当前所有话题（刚装好时应该只有 /parameter_events 和 /rosout）
```

> 如果你用的是 WSL2 或虚拟机，确保安装的是 Ubuntu 22.04（ROS 2 Humble 的推荐系统）。

## 目标：能够独立编写 ROS 2 节点和程序

需掌握如何使用 ROS 2 编写节点，实现模块之间的通信。基本技能包括：

### 1. 创建功能包（package）

```bash
# C++ 版本
ros2 pkg create --build-type ament_cmake my_vision_node

# Python 版本
ros2 pkg create --build-type ament_python my_vision_node
```

### 2. 编写节点程序

**C++ 版本（`my_node.cpp`）：**

```cpp
#include <rclcpp/rclcpp.hpp>

class MyNode : public rclcpp::Node {
public:
    MyNode() : Node("my_node") {
        timer_ = this->create_wall_timer(
            std::chrono::seconds(1),
            std::bind(&MyNode::timer_callback, this));
    }
private:
    void timer_callback() {
        RCLCPP_INFO(this->get_logger(), "Hello ROS 2!");
    }
    rclcpp::TimerBase::SharedPtr timer_;
};

int main(int argc, char** argv) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<MyNode>());
    rclcpp::shutdown();
    return 0;
}
```

**Python 版本（`my_node.py`）：**

```python
import rclpy
from rclpy.node import Node

class MyNode(Node):
    def __init__(self):
        super().__init__('my_node')
        self.timer = self.create_timer(1.0, self.timer_callback)

    def timer_callback(self):
        self.get_logger().info('Hello ROS 2!')

def main():
    rclpy.init()
    node = MyNode()
    rclpy.spin(node)
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### 3. 通信模型

ROS 2 有三种核心通信模型：

| 通信模型 | 特点 | 适用场景 |
| --- | --- | --- |
| **Topic（话题）** | 发布/订阅，异步 | 图像流、传感器数据 |
| **Service（服务）** | 请求/响应，同步 | 触发某个动作（如开始录制） |
| **Action（动作）** | 请求/响应 + 反馈，异步 | 长时间任务（如导航到目标点） |

### 4. 常用命令

```bash
# 查看所有节点
ros2 node list

# 查看所有话题
ros2 topic list

# 查看话题数据
ros2 topic echo /image_raw

# 查看话题信息
ros2 topic info /image_raw

# 运行节点
ros2 run my_vision_node my_node

# 用 launch 文件启动多个节点
ros2 launch my_vision_node vision.launch.py
```

## 可视化调试工具

### rviz2

ROS 2 自带的可视化工具，可以显示图像、点云、TF 坐标树等：

```bash
rviz2
```

### Foxglove Studio

第三方可视化工具，支持 ROS 2 WebSocket 连接，界面友好：

1. 安装 Foxglove Studio
2. 启动 rosbridge：
   ```bash
   ros2 launch rosbridge_server rosbridge_websocket_launch.xml
   ```
3. 打开 Foxglove Studio，选择 "ROS 2 WebSocket" 连接
4. 订阅需要可视化的 topic，如 `/image_raw`、`/target_pose`、`/fire_command` 等
5. 拖入合适的 Widget（Image、3D Panel、Plot 等）进行实时观察

## 推荐学习资源

**官方文档**

* ROS 2 官方文档：[https://docs.ros.org/en/rolling/index.html](https://docs.ros.org/en/rolling/index.html)
* ROS 2 Tutorials（强烈推荐动手练习）：[https://docs.ros.org/en/rolling/Tutorials.html](https://docs.ros.org/en/rolling/Tutorials.html)

**中文资料**

* ROS 2 中文社区及入门教程：[https://fishros.org.cn/docs/ros2](https://fishros.org.cn/docs/ros2)
  （由国内 Fishbot 团队维护，内容完整易懂）

**视频课程**

* B 站【鱼香 ROS】动手学 ROS2（BV 号：BV1gr4y1Q7j5）
* Foxglove Studio 教程：[https://foxglove.dev/blog/](https://foxglove.dev/blog/)

## Checkpoint

* [ ] 能用 `ros2 pkg create` 创建一个功能包
* [ ] 能编写一个简单的 ROS 2 节点（C++ 或 Python）
* [ ] 能用 Topic 实现两个节点之间的消息传递
* [ ] 能用 `ros2 topic echo` 查看话题数据
* [ ] 能用 rviz2 可视化图像或点云数据
