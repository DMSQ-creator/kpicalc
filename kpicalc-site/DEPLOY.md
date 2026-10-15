# KPICalc — 部署指南

## 1. 注册域名

- 推荐：`kpicalc.com`（2026-10-10 已核验可注册，付款前请再查一次）。
- 注册商建议：Cloudflare Registrar，按成本价卖，续费不加价。
- 别用 `.xyz`：续费并不比 .com 便宜，而且 B2B 用户更信任 `.com`——信任正是这个站变现的东西。

## 2. 部署（15 分钟，免费）

1. 把 `kpicalc-site` 整个文件夹推送到一个 GitHub 仓库。
2. Cloudflare 后台 → Pages → Create → Connect to Git → 选择该仓库。
   - Build command：留空；Output directory：填 `/kpicalc-site`
   - （如果传的是文件夹"里面"的内容到仓库根目录，输出目录填 `/`）
3. Pages → Custom domains → 添加 `kpicalc.com`（再加个 `www`，重定向到主域名）。
   - 域名如果已经托管在 Cloudflare，DNS 自动配置，SSL 证书也自动。
4. 完成。以后每次 `git push` 都会自动重新部署。

## 3. 申请 AdSense 之前

纯工具页会被以 "Low value content"（低价值内容）拒掉。本站已按过审配方来做——
每新增一个工具页，都照着复制：

- [ ] 每个工具页：可用的计算器 + 200–400 词的原创指南文字 + 3–5 个 FAQ
- [ ] JSON-LD：WebApplication + FAQPage schema（照抄 roi-calculator/index.html）
- [ ] About 和 Privacy 页面必须上线（cookie/广告披露已写好）
- [ ] 广告位现在是注释掉的占位符——**过审之后**再打开，且广告不能紧贴"计算"按钮和输入框（政策要求）
- [ ] 攒到 ~10 个工具页再去申请，别一两个页面就申
- [ ] 指南文字每篇现写，别复制粘贴

## 4. 联系邮箱收信

privacy 页写的是 contact@kpicalc.com，要让它真能收信：
Cloudflare 后台开 **Email Routing**（免费），把 contact@kpicalc.com
转发到你自己的邮箱，几分钟搞定。
