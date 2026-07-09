# QuotaCard — AI 额度桌面卡片

Windows 桌面小卡片,实时显示各 AI 平台的**真实额度**:5 小时/每周窗口、账户余额、消耗曲线,支持置顶悬浮、屏幕四边「刘海」贴靠、消息推送提醒。

> 本仓库仅发布编译好的安装包与使用文档,**不开源**。

## 下载安装

下载最新版 [QuotaCard Setup 1.10.0.exe](downloads/QuotaCard%20Setup%201.10.0.exe),双击安装即可(Windows 10/11 x64)。

### 更新日志

**v1.10.0**
- 刘海支持拖拽吸附到屏幕上/下/左/右四边,左右停靠时窄条竖排、文字竖向显示,悬浮弹出完整卡片
- 红绿灯自动综合 5 小时窗口 + 每周窗口等全部额度维度判定颜色,且随全局透明度一起变透
- 新增全能消息推送(Brak):额度每消耗 20%、用尽、窗口恢复各推送一次,每天 22:00 汇总
- 新增硅基流动、词元跳动、可添加多个的自定义接口(OpenAI 兼容)
- 卡片透明度调节实时预览(含刘海),增强光圈支持刘海显示
- 多项界面细节修复(刘海内容精简、圆角/间距、Cursor 网络拦截报错提示更友好等)

## 支持的平台

| 平台 | 显示内容 | 凭证来源 |
|---|---|---|
| Claude | 5h / 7d 窗口用量(含 Opus/Sonnet 分项、Fable 限时窗口)、重置倒计时 | 自动读 Claude Code CLI 凭证并**自动刷新过期令牌**,或设置里粘贴令牌 |
| Codex | 5h / 每周窗口、重置卡数量(专用接口)、邀请剩余次数 | 自动读 `~/.codex/auth.json` |
| DeepSeek | 账户余额 + 消耗曲线 | API Key |
| Kimi | Coding 套餐用量(sk-kimi-)或开放平台余额(sk-) | API Key |
| 智谱AI / Z.ai | GLM Coding Plan 5h + 周期额度、套餐名 | API Key(优先走 z.ai 全球站,绕过反爬;bigmodel 可补 Cookie) |
| MiniMax | Token Plan 5h + 每周窗口 | API Key |
| 小米 MiMo | Token Plan 用量(tp-)或余额(sk-) | API Key |
| 硅基流动 SiliconFlow | 账户余额 + 消耗 | API Key |
| 词元跳动 | 账户余额 + 消耗 | API Key |
| 自定义接口(可添加多个) | OpenAI 兼容余额/账单 | 厂商名称 + 接口地址 + API Key |
| Cursor | 套餐用量 % / Premium 请求 / 按需额度 / 账单周期 | 浏览器 Cookie |
| GitHub Copilot | Premium / Chat 额度、月度重置 | GitHub 令牌(需 Copilot 订阅) |
| Grok(xAI) | SuperGrok 用量、账单周期 | Bearer 令牌 或自动读 `~/.grok/auth.json` |
| Qoder | Credits 额度、套餐、重置时间 | 浏览器 Cookie |
| 火山引擎 | Coding Plan 5h / 周 / 月窗口 | AccessKey(`AK:SK[:region]`) |
| Kiro(AWS) | Credits 用量 | 本地 `kiro-cli`(需 `kiro-cli login`) |
| Antigravity | 各模型剩余额度 | 读取本机运行中的 Antigravity IDE 语言服务器 |

## 主要功能

- **卡片墙**:默认显示 Claude + Codex,底部「＋ 添加卡片」可加其余平台;左滑移除,拖出窗口变独立小卡片
- **刘海模式**:贴靠屏幕顶部(可拖拽吸附到上/下/左/右四边),收起时循环展示额度或显示红绿灯,悬浮弹出完整卡片,双击打开主界面;左右停靠时窄条竖排、文字竖向显示
- **红绿灯**:自动综合 5 小时窗口 + 每周窗口等所有额度维度,取剩余最紧张的一项判定绿/黄/红
- **消息推送**(全能消息推送 / Brak):额度每消耗 20%、用尽、窗口重置恢复各推送一次;每天 22:00 汇总当日消耗
- **外观**:透明度、深色/浅色/跟随系统主题、大字/高对比模式、增强光圈,调节透明度时全窗口(含刘海)实时预览
- 托盘常驻,自动刷新(默认 3 分钟)

## 关于 Claude 桌面版

**Claude 桌面版/网页版无法提供额度接口所需的令牌**,二选一:

1. 安装 [Claude Code CLI](https://docs.claude.com/en/docs/claude-code/setup)(`npm install -g @anthropic-ai/claude-code`)并运行 `claude` 登录一次,卡片会自动读取凭证;
2. 终端运行 `claude setup-token`,把生成的 `sk-ant-oat01-...` 令牌粘贴到 卡片设置 → Claude 令牌。

## Codex 邀请剩余次数

需要 ChatGPT 浏览器 Cookie(OpenAI 服务端限制):设置里点「去获取 →」打开 chatgpt.com,登录后 F12 → Network → 任意 backend-api 请求 → 复制完整 Cookie 粘贴保存。Cookie 仅存本机。

## 消息推送(全能消息推送 / Brak)

在设置 → 全能消息推送里启用,填入你在「全能消息推送」App 中获取的接收端 Token,勾选要监控的卡片即可。[接口文档](http://www.ggsuper.com.cn/push/api.html)

## 常见问题

- **令牌过期**:Claude 现会用 refresh_token **自动刷新**(即将过期时主动刷新、401 时被动刷新并写回 `~/.claude/.credentials.json`);Codex 仍需终端运行一次 `codex` 刷新后点卡片 ⟳。
- **智谱返回为空**:官方接口有反爬,设置里补充 bigmodel.cn 登录 Cookie,或点「用量网页」直接看。
- **接口请求被拦截(ERR_BLOCKED_BY_CLIENT)**:本机安全软件/广告拦截/防火墙拦截了请求,请在其中放行对应域名后重试。
- **接口字段变动**:第三方/未公开接口官方可能调整,显示异常请反馈。

## 隐私说明

所有 API Key / Cookie / 令牌**仅保存在本机**(`userdata/settings.json`),不会上传到任何第三方服务器。程序仅直接请求各平台官方/开放接口获取你自己账户的额度数据。

## 版权说明

本项目仅在此仓库发布预编译安装包与文档,供个人下载使用,不提供源代码、不开放二次分发授权。
