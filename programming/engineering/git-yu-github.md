---
icon: git
---

# Git 与 GitHub

在 RoboMaster 项目开发中，视觉组成员往往需要多人协作、频繁修改代码并进行版本管理。**Git 与 GitHub** 是现代软件开发中最常用的**版本控制与协作工具**，对规范开发流程、提升团队效率至关重要。

## 什么是 Git？

**Git** 是一个开源的分布式版本控制系统，用于**跟踪文件的变化历史、管理代码版本**。

**Git 的核心功能：**

* 保存每次代码修改的"快照"
* 随时回退到旧版本
* 支持多人协作开发，自动合并改动
* 管理不同开发分支（如主线 `main`、实验 `dev`）

**常见 Git 操作：**

| 操作       | 命令示例                  |
| -------- | --------------------- |
| 初始化仓库    | `git init`            |
| 克隆远程项目   | `git clone <仓库地址>`    |
| 查看状态     | `git status`          |
| 添加修改到暂存区 | `git add .`           |
| 提交修改     | `git commit -m "说明"`  |
| 推送到远程仓库  | `git push`            |
| 拉取最新代码   | `git pull`            |
| 创建/切换分支  | `git checkout -b dev` |
| 合并分支     | `git merge dev`       |



<figure><img src="../.gitbook/assets/IMG_20260922_182223 (1).jpg" alt="" width="375"><figcaption></figcaption></figure>

## 什么是 GitHub？

**GitHub** 是基于 Git 的**在线代码托管平台**，提供远程仓库、协作开发、代码审查、Issue 管理等功能。你可以将代码推送到 GitHub 实现云端备份和团队共享。

## Git 与 GitHub 的关系

| Git         | GitHub           |
| ----------- | ---------------- |
| 本地工具        | 在线平台             |
| 管理本地代码版本    | 托管远程仓库，实现协作与共享   |
| 无需联网也能使用    | 需要联网登录账户         |
| 需搭配使用远程仓库功能 | 是 Git 最流行的远程仓库平台 |

你可以将 Git 看作本地"保存记录"的工具，而 GitHub 是"云端共享与协作"的空间。

## 推荐学习资源

**入门教程**

* Git 官方文档：[https://git-scm.com/](https://git-scm.com/)
* 廖雪峰的 Git 教程：[https://www.liaoxuefeng.com/wiki/896043488029600](https://www.liaoxuefeng.com/wiki/896043488029600) 中文讲解，简单易懂，从零开始学 Git
* 菜鸟教程：[https://www.runoob.com/git/git-tutorial.html](https://www.runoob.com/git/git-tutorial.html)
* B 站搜索 "Git 和 GitHub 入门教程"

**工具推荐**

* GitHub Desktop：可视化 Git 工具，适合初学者
* VS Code Git 插件：集成 Git 操作、可视化合并冲突
* Sourcetree：图形化界面辅助管理 Git 仓库

## Checkpoint

* [ ] 能用 `git clone` 克隆一个远程仓库
* [ ] 能完成 `add → commit → push` 的完整流程
* [ ] 能创建分支并合并回主分支
* [ ] 理解 `git pull` 和 `git fetch` 的区别
* [ ] 能用 `git log` 查看提交历史
