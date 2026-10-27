# KPICalc — 项目说明

KPICalc（https://kpicalc.com）是一个免费的英文 B2B 营销计算器工具站：
10 个交互式计算器（ROI、ROAS、A/B 显著性、CAC、UTM 生成器、LTV:CAC、
邮件基准、CPM/CPC 互算、SaaS 流失/MRR、利润率），每个配指南文字和 FAQ，
靠 Google AdSense 广告变现。

## 技术栈

- 纯静态：HTML + CSS + 原生 JS，无构建步骤、无后端、无依赖
- 计算全部在浏览器端完成，不上传、不存储用户输入
- 托管：Cloudflare Pages（免费层）；每年成本 = 一个域名

## 目录结构

```
kpicalc-site/
├── index.html              首页（品牌 + 10 个工具矩阵）
├── assets/
│   ├── css/style.css       全站共用样式
│   └── favicon.svg         站点图标（品牌蓝圆角 + 白色 K）
├── roi-calculator/         工具页模板（每个工具一个文件夹，内含 index.html）
├── roas-calculator/
├── ab-test-significance/
├── ...（其余 7 个工具同理）
├── about/                  关于页
├── privacy/                隐私政策（含 cookie/广告披露、联系邮箱）
├── README.md               本文件（项目说明）
└── DEPLOY.md               部署指南（注册域名、Cloudflare 上线、AdSense 申请）
```

## 工具页标准配方（新增工具照抄）

每个工具页 = 可用的计算器 + 200–400 词原创指南 + 5 个 FAQ +
JSON-LD（WebApplication + FAQPage）+ 页头面包屑 + 页尾免责声明。
复制 `roi-calculator/` 文件夹改名后，逐项改写：`<title>`、meta 描述、
H1、计算器输入/逻辑、指南文字、FAQ（页面显示和 JSON-LD 里都要改）、
schema 中的 URL。首页工具矩阵加一张卡片，每个工具页互链 3–5 个兄弟工具。

## 广告位

每页预留了 2 个 AdSense 广告位（注释掉的占位符）：
一个在计算器下方、一个在文章底部。**过审之前不要打开**，
打开后保持广告远离"计算"按钮和输入框（AdSense 政策要求）。

## 路径规范

全站使用相对路径（`../assets/...`），不要写成 `/assets/...` 开头，
否则本地预览和换目录部署会挂。新增页面时注意自己所在的目录层级。

## Benchmarks 栏目（/benchmarks/）

定位：原创、可引用的数据报告栏目——不是资讯博客。
每篇报告服务于两个目的：拿长尾关键词排名 + 成为别人文章里的引用来源（带链接）。

报告页标准结构（照着 /benchmarks/index.html 的方法论来）：
- 顶部：报告标题 + 发布日期 + 最后更新日期 + 更新频率
- 方法论小节：数据来源、样本口径、统计周期
- 数据表：每个数字带来源和覆盖年份
- 引用说明：欢迎引用，唯一要求是链接回报告页
- FAQ + FAQPage schema

铁律：**没有来源的数字不许编**。来源不足就写"暂无可靠来源"，
不要用"大约""据估计"蒙混。报告里的数字每年按公布的频率复审一次。

已上线（2026-10-27）：邮件基准（MailerLite 2025 + Mailchimp 2023）、
SaaS 流失基准（ChartMogul 2025 + Benchmarkit 2026）、
CAC/LTV 基准（Benchmarkit 2026）；三篇均带来源链接与 FAQ schema，
落地页卡片已由 Coming soon 改为正式入口。

## 年度复审（每年 10 月）

三篇基准报告每年 10 月复审一次（下次 2027 年 10 月）：
去 MailerLite / ChartMogul / Benchmarkit 查新版报告，有新数据就更新
数字 + 发布日期 + lastmod + sitemap；无新版则只更新"最后复核"日期，
不硬改数字。复审本身也要留记录（改了什么、来源是哪版）。

## 每周数据点栏目（/benchmarks/weekly/）

每周一个数字，格式固定：日期 + 数字 + 一句话说明 + 来源（发布者与发布时间）。
规则：必须有公开来源；某周找不到好来源就空着，不编数、不凑数。
新条目插到列表最前面，并同步更新落地页卡片里的"最新"一句和
sitemap 里该 URL 的 lastmod。

更新用一键脚本（在站外，~/workspace/kpicalc-tools/add_weekly_entry.py，
不会部署到网站），它一次改三处，缺一处就报错停下：

```
python3 ~/workspace/kpicalc-tools/add_weekly_entry.py \
  --date "Week of November 3, 2026" \
  --figure "37%" \
  --label "of email-driven sales from automated emails" \
  --text "Automated emails drove 37% of email-driven sales while accounting for just 2% of email volume." \
  --source-name "Omnisend, 2024 ecommerce data" \
  --source-url "https://www.omnisend.com/"
```

先加 --dry-run 可只看不写。页面里的 <!-- WEEKLY-ENTRIES-START --> 与
<!-- WEEKLY-LATEST-START --> 标记是脚本的定位点，不要删。
手动改格式时照抄现有条目的 div 结构（.data-point），不要自创样式。

## 日常维护

- 改全站共用样式（style.css）后，必须给所有页面的 CSS 链接加 ?v=N（每次改动 N+1）强制刷新，否则老访客浏览器会继续用缓存的旧样式（2026-10-27 教训：表格样式已上线但因缓存看不到）

- UptimeRobot 免费版做可用性监控（死链直接掉排名）
- 每年审一次内容（基准数据、统计口径有变的更新）
- AdSense 政策中心：ads.txt 保持有效，有警告马上处理

## 路线图

- 第一批 10 个工具：已全部上线
- 第二层（待定）：金融计算器系列（房贷、复利、退休、税务），等第一批跑顺、拿到搜索权重后再铺
