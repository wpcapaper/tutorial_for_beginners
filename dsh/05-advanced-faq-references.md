# 第五章：进阶、常见问题与参考文献

[返回教程首页](README.md) · [上一章：macOS / Linux 快速上手](04-getting-started-unix.md)

这一章分四部分：**进阶玩法**（学有余力再看）、**常见问题汇总**、**去哪里求助**、以及最重要的——**参考文献**（全文所有论断的出处）。

---

## 5.1 进阶玩法（可选）

以下内容面向已经能用 dsh 干活、想更进一步的同学。看不懂没关系，不影响正常使用。

### 5.1.1 命令行"一次性任务"（headless 模式）

除了网页版，dsh 还自带一个"一次性任务"模式：在命令行里直接派活，AI 干完、打印结果、自动退出 [11]。官方对它的描述：

> "Run one fresh persisted session, print the final answer, and exit."（运行一个全新的一次性会话，打印最终答案后退出。）[11]

用法（在终端里，工作文件夹内）：

```powershell
npx @deepseek-ai/dsh --profile headless "把这个文件夹里所有 txt 文件的标题整理成列表"
```

适合不想开网页、只想"丢一个任务就跑"的场景 [33]。

### 5.1.2 配置文件 settings.yaml

dsh 的很多设置都存在 `$DSH_HOME/settings.yaml` 里（Windows 上一般是 `C:\Users\你的用户名\.dsh\settings.yaml`）[27]。官方说这个文件支持**热更新**——你改完保存，dsh 会自动生效，不用重启 [27]。当你需要配置官方网页界面里没有的进阶选项时（比如自定义模型提供方、兼容参数），就编辑这个文件 [7]。

### 5.1.3 插件的世界

还记得第一章说的"一切皆插件"吗 [1][3]？如果你以后想给 dsh 加功能：

- 官方鼓励开发者发布插件，并建议给插件仓库打上 `dsh-plugin` 话题标签，便于被发现 [1]；
- 每个部件（模型适配器、工具、会话记录、审批……）都是插件，都可以替换 [3]；
- 想了解 dsh 由哪些插件组成，可以运行 `dsh --profile web --dump-config` 查看实际启动的配置树 [3]。

### 5.1.4 术语表与官方文档地图

- 术语表（遇到不懂的词先查这个）：[官方术语表](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.zh.md) [12]
- 文档地图：官方仓库的 `docs/` 目录下有架构、配置、工具、子系统等全套文档（本教程的参考文献里列了主要几篇）。

## 5.2 常见问题汇总

| 问题 | 答案 |
|---|---|
| dsh 免费吗？ | 软件本身免费开源（MIT 协议）[1]；调用模型需要 DeepSeek API 密钥，按用量计费 [7] |
| 我的对话记录存在哪？ | 会话记录是持久化的 [8]；配置和密钥存在 `~/.dsh`（`$DSH_HOME`）下，其中密钥在 `.credentials.yaml` [7] |
| AI 会乱删我的文件吗？ | 默认权限是"工作区可写 + 询问"：AI 只能在工作区内自由读写，危险操作会先问你 [10][27]；不点"完全访问"它动不了工作区以外的东西 |
| 为什么 AI 在 Windows 上用的是 PowerShell？ | 官方设计：Windows 没有 bash 运行器，所以 Windows 上挂载 PowerShell 命令栈 [13] |
| 版本会变吗？ | 会。官方明确提示"开发者预览阶段，会有破坏兼容性的变更" [1]。教程基于 `0.1.1-rc.2` 撰写 [2] |
| 我想用别的模型（OpenAI、Claude 等）可以吗？ | 可以。官方模型配置指南支持添加其他提供方和自定义兼容端点 [7] |
| 一个命令都记不住怎么办？ | 只需要记住一条：`npx @deepseek-ai/dsh web`（在你要干活的那个文件夹里运行）[1] |

## 5.3 去哪里求助（官方渠道）

| 渠道 | 用途 | 地址 |
|---|---|---|
| GitHub Discussions | 提交反馈、问问题、报 bug | [https://github.com/deepseek-ai/deepseek-harness/discussions](https://github.com/deepseek-ai/deepseek-harness/discussions) [30] |
| Discord 社区 | 和开发者、用户交流 | [https://discord.gg/Ycq5dCaS4](https://discord.gg/Ycq5dCaS4) [31] |
| 企微群 / 微信公众号 | 中文用户社群（官方 README 中文版提供入群二维码） | [官方仓库 README.zh.md](https://github.com/deepseek-ai/deepseek-harness/blob/master/README.zh.md) [1] |

> 提问小技巧：先看看官方文档和 Discussions 里有没有人问过同样的问题；提问时附上你的系统、版本和报错原文，别人更容易帮你。

## 5.4 延伸阅读（媒体报道，帮你了解背景）

- 澎湃新闻：《DeepSeek智能体框架开放测试：Harness是什么？有什么特别？》 [34]
- 小众软件：《DeepSeek 官方发布类 OpenClaw 工具：开源 Agent 框架 DeepSeek Harness》 [35]
- 驱动 dsh 的底层框架 Cordis 项目：[https://github.com/cordiverse/cordis](https://github.com/cordiverse/cordis) [36]

## 5.5 参考文献（全文出处）

> 说明：本教程所有事实性论述均标注了编号引用。官方仓库文档以 `master` 分支的路径给出；如链接失效，请到 [https://github.com/deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness) 按文件名查找。

### DeepSeek Harness 官方资料（1–13）

1. DeepSeek Harness 官方仓库及 README（英文/中文）——定义、插件化架构、开发者预览说明、启动命令、社区渠道、MIT 协议：https://github.com/deepseek-ai/deepseek-harness/blob/master/README.md ／ https://github.com/deepseek-ai/deepseek-harness/blob/master/README.zh.md
2. npm 上 `@deepseek-ai/dsh` 包页面（版本号 `0.1.1-rc.2`）：https://www.npmjs.com/package/@deepseek-ai/dsh
3. 官方《架构》文档（中文）——一切皆插件、profile、核心包、轮次流程、会话日志、扩展点：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.zh.md
4. 官方《Web UI 使用指南》（中文）——配置模型、选择工作区、运行任务、审批说明：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.zh.md
5. 官方《开发》文档（中文）——Node.js 版本要求（22.19+ 与 24+）：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/development.zh.md
6. 官方《工具 Schema 目录》（中文）——read/write/edit、glob/grep、bash/pwsh、run_code、ask_user_question 等工具清单：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/tool-catalog.zh.md
7. 官方《配置模型》指南（中文）——DeepSeek API 密钥、密钥存储位置（`$DSH_HOME/.credentials.yaml`）、自定义提供方：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.zh.md
8. 官方《插件配置目录》（中文）——会话持久化（`dsh-session-persistence-*`）等插件配置：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/config-catalog.zh.md
9. 官方《用户审批》子系统文档（中文）——`ask` / `never` 审批策略：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/approval.zh.md
10. 官方《进程沙箱》子系统文档（中文）——`read-only` / `workspace-write` / `danger-full-access` 三种模式，Linux bwrap/Landlock、macOS Seatbelt、Windows ACL：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/sandbox.zh.md
11. 官方 dsh 命令行（CLI）README——`dsh web` 别名、`--profile headless`、应用参数（如 `--port`）：https://github.com/deepseek-ai/deepseek-harness/blob/master/apps/cli/README.md
12. 官方《术语表》（中文）：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/glossary.zh.md
13. 官方 dsh-base 组合包 README（中文）——Windows 平台禁用 bash、挂载 PowerShell 命令栈：https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/bundle/base/README.zh.md

### 对比工具（Coze / WorkBuddy，14–26）

14. 百度百科《扣子Coze》词条——"字节跳动开发的AI智能体搭建与工作流编排平台"：https://baike.baidu.com/item/扣子Coze/68194952
15. 扣子（Coze）官网：https://www.coze.cn/
16. 扣子官方文档（工作流、插件、知识库、发布渠道等）：https://docs.coze.cn/
17. 扣子官方文档《订阅套餐上线通知》（免费与付费说明）：https://docs.coze.cn/guides_coze_premium_preview
18. 腾讯云开发者社区《腾讯全场景 AI 智能体桌面工作台 WorkBuddy 产品与技术应用概要》：https://cloud.tencent.com.cn/developer/article/2651884
19. 新浪科技《腾讯WorkBuddy正式上线，免部署兼容OpenClaw开启AI办公新体验》：https://k.sina.cn/article_5787187353_158f17899020022ehu.html
20. 东方财富《腾讯版"小龙虾"WorkBuddy来了！不用部署 安装就能用》：https://finance.eastmoney.com/a/202603093666142382.html
21. 程序那些事儿《拒绝"牛马"！腾讯出品的WorkBuddy，这款在你电脑里"替你干活"的神器》：https://cloud.tencent.com.cn/developer/article/2646827
22. 《小白2天上手WorkBuddy的经验分享》：https://cloud.tencent.com.cn/developer/article/2699138
23. 量子位《从超级个体到超级团队，腾讯云发布WorkBuddy企业版》：https://www.qbitai.com/2026/06/430758.html
24. CodeBuddy《腾讯版🦞上岗！WorkBuddy Claw 重磅公测，5,000 Credits 免费送！》：https://cloud.tencent.com.cn/developer/article/2638721
25. WorkBuddy 官方文档《产品简介》：https://www.workbuddy.cn/docs/workbuddy/Overview
26. WorkBuddy 官方定价页：https://www.workbuddy.cn/pricing/

### 平台与配置文件（27–29）

27. 官方《插件配置目录》（中文）——权限预设（`workspace-write` + `ask` 默认）、PowerShell 探测顺序（`dsh-pwsh-local`）、`settings.yaml` 与 `$DSH_HOME`（`~/.dsh`）路径：https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/config-catalog.zh.md
28. DeepSeek 开放平台（注册、API 密钥、用量计费）：https://platform.deepseek.com/
29. Node.js 官网（下载 LTS 版本）：https://nodejs.org/

### 社区与组合包（30–33）

30. DeepSeek Harness GitHub Discussions：https://github.com/deepseek-ai/deepseek-harness/discussions
31. DeepSeek Harness Discord 社区：https://discord.gg/Ycq5dCaS4
32. 官方 dsh-web-app 组合包 README（中文）——SSH 启动行为、Web UI 相关说明：https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/bundle/web-app/README.zh.md
33. 官方 dsh-headless 组合包 README（中文）——一次性任务运行器：https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/bundle/headless/README.zh.md

### 延伸阅读（34–36）

34. 澎湃新闻《DeepSeek智能体框架开放测试：Harness是什么？有什么特别？》：https://m.thepaper.cn/detail/33783308
35. 小众软件《DeepSeek 官方发布类 OpenClaw 工具：开源 Agent 框架 DeepSeek Harness》：https://www.appinn.com/deepseek-harness/
36. Cordis 项目仓库（dsh 的底层框架）：https://github.com/cordiverse/cordis

---

## 5.6 版本与更新说明

- 本教程撰写时的最新版本：`@deepseek-ai/dsh@0.1.1-rc.2` [2]（2026 年 8 月）。
- 版本号随时会变：官方提示处于开发者预览阶段 [1]。建议你每次安装时以 npm 页面显示的最新版本为准 [2]。
- 如果未来界面/命令有变化，本教程的[官方资料参考文献](05-advanced-faq-references.md#55-参考文献全文出处)依然是第一手依据。

**教程到这里就结束了。现在，去[第三章](03-getting-started-windows.md)（或[第四章](04-getting-started-unix.md)）装好它，然后像用 WorkBuddy 一样，用一句大白话给 DeepSeek 派第一件活吧！**
