# 排排座 · Seating Chart

一个**纯前端、单文件、离线可用**的交互式座位表工具。双击 HTML 就能用，拖拽换座、增删人员、导入 Excel 名单、一键生成可群发的分享链接。

适用于：婚宴 / 年会 / 会议 / 培训 / 答辩 / 聚餐 / 考场 / 任何「谁坐哪」的场景。

> 本项目同时是一个 [WorkBuddy / CodeBuddy Skill](#作为-workbuddy-skill-使用)，可被 AI 助手自动调用来生成座位表。

---

## ✨ 功能一览

| 能力 | 说明 |
| --- | --- |
| 🖱 拖拽换座 | 拖到**人名上** = 两人互换；拖到**桌面空白** = 移到该桌末尾 |
| 🪑 桌位管理 | 一键加桌、删桌；布局固定每行 2 桌，桌名自动生成 |
| 👤 人员管理 | 添加人员、右键「在此人后加人」、删除；支持性别、职级字段 |
| 📥 名单导入 | 支持 `.xlsx` / `.xls` / `.csv`，自动识别表头、中文数字桌号 |
| 🎨 颜色标记 | 右键单个姓名框 → 填充颜色，用于区分部门 / 嘉宾 / 桌主等 |
| 📄 导出 CSV | 导出含「姓名 / 桌号 / 性别 / 职级」的表格（带 BOM，Excel 不乱码） |
| 🔗 分享链接 | 把整份排座编码进 URL 的 `#s=` 片段，复制链接即可群发，对方可继续编辑 |
| 🖨 打印 / 存 PDF | 打印预览面板：每页桌数（自动 / 1~6 桌）、缩放、横纵向 |
| 🔍 搜索定位 | 左侧名单实时搜索，点击定位到座位 |
| 🗂 多任务 | 可建多个排座任务并存、切换、重命名、删除 |
| 💾 本地保存 | 所有数据自动存入浏览器 `localStorage`，刷新不丢 |

---

## 🚀 快速开始

**方式一：直接用（推荐）**

1. 下载 [`assets/seating.html`](assets/seating.html)（约 60KB）
2. 双击用浏览器打开 → 开始排座
3. 排完点「🔗 分享」复制链接发给别人

**方式二：用在线版**

开启 GitHub Pages 后访问 `https://<用户名>.github.io/seating-chart/` 即可（见[部署](#部署到-github-pages)）。

---

## 📖 使用说明

### 鼠标操作

| 操作 | 效果 |
| --- | --- |
| 拖拽姓名 → 另一个姓名 | 两人互换座位 |
| 拖拽姓名 → 桌面空白处 | 移到该桌末尾 |
| 单击姓名（或右键） | 弹出菜单：在此人后加人 / 填充颜色 / 删除此人 |
| 点击顶部标题 | 直接编辑活动名称 |

### 导入名单格式

导入文件按列读取（**有无表头都能识别**）：

| 第 1 列 | 第 2 列（可选） | 第 3 列（可选） | 第 4 列（可选） |
| --- | --- | --- | --- |
| 姓名 | 桌号 | 性别 | 职级 |

- 桌号支持 `1`、`第1桌`、`Table 3`、`三` 等写法
- 左侧名单栏用彩色徽标显示性别 / 职级；座位图上只显示姓名，鼠标悬停可看完整信息
- **导入 Excel 需要联网**（首次会从 CDN 拉取 `xlsx` 解析库）；导入 CSV 完全离线

### 分享链接原理

```
https://你的域名/排排座.html#s=eyJ2IjoxLCJ0YXNrcyI6...
```

- 姓名、桌号、颜色、字号、缩放等全部状态被 JSON 序列化 → Base64 → 放进 URL 片段
- **数据不上服务器**，纯前端解析，隐私友好
- 打开链接自动还原排座，接收方可以继续编辑（存到他自己的浏览器）
- ⚠️ 人数多时 URL 会很长（部分聊天软件可能截断）；超大排座建议改用「📄 导出表格」发 CSV

### ⚠️ 数据安全提醒

数据存在**当前浏览器**的 `localStorage` 里。**换浏览器、换设备、清缓存都会丢失**。重要排座请务必：
1. 点「📄 导出表格」备份 CSV，或
2. 点「🔗 分享」把链接存到备忘录

---

## 部署到 GitHub Pages

仓库里已内置 `docs/index.html`，开箱即用：

1. 仓库 → **Settings** → **Pages**
2. Source 选 `Deploy from a branch`
3. Branch 选 `main`，文件夹选 `/docs`
4. 保存，等 1~2 分钟，访问 `https://<用户名>.github.io/seating-chart/`

部署后，本地排座点「分享」拿到的 `#s=...` 片段，拼到这个公开地址后面就是可群发的链接：

```
https://<用户名>.github.io/seating-chart/#s=eyJ2IjoxLCJ0YXNrcyI6...
```

> `docs/index.html` 是 `assets/seating.html` 的副本（GitHub Pages 根目录需要 `index.html`）。
> 改动主文件后同步一次：
> ```bash
> cp assets/seating.html docs/index.html
> ```

---

## 作为 WorkBuddy Skill 使用

本仓库同时是一个 Skill 包。安装方式：

```bash
# 用户级（所有项目可用）
git clone https://github.com/<用户名>/seating-chart.git ~/.workbuddy/skills/seating-chart

# 或项目级
git clone https://github.com/<用户名>/seating-chart.git .workbuddy/skills/seating-chart
```

安装后，对 AI 说「**帮我排个座**」「**做个婚宴座位表**」「**排排座**」等，助手会自动：

1. 复制 `assets/seating.html` 到工作区（不污染模板源文件）
2. 打开预览面板供你拖拽编辑
3. 说明导入 / 分享 / 导出等用法

`SKILL.md` 中的 `description` 字段是触发词表，修改它可调整触发范围。

---

## 📁 目录结构

```
seating-chart/
├── README.md            # 你正在看的这份说明
├── SKILL.md             # Skill 定义文件（触发词、调用步骤）
├── LICENSE              # MIT
├── .gitignore
├── assets/
│   └── seating.html     # ⭐ 核心：自包含单文件应用（唯一需要维护的源文件）
└── docs/
    └── index.html       # assets/seating.html 的副本，供 GitHub Pages 使用
```

---

## 🛠 技术说明

- **零依赖、零构建**：原生 HTML + CSS + JavaScript，无框架、无打包步骤
- **离线可用**：除「导入 Excel」需联网拉 CDN 外，其余功能断网也能跑
- **浏览器要求**：Chrome / Edge / Safari / Firefox 现代版本（用到 `localStorage`、`URL.createObjectURL`、`btoa`）
- **移动端**：界面为桌面端优化，手机上可查看，编辑体验一般

---

## 📄 License

[MIT](LICENSE) © kaisa

可以自由使用、修改、分发，包括商业用途。
