# QuotaCard — AI 额度桌面卡片

Windows 桌面小卡片,实时显示各 AI 平台的**真实额度**:窗口用量、账户余额、消耗曲线,支持置顶悬浮、「刘海 / 灵动岛」贴靠、桌面宠物、消息推送提醒。

> 本仓库仅发布编译好的安装包与使用文档,**不开源**。

## 下载安装

前往 [Releases](https://github.com/dcxa521gi/QuotaCard/releases/latest) 页面下载最新版 `QuotaCard Setup X.Y.Z.exe`,双击安装即可(Windows 10/11 x64)。

### 更新日志

**v1.16.0**
- **灵动岛模式**:除贴边「刘海」外新增悬浮胶囊「灵动岛」;拖拽吸附上/下/左/右,收起为四角纯圆的紧凑胶囊、宽度自适应,灵动岛在上/下可自由左右摆放
- **桌面宠物**:随额度健康度变表情,有任务在跑时进入「工作中」动画;内置团子/小恶魔/小天使/像素人/动物森友会/塞尔达 ChuChu 六种,并支持**上传自定义图片 / GIF**
- **ChatGPT(原 Codex)**:更名、仅保留每周窗口、移除已下线的邀请;新增 **Token 活动热力图**(GitHub 风格,每日/每周/累计切换,悬浮看数值,随卡片宽度自适应)
- **消息推送**:全能消息推送(Brak)+ 飞书自定义机器人双通道;用尽后每 30 分钟提醒剩余重置时间,22:00 汇总含当日用尽次数
- **运行监测**:标注 Claude / ChatGPT CLI 是否在运行,额度重置后可弹「继续任务」卡片

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
| ChatGPT(原 Codex) | 每周窗口、重置卡数量、Token 活动热力图(本地会话统计) | 自动读 `~/.codex/auth.json` |
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

- **卡片墙**:默认显示 Claude + ChatGPT,底部「＋ 添加卡片」可加其余平台;左滑移除,拖出窗口变独立小卡片
- **刘海 / 灵动岛**:贴靠屏幕顶部或四边,收起时循环额度 / 红绿灯 / 宠物,悬浮弹出完整卡片,双击打开主界面;灵动岛为悬浮胶囊、可自由摆放
- **桌面宠物**:随额度健康度和 CLI 运行状态做休息/工作动画,多种形象 + 支持上传自定义图片/GIF
- **消息推送**(全能消息推送 Brak + 飞书):额度每消耗 20%、用尽、窗口恢复各推送一次;每天 22:00 汇总当日消耗与用尽次数
- **外观**:透明度、深色/浅色/跟随系统主题、大字/高对比模式、增强光圈,调节透明度时全窗口实时预览
- 托盘常驻,自动刷新(默认 3 分钟)

## 关于 Claude 桌面版

**Claude 桌面版/网页版无法提供额度接口所需的令牌**,二选一:

1. 安装 [Claude Code CLI](https://docs.claude.com/en/docs/claude-code/setup)(`npm install -g @anthropic-ai/claude-code`)并运行 `claude` 登录一次,卡片会自动读取凭证;
2. 终端运行 `claude setup-token`,把生成的 `sk-ant-oat01-...` 令牌粘贴到 卡片设置 → Claude 令牌。

## ChatGPT(原 Codex)Token 活动

安装并登录 Codex CLI 后,程序会自动读取 `~/.codex/auth.json` 显示每周额度与重置卡,并聚合本地会话日志画出 Token 活动热力图(每日/每周/累计,悬浮看具体数值)。无需额外填写。

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
