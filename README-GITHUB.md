# 在线考试监考系统 - 部署指南

## 🎯 一、获取永久网址（GitHub Pages - 免费 + 永久）

### 步骤 1：创建 GitHub 账号
打开 https://github.com → 点击 "Sign up" 注册账号（免费）

### 步骤 2：创建代码仓库
1. 登录后，点击右上角 **"+"** → **"New repository"**
2. 填写：
   - **Repository name**：`exam-system`（或任意名称）
   - 选择 **Public**（GitHub Pages 必须公开仓库）
   - 勾选 **"Add a README file"**
3. 点击 **"Create repository"**

### 步骤 3：上传代码
在新仓库页面：
1. 点击 **"uploading an existing file"**
2. 将 `exam-system` 文件夹中的以下文件拖入上传区：
   - `index.html`
   - `app.js`（如果有）
   - `package.json`
   - `.github/workflows/build-and-release.yml`
   - `server.js`（仅用于本地运行，GitHub Pages 不需要）
3. 点击 **"Commit changes"**

### 步骤 4：启用 GitHub Pages（自动部署）
1. 进入仓库 → **Settings** → 左侧 **"Pages"**
2. **Source** 选择：**Deploy from a branch**
3. **Branch** 选择：**main**（或 master），`/(root)`，点击 **Save**
4. 等待 1-2 分钟，页面顶部会显示：
   > Your site is live at `https://你的用户名.github.io/exam-system/`

### ✅ 完成！
把这个地址发给考生，他们就能在任何网络下访问了！

---

## 🔧 二、生成离线 exe 文件（自动构建）

当代码推送到 GitHub 后，Actions 会自动运行：

1. 进入仓库 → **Actions** 页面
2. 看到 "构建与发布" 工作流正在运行
3. 等待约 **3-5 分钟**（首次构建）
4. 构建完成后：
   - 点击工作流运行记录
   - 找到 **"exam-system-portable"** 的 artifact
   - 点击下载 `exam-system-portable.zip`
5. 解压 ZIP，双击 `exam-system.exe` 即可运行（无需安装 Node.js）

---

## 📋 三、离线使用流程

### 方式 A：通过网址（推荐）

1. **管理员**：用自己的电脑访问 `https://你的用户名.github.io/exam-system/`
   - 登录 admin / admin123
   - 创建题库、考生、考试
   - 点击 **"📤 导出考试数据"** 下载 JSON 文件
   - 把 JSON 文件发给考生

2. **考生**：收到 JSON 文件后
   - 访问同一网址
   - 点击 **"📥 导入考试数据"** 选择 JSON 文件
   - 输入账号密码登录考试

### 方式 B：通过 exe 文件

1. **管理员**：下载 exe 压缩包，解压运行
   - 设置题库、导出 JSON
2. **考生**：同样下载 exe，解压运行
   - 导入 JSON，登录考试

---

## 📊 四、账号说明

| 角色 | 账号 | 密码 | 说明 |
|------|------|------|------|
| 管理员 | admin | admin123 | 创建题库、管理考试 |
| 考生 | student001 | 123456 | 参加考试 |
| 考生 | student002 | 123456 | 参加考试 |

---

## 🆘 五、常见问题

**Q: GitHub Pages 部署失败怎么办？**
A: 检查仓库是否为 Public（公开），确认 index.html 在仓库根目录。

**Q: 考生没有 GitHub 怎么访问？**
A: 用永久网址，考生只需在浏览器打开链接，无需账号。

**Q: 想修改题库怎么办？**
A: 管理员登录后修改，点击"导出数据"重新分发 JSON 文件。

**Q: exe 文件下载失败？**
A: GitHub Actions 运行需要几分钟，稍后再试。

**Q: 能让考生数据同步吗？**
A: 目前为离线模式，管理员导出 JSON → 考生导入 JSON 即可共享数据。

---

## 📁 文件说明

| 文件 | 用途 |
|------|------|
| `index.html` | 主程序（GitHub Pages 部署用） |
| `server.js` | 本地服务器（双击启动时用） |
| `启动考试系统.bat` | Windows 一键启动脚本 |
| `.github/workflows/build-and-release.yml` | 自动构建 exe + 部署 Pages |
| `package.json` | Node.js 配置文件 |
