# Z.AI Scholarship 2026 官网

智谱青年研究者奖学金计划（Z.AI Scholarship 2026）官方网站。

> 问道 AGI，同行未来 · Toward AGI, with the next generation.

这是一个**纯静态单页网站**：`index.html` 已内联全部 CSS 与 JavaScript，运行时仅外链 Google Fonts，**不依赖**任何后端、构建步骤、React runtime 或 Claude Design 的 `.dc.html` / `support.js`。

---

## 目录结构

```
z-ai-scholarship-2026/project/        ← 部署根目录
├── index.html                        ← 网站入口（自包含）
├── public/
│   └── images/
│       └── z-scholarship-hero-real.png   ← Hero 背景图（被引用）
├── vercel.json                       ← Vercel 静态站点配置
├── README.md
├── .gitignore
└── .vercelignore
```

> 以下文件保留在本地但**不参与部署**（已在 `.gitignore` / `.vercelignore` 中排除）：
> `*.dc.html`（Claude Design 原始设计源文件）、`support.js`（未使用的设计 runtime）、
> `screenshots/`、`uploads/`（内部截图与参考素材）、`.DS_Store`、`.thumbnail`。

---

## 本地预览

无需安装依赖，任选其一：

```bash
# 方式一：Python 自带 HTTP 服务
cd z-ai-scholarship-2026/project
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080

# 方式二：Node serve
npx serve .
```

也可直接用浏览器打开 `index.html`，但通过本地服务器预览更接近线上效果。

---

## 部署

### 部署根目录

```
z-ai-scholarship-2026/project/
```

### Vercel 部署说明

**配置（vercel.json）**

```json
{
  "cleanUrls": true,
  "trailingSlash": false
}
```

纯静态站点，无需 Build Command 与 Output Directory，Vercel 直接托管根目录静态文件。

**方式 A：Vercel CLI**

```bash
npm i -g vercel          # 若未安装
cd z-ai-scholarship-2026/project
vercel                   # 预览部署，按提示登录并选择项目
vercel --prod            # 确认无误后生产部署
```

建议项目名：`zai-scholarship-2026`

**方式 B：连接 GitHub 仓库（推荐）**

在 Vercel Dashboard 中 Import Git Repository，选择本仓库，Framework Preset 选 **Other**，Root Directory 指向 `z-ai-scholarship-2026/project`（若仓库根即为该目录则留空）。之后每次 `git push` 自动触发部署。

### 日常更新流程

```bash
cd z-ai-scholarship-2026/project
git add .
git commit -m "<描述本次修改>"
git push
# 已连接 GitHub 的 Vercel 项目会自动重新部署
```

---

## 待补充信息

页面中以下字段当前为占位/待补充状态，需后续填入正式内容：

| 字段 | 当前状态 | 位置 |
| --- | --- | --- |
| 申请链接（立即申请 / 进入申请通道） | 已填飞书 wiki 临时链接（`APPLY_URL`） | `index.html` 顶部脚本常量 |
| 申请指南链接 | 同上（`GUIDE_URL`，与申请链接一致） | `index.html` 顶部脚本常量 |
| 申请材料包 / 申请表下载链接 | 待补充（`MATERIALS_URL` 为空） | `index.html` 顶部脚本常量 |
| 咨询邮箱 | 待补充（`CONTACT_EMAIL` 为空，页脚显示「待补充」） | `index.html` 顶部脚本常量 / 页脚 |
| 智谱官网链接 | 待补充（页脚显示「待补充」） | `index.html` 页脚 |
| English 版本 | 待补充（导航语言切换暂为占位） | `index.html` 导航 |

补充时统一修改 `index.html` `<script>` 顶部的链接常量即可，未填写的链接会提示「该链接待补充」。
