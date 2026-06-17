---
icon: diagram-project
---

# 数据结构与算法

## 为什么视觉组要学数据结构与算法？

视觉算法每秒要处理几十甚至上百帧图像，每帧只有几毫秒的处理时间。选对数据结构，代码可能快 10 倍；选错数据结构，再好的算法思路也跑不动。

几个实际场景：

* **图像帧缓存**：用环形队列，入队出队 O(1)
* **目标追踪匹配**：用匈牙利算法，比暴力遍历快得多
* **路径规划**：用优先队列 + Dijkstra/A\*，比 BFS 快几个量级
* **KD 树**：点云最近邻搜索，比线性搜索快几个量级

## 核心知识点

### 基础数据结构

* **数组 / 动态数组**（`std::vector`）：随机访问 O(1)
* **链表**（`std::list`）：插入删除 O(1)，随机访问 O(n)
* **栈**：后进先出（LIFO），用于函数调用、表达式求值
* **队列**：先进先出（FIFO），用于 BFS、帧缓存
* **哈希表**（`std::unordered_map`）：查找/插入/删除平均 O(1)
* **二叉搜索树 / 红黑树**（`std::map`）：查找/插入/删除 O(log n)
* **优先队列 / 堆**（`std::priority_queue`）：获取最值 O(1)，插入 O(log n)

### 常见算法

* **排序**：快排、归并排序、堆排序
* **查找**：二分查找、哈希查找
* **图算法**：BFS、DFS、Dijkstra、A\*（路径规划必备）
* **动态规划**：最优子结构问题的通用解法
* **搜索与回溯**：组合优化问题

### 复杂度分析

* **时间复杂度**：O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ)
* **空间复杂度**：算法额外消耗的内存

理解复杂度，你才能判断"我的算法在 90fps 下能不能跑完"。

## 推荐学习资源

* **OI Wiki**：[https://oi-wiki.org/](https://oi-wiki.org/) — 免费开放的编程竞赛知识库，覆盖所有经典数据结构与算法
* **The Algorithms**（GitHub）：[https://github.com/TheAlgorithms](https://github.com/TheAlgorithms) — 多语言数据结构实现代码
* **LeetCode**：[https://leetcode.cn/](https://leetcode.cn/) — 刷题平台，建议刷 20-30 道基础题入门
* **洛谷**：[https://www.luogu.com.cn/](https://www.luogu.com.cn/) — 国内 OJ 平台
* **经典教材**：
  * 《算法（第四版）》（Sedgewick）— 入门友好
  * 《数据结构与算法分析：C 语言描述》— 结合代码
  * 《算法导论》（CLRS）— 理论深入，选学

## Checkpoint

* [ ] 能说出数组和链表各自的优缺点
* [ ] 理解时间复杂度的大 O 表示法
* [ ] 能用 C++ STL 的 `vector`、`map`、`unordered_map`、`priority_queue`
* [ ] 能手写二分查找
* [ ] 了解 BFS 和 DFS 的区别，知道什么场景用哪个
