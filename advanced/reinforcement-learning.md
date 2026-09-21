---
icon: head-side-gear
---

# 强化学习

强化学习（Reinforcement Learning, RL）是人工智能的三大核心分支之一。与监督学习"给数据学规律"不同，强化学习通过"试错"来学习最优决策策略——智能体在环境中采取动作，获得奖励或惩罚，逐步优化自己的行为。

## 基本概念

强化学习的核心框架是**智能体-环境交互**：

```
        动作 a
智能体 ─────────→ 环境
  ↑                 │
  │    状态 s, 奖励 r
  └─────────────────┘
```

* **状态（State, s）**：环境的当前描述，如机器人的位置、速度、周围障碍物分布
* **动作（Action, a）**：智能体可以选择执行的操作，如前进、转向、射击
* **奖励（Reward, r）**：环境对动作的反馈，如命中敌方得正奖励、撞墙得负奖励
* **策略（Policy, π）**：智能体根据状态选择动作的规则
* **价值函数（Value Function）**：衡量某个状态下长期累积奖励的期望值

强化学习的目标是找到一个最优策略 π\*，使得长期累积奖励最大化。

## 与监督学习的区别

| 对比项 | 监督学习 | 强化学习 |
| --- | --- | --- |
| 数据 | 标注好的输入-输出对 | 无标注数据，通过交互获取经验 |
| 反馈 | 每个样本都有正确答案 | 奖励可能有延迟（下了好棋很久才赢） |
| 目标 | 拟合输入到输出的映射 | 最大化长期累积奖励 |
| 探索 | 不需要探索 | 需要平衡探索（试新动作）与利用（用已知好动作） |

## 主要方法分类

### 1. 基于价值（Value-Based）

学习价值函数，间接推导策略。代表算法：

* **Q-Learning**：经典离策略算法，学习动作价值函数 Q(s, a)
* **DQN（Deep Q-Network）**：用神经网络逼近 Q 函数，DeepMind 提出，在 Atari 游戏上达到人类水平
* **Dueling DQN、Double DQN**：DQN 的改进版本

### 2. 基于策略（Policy-Based）

直接学习策略函数 π(a|s)，输出动作的概率分布。代表算法：

* **REINFORCE**：最基础的策略梯度算法
* **TRPO、PPO**：策略梯度的改进版本，训练更稳定

### 3. Actor-Critic

结合价值函数和策略函数：Actor 负责选动作，Critic 负责评价动作好坏。代表算法：

* **A2C / A3C**：Advantage Actor-Critic
* **SAC（Soft Actor-Critic）**：引入熵正则化，鼓励探索
* **DDPG、TD3**：适用于连续动作空间

## 深度强化学习

深度强化学习（Deep RL）将深度学习与强化学习结合，用神经网络来逼近价值函数或策略函数，能够处理高维状态空间（如图像输入）。

**典型代表**：

* DQN：用 CNN 从图像中提取特征，逼近 Q 函数
* AlphaGo / AlphaZero：结合 MCTS（蒙特卡洛树搜索）与深度强化学习，击败人类围棋冠军
* PPO：OpenAI 的默认算法，在多个基准任务上表现稳定

## 在 RoboMaster 中的潜在应用

> 目前强化学习在 RoboMaster 实战中应用还不广泛，但随着比赛对自主性要求的提高，其潜力正在被探索。

### 1. 自动步兵导航与决策

* **场景**：自动步兵在赛场上自主选择移动路线、交战时机
* **优势**：相比规则硬编码，RL 可以学会更灵活的策略
* **挑战**：训练需要仿真环境（如 Isaac Gym），sim-to-real 迁移困难

### 2. 自瞄策略优化

* **场景**：面对敌方的不同运动模式（直线、小陀螺、变向），自适应选择瞄准策略
* **优势**：可以学会应对传统算法难以覆盖的复杂运动模式

### 3. 多智能体协作

* **场景**：多个自动机器人协同作战
* **方向**：多智能体强化学习（MARL），如 MAPPO 算法

### 4. 仿真对抗训练

* **场景**：在仿真环境中训练 RL 策略，用于赛前策略验证
* **工具**：NVIDIA Isaac Sim / Isaac Gym、Webots、Gazebo

## 挑战与局限

在 RoboMaster 中应用 RL 面临的主要挑战：

* **Sim-to-Real Gap**：仿真环境与真实赛场的差异（摩擦力、光照、传感器噪声等）导致策略迁移困难
* **训练效率**：RL 需要大量交互数据，真实环境训练成本高且危险
* **安全性**：训练初期的随机策略可能导致机器人损坏
* **可解释性**：RL 策略是黑盒，出了问题难以调试

## 推荐学习资源

**入门资料**

* 《强化学习导论》（Reinforcement Learning: An Introduction, Sutton & Barto）——RL 圣经，理论扎实
* OpenAI Spinning Up：[https://spinningup.openai.com/](https://spinningup.openai.com/) ——深度 RL 入门教程，含完整代码
* 李宏毅强化学习课程（B 站搜索："李宏毅 强化学习"）

**实践平台**

* Gymnasium（原 OpenAI Gym）：[https://gymnasium.farama.org/](https://gymnasium.farama.org/) ——标准 RL 训练环境
* Stable Baselines3：[https://stable-baselines3.readthedocs.io/](https://stable-baselines3.readthedocs.io/) ——封装好的 RL 算法库
* NVIDIA Isaac Gym：GPU 加速的机器人仿真环境

**RoboMaster 相关**

* RMUC 仿真赛（官方提供的仿真平台）
* RoboMaster 论坛中的 RL 相关开源项目

## Checkpoint

* [ ] 用自己的话解释"探索与利用"的矛盾
* [ ] 说出 Q-Learning 和策略梯度方法的核心区别
* [ ] 思考：为什么 RL 在 RoboMaster 中的实际应用比监督学习少？
* [ ] 了解 Sim-to-Real Gap 是什么，以及为什么它是 RL 落地的主要障碍
