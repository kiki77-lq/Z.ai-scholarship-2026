# Z.AI Scholarship 2026 官网

智谱青年研究者奖学金计划（Z.AI Scholarship 2026）官方网站。

> 问道 AGI，同行未来 · Toward AGI, with the next generation.

这是一个**纯静态单页网站**：`index.html` 已内联全部 CSS 与 JavaScript，运行时仅外链 Google Fonts，**不依赖**任何后端、构建步骤、React runtime 或 Claude Design 的 `.dc.html` / `support.js`。

---

## 目录结构

```
z-ai-scholarship-2026/project/        ← 部署根目录
├── index.html                        ← 网站入口（自包含）
├── assets/                           ← 静态资源（刻意不命名为 public，见下方说明）
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

> ⚠️ **不要把静态资源目录命名为 `public/`**。对无框架（Other）项目，Vercel 会自动把根目录下的 `public/` 当作站点输出目录，导致根目录的 `index.html` 不被托管、访问首页返回 `404: NOT_FOUND`。本项目因此使用 `assets/` 存放资源。

**方式 A：Vercel CLI**

```bash
npm i -g vercel          # 若未安装
cd z-ai-scholarship-2026/project
vercel                   # 预览部署，按提示登录并选择项目
vercel --prod            # 确认无误后生产部署
```

建议项目名：`zai-scholarship-2026`

**方式 B：连接 GitHub 仓库（推荐）**

在 Vercel Dashboard 中 Import Git Repository，选择本仓库。注意：**本仓库的根目录就是站点目录**（`index.html` 直接位于仓库根），因此设置如下：

- Framework Preset → **Other**
- Root Directory → **留空 / `./`**（⚠️ 不要填 `z-ai-scholarship-2026/project`，仓库内不存在这层目录，填了会导致 `404: NOT_FOUND`）
- Build Command / Output Directory / Install Command → **全部留空（不要开启 Override）**

之后每次 `git push` 自动触发部署。

### 日常更新流程

```bash
cd z-ai-scholarship-2026/project
git add .
git commit -m "<描述本次修改>"
git push
# 已连接 GitHub 的 Vercel 项目会自动重新部署
```

---

## 正式申请入口（两个飞书链接，集中在 `index.html` `<script>` 顶部常量）

**1. 申请入口（`APPLICATION_FORM_URL`，飞书表单）**
- URL：`https://zhipu-ai.feishu.cn/share/base/form/shrcnAJYvhX1QOm2G42Uq4TEwwb`
- 绑定：Header「立即申请」、Hero「立即申请」、移动菜单「立即申请」、页脚「在线申请表（飞书）」。

**2. 申请表下载（`FORM_DOWNLOAD_URL`，飞书 wiki）**
- URL：`https://zhipu-ai.feishu.cn/wiki/XWtVwYs37iN4EvkzY6ScgFOBnre?from=from_copylink`
- 绑定：申请指南「申请材料」第一项后的小号文字链接「下载申请表」。

> 两者均新标签页打开（`target="_blank"` + `rel="noopener noreferrer"`）。更换对应链接只改对应常量即可；Application Guide 底部无大按钮。

## 变更记录

### 2026-07-08 · 报名截止日期延期

更新背景：根据项目负责人确认，Z.AI Scholarship 2026 报名截止日期由原日期延后至 2026 年 8 月 16 日 24:00。

更新内容：
- 更新顶部报名提示中的截止日期与倒计时；
- 更新 Review Process / Timeline 中的报名截止节点；
- 更新中英文页面中的报名截止日期表达；
- 确保 Apply / Download Application Form / Privacy Terms 等核心链接不变；
- 确保页面布局和移动端适配不受影响。

验收结论：中文页面截止日期显示为 2026 年 8 月 16 日 24:00；英文页面截止日期显示为 August 16, 2026, 24:00；顶部倒计时正常计算；Review Process / Timeline 日期同步更新；申请入口链接保持不变；桌面端与移动端布局正常。

### 2026-07-08 · 移动端 Header / Notice / Brand 适配修复

修复范围：上线前小范围移动端适配，仅处理 Header、顶部报名提示与品牌文字在移动端的布局问题；不改页面结构、正文文案、申请链接、下载申请表链接或 Privacy Terms 链接。

修复内容：
- 修复移动端报名提示与导航栏重合问题；
- 修复移动端「Z奖学金」品牌文字变形问题；
- 补充移动端多视口 QA。

验收视口：`375×812`、`390×844`、`430×932`、`768×1024`、`1440×900`。

验收结论：无横向滚动；Header 与报名提示不重合；品牌文字不变形；中文页 / 英文页正常；桌面端不受影响；Apply / Download Application Form / Privacy Terms 等核心链接保持正常。

## 待补充信息

页面中以下字段当前仍为占位/待补充状态，需后续填入正式内容：

| 字段 | 当前状态 | 位置 |
| --- | --- | --- |
| 咨询邮箱 | 待补充（`CONTACT_EMAIL` 为空，页脚显示「待补充」） | `index.html` 顶部脚本常量 / 页脚 |
| 智谱官网链接 | 待补充（页脚显示「待补充」） | `index.html` 页脚 |
| English 版本 | 待补充（导航语言切换暂为占位） | `index.html` 导航 |

> 申请入口已接入飞书表单，不再「待补充」。其余未确认信息（邮箱、官网、EN）仍保留「待补充」，未填写的链接点击会提示「该链接待补充」。
