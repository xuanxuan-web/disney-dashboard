# 迪士尼轨交到达客流数据看板（GitHub Pages 部署包 · 单文件版）

把「上海迪士尼轨交到达客流数据看板」打包成**一个自包含的 `index.html`**，上传到 GitHub 即可直接访问，图表完整、可交互。

## 包内容（只有 2 个文件）

```
disney-dashboard-github/
├── index.html      # 1,136,961 字节（约 1.08 MB），ECharts + 上海 16 区地图 + 全部数据均已内联
└── .nojekyll       # 空文件，关闭 Jekyll 处理，静态文件原样托管
```

**关键特性：`index.html` 对外零依赖。** 不加载任何 CSS/JS/图片/瓦片/瓦片地图，断网也能完整显示。已用无头浏览器实测：**11 个图表全部渲染、0 报错、0 失败请求、点击「2024 / 2025 / 对比」切换正常**。

## 部署步骤（三步）

### 1. 准备仓库
新建或打开一个 **Public** 仓库（例如 `Shanghai-Disney-Resort`）。

### 2. 上传文件到仓库根目录
**Add file → Upload files**，把本包里的 `index.html` 和 `.nojekyll` 拖进去，提交。

> 目录要求：`index.html` 必须在**仓库根目录**，不能放在子文件夹里。
> 若仓库里已有旧文件（如 `assets/`、`echarts.min.js`、`disney-dashboard-github/` 文件夹、`disney-dashboard.zip`），可以直接删掉，本包不需要它们。

### 3. 开启 GitHub Pages
**Settings → Pages → Build and deployment → Source** 选 **Deploy from a branch**，Branch 选 `main`、目录选 `/ (root)`，点 **Save**。
等待约 1–3 分钟（Actions 里 `pages build and deployment` 显示绿色对勾），访问：

```
https://<用户名>.github.io/<仓库名>/
```

## 上传完整性校验（很重要）

`index.html` 必须完整上传。GitHub 仓库文件列表里点击 `index.html` → 右上角 **Raw**，确认文件大小是 **1,136,961 字节（约 1.08 MB）**。

- 若明显小于该值（例如只有几百 KB），说明上传被网络截断 → 页面会出现**标题能显示但图表空白**。
- 处理方式：删掉重新上传，或改用下方 Git 命令行方式。

## 备选用 Git 命令行上传（更稳，避免网页上传中断）

```bash
git clone https://github.com/<用户名>/<仓库名>.git
cd <仓库名>
cp /路径/disney-dashboard-github/index.html .
cp /路径/disney-dashboard-github/.nojekyll .
git add -A && git commit -m "deploy dashboard" && git push
```
再到 Settings → Pages 开启（同步骤 3）。

## 看板功能

- **年份切换**：2025 / 2024 / 双年对比
- **地图三模式**：OD 飞线 / 热力图 / 仅站点
- **TOP-N 滑杆**（5–30）、**15 条线路筛选 chip**、**点击联动**（点柱状图/玫瑰图定位到地图站点）
- 数据口径：2025-05-01 09 时 TOP100 OD（201 人次 / 95 站 / 15 线 / 12 区）；2024 同期基线（398 人次 / 284 站）。两年榜单截断口径不同，同比以头部 TOP 与结构占比为准。

## 本地预览

直接双击 `index.html` 即可打开（无需服务器）。
