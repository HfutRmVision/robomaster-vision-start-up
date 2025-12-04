# Robomaster Vision Start-Up

本项目是一个纯 **HTML/CSS/JavaScript** 静态网页示例。由于浏览器直接通过 `file://` 协议打开会导致超链接失效或出现跨域问题，因此推荐使用本地服务器进行启动与调试。  

本文档介绍两种本地启动方式：  

---

## 🚀 方法一：使用 VS Code + Live Server 插件（推荐）

1. **安装 VS Code**  
   - 前往 [Visual Studio Code 官网](https://code.visualstudio.com/) 下载并安装。
   - 详细安装流程可参考 [VSCode保姆级安装教程](https://zhuanlan.zhihu.com/p/1891619024938451892)。

2. **安装 Live Server 插件**  
   - 打开 VS Code  
   - 点击左侧扩展（Extensions）面板  
   - 搜索 `Live Server` 并安装  

3. **启动本地服务器**  
   - 在 VS Code 中打开项目文件夹  
   - 右键 `index.html`  
   - 选择 **“Open with Live Server”**  
   - 浏览器将自动打开 `http://127.0.0.1:5500/index.html`  

👉 此方式支持 **热加载**，保存文件后浏览器会自动刷新，非常适合开发调试。  

---

## 🚀 方法二：使用 Python 内置 HTTP 服务器

通过 **Python 3.x** 可直接在终端启动内置服务器。  

1. 安装 python：
   - 前往 [Python 官网下载界面](https://www.python.org/downloads/) 下载并安装，可选择任意 **Python 3.x** 版本安装。
   - 将安装好的 python 添加至环境变量。
   - 详细流程可参考 [手把手教你安装Python，2024最详细的安装教程来了（附安装包 建议收藏）](https://zhuanlan.zhihu.com/p/28168900682)。

2. 终端中进入项目目录：

   ```bash
   cd path/to/robomaster-vision-start-up
   ```

3. 启动服务器：

   ```bash
   python -m http.server 8080
   ```

4. 在浏览器中访问：

   ```bash
   http://localhost:8080/index.html
   ```

👉 此方式无需额外插件，轻量快捷。

---

## 📌 注意事项

- 请勿直接双击 `index.html` 打开，否则可能出现 **超链接跳转失效** 或 **跨域错误**。
- 推荐开发时使用 **VS Code + Live Server**，部署或临时查看可用 **Python 内置服务器**。
