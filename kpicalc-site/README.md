# KPICalc — 部署指南

纯静态营销计算器网站。无服务器、无后端、无需构建。
托管：Cloudflare Pages（免费）。每年成本：一个域名（约 $10/年）。

## 1. 注册域名

- 推荐：`kpicalc.com`（2026-10-10 已核验可注册，付款前请再查一次）。
- 注册商建议：Cloudflare Registrar，按成本价卖，续费不加价。
- 别用 `.xyz`：续费并不比 .com 便宜，而且 B2B 用户更信任 `.com`——信任正是这个站变现的东西。

## 2. 部署（15 分钟，免费）

1. 把本文件夹推送到一个 GitHub 仓库。
2. Cloudflare 后台 → Pages → Create → Connect to Git → 选择该仓库。
   - Build command：留空；Output directory：`/`
3. Pages → Custom domains → 添加 `kpicalc.com`（再加个 `www`，重定向到主域名）。
   - 域名如果已经托管在 Cloudflare，DNS 自动配置，SSL 证书也自动。
4. 完成。以后每次 `git push` 都会自动重新部署。

## 3. 申请 AdSense 之前

纯工具页会被以 "Low value content"（低价值内容）拒掉。本模板已经按过审配方来做——
每新增一个工具页，都照着复制：

- [ ] 每个工具页：可用的计算器 + 200–400 词的原创指南文字 + 3–5 个 FAQ
- [ ] JSON-LD：WebApplication + FAQPage schema（照抄 roi-calculator/index.html）
- [ ] About 和 Privacy 页面必须上线（cookie/广告披露已写好）
- [ ] 广告位现在是注释掉的占位符——**过审之后**再打开，且广告不能紧贴"计算"按钮和输入框（政策要求）
- [ ] 攒到 ~10 个工具页再去申请，别一两个页面就申
- [ ] 指南文字每篇现写，别复制粘贴

## 4. 新增工具（复制粘贴流程）

1. 复制 `roi-calculator/` 文件夹 → 改名，比如 `roas-calculator/`。
2. 改写：`<title>`、meta description、H1、计算器的输入项和计算逻辑、
   指南文字、FAQ（页面上显示的和 JSON-LD 里的都要改）、schema 里的 URL。
3. 首页工具矩阵里加一张卡片（把 `soon` 改成正式链接）。
4. 内链：每个工具页链向 3–5 个兄弟工具页。

## 5. 路线图（按方案优先级）

接下来 9 个工具：ROAS 计算器 → A/B 显著性检验 → CAC → UTM 生成器 →
LTV:CAC → 邮件基准对比 → CPM/CPC 互算 → SaaS 流失/MRR → 利润率计算器。
第二层再做金融计算器系列。

## 6. 日常维护（每年几十小时）

- 可用性监控（UptimeRobot 免费版）——死链直接掉排名。
- 每年审一次内容（基准数据、口径有变的更新）。
- AdSense 政策中心：ads.txt 保持有效，有警告马上处理。
