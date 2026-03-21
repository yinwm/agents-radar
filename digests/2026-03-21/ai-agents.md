# OpenClaw 生态日报 2026-03-21

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-03-21 01:14 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 (2026-03-21)

## 1. 今日速览
OpenClaw 项目今日继续保持极高的活跃度，过去 24 小时内处理了约 **1000** 个 Issue 和 PR 更新（500+ Issues, 500+ PRs），显示出强大的社区开发动力。代码合并（244 个 PR）与新开启的请求（256 个 PR）几乎持平，表明项目在快速迭代的同时，技术债务管理也面临挑战。核心开发者的工作集中在**移动端配对流程优化**（iOS）、**Ollama 本地模型支持增强**以及 **WhatsApp/Feishu 等通讯渠道的 Bug 修复**。值得注意的是，虽然新版本未发布，但主分支已集成了大量针对 Gateway 稳定性和模型兼容性的修复。

## 2. 版本发布
*   **当前状态**：暂无新版本发布。
*   **主分支状态**：基于今日 PR 分析，主分支已包含多项关键修复（见下文“项目进展”），建议关注即将到来的 v2026.3.14 或补丁版本，以解决近期（尤其是 v2026.3.12/v2026.3.13）引入的回归问题。

## 3. 项目进展
今日合并或正在积极合并的重要 PR 推动了以下领域的进展：

*   **移动端与配对体验 (PR #51359, #51340)**:
    *   改进了 iOS 端的 QR 配对流程，从 ASCII 输出切换为 PNG 图片交付，并强化了安全性。这显著提升了移动用户的首次使用体验。
*   **本地模型支持增强 (PR #51356, #51094)**:
    *   修复了 Ollama 模型在 `openclaw.json` 中无法正确配置 `options` (如 `num_ctx`) 的 Bug。
    *   修复了小型模型在无原生工具支持时的文本回退机制，确保本地 Agent 能更稳定地工作。
*   **模型兼容性与适配 (PR #49512, #51325, #51358)**:
    *   **OpenAI Codex**: 修复了 `gpt-5.4` 模型的解析路径问题。
    *   **GitHub Copilot**: 扩展了动态模型解析能力，现在支持任何未在 SDK 注册表中注册的新模型 ID。
    *   **Azure OpenAI**: 修复了多轮对话中 `reasoning` 模块引发的 400 错误，增强了流式对话的稳定性。
*   **渠道修复 (PR #51059, #51127)**:
    *   **WhatsApp**: 支持了引用回复 (`quote-reply`) 和 `@mention` 功能。
    *   **Feishu**: 修复了忽略 `blockStreamingDefault` 配置的硬编码问题，现在允许用户自定义流式输出行为。
*   **核心架构与稳定性 (PR #51348, #51344)**:
    *   修复了 Gateway 重启后配置文件模型变更不生效的顽固 Bug。
    *   增强了媒体提取错误的处理，防止包含 PII（个人身份信息）的原始错误信息泄露到公开频道。

## 4. 社区热点
以下是今日社区讨论最热烈的话题，反映了用户的迫切需求：

*   **[#3460 国际化 (i18n) 支持](https://github.com/openclaw/openclaw/issues/3460)**
    *   **热度**: 106 👍, OPEN (Enhancement)
    *   **摘要**: 尽管社区呼声极高，官方明确表示目前缺乏带宽支持多语言。这是目前点赞数最高的开放 Issue，表明非英语用户群庞大且需求未被满足。
*   **[#45772 Gateway 心跳定时器失效](https://github.com/openclaw/openclaw/issues/45772)**
    *   **热度**: 20 评论, OPEN (Bug)
    *   **摘要**: v2026.3.8 引入的严重回归，导致 Gateway 心跳在触发 1-2 次后永久停止。这是一个影响系统长期稳定性的高优 Bug。
*   **[#23538 Anthropic 认证 401 错误](https://github.com/openclaw/openclaw/issues/23538)**
    *   **热度**: 23 评论, OPEN (Bug)
    *   **摘要**: Anthropic `setup-token` 在特定版本下运行时调用失败，用户在隔离环境中复现了该问题。
*   **[#50090 社区技能开发与 ClawHub](https://github.com/openclaw/openclaw/issues/50090)**
    *   **热度**: 7 评论, OPEN (Discussion)
    *   **摘要**: 社区正在呼吁改善“插件/技能”生态系统，指出 ClawHub 的承诺与实际体验存在差距。

## 5. Bug 与稳定性
今日报告的关键故障与回归问题，按严重程度排序：

*   **[严重] 上下文限制警告图标遮挡界面 ([#44906](https://github.com/openclaw/openclaw/issues/44906))**:
    *   **现象**: v2026.3.12 中，警告图标异常放大覆盖整个聊天视窗，导致 UI 不可用。
    *   **状态**: Regression (v2026.3.12), Open。
*   **[严重] CLI/WebSocket 握手超时 ([#47265](https://github.com/openclaw/openclaw/issues/47265), [#46892](https://github.com/openclaw/openclaw/issues/46892))**:
    *   **现象**: 升级到 v2026.3.13 后，WebSocket 连接频繁断开 (Error 1000)，3秒的超时设置在负载较高时过于激进。
    *   **状态**: 已有相关修复 PR 正在处理中。
*   **[中等] 工具调用间文本泄露 ([#25592](https://github.com/openclaw/openclaw/issues/25592))**:
    *   **现象**: Agent 处理过程中的内部文本（如错误处理、处理确认）被意外发送到 Slack/iMessage 等消息通道。
    *   **影响**: 严重的 UX 问题，可能泄露内部逻辑。
*   **[中等] Google Vertex ADC 认证失效 ([#49191](https://github.com/openclaw/openclaw/issues/49191))**:
    *   **现象**: 使用 Application Default Credentials 时，字面量字符串 `<authenticated>` 被当作 API Key 发送，导致 401 错误。
*   **[中等] 执行工具输出损坏 ([#24872](https://github.com/openclaw/openclaw/issues/24872))**:
    *   **现象**: `exec` 工具对所有命令返回 `[compacted: ...]`，完全阻断了 Agent 的执行能力。

## 6. 功能请求与路线图信号
用户提出的新功能方向，部分已有 PR 对应：

*   **[外部内存提供者 API](https://github.com/openclaw/openclaw/issues/49233)**: 提出零停机上下文压缩的 API，旨在将 Agent 黑屏时间从 30-60 秒降低至 100ms。这是架构级的重要增强。
*   **[Per-Agent Thinking Config](https://github.com/openclaw/openclaw/issues/21097)**: 请求在 `agents.list` 单个配置中支持 `thinkingDefault`，而不是全局统一设置。这对于混合使用不同算力模型的用户非常关键。
*   **[Tavily 搜索支持](https://github.com/openclaw/openclaw/issues/12034)**: 社区请求用 Tavily API 替代不再免费的 Brave Search API。
*   **[Ollama 模型选项支持](https://github.com/openclaw/openclaw/pull/51356)**: **(已有 PR)** 支持在配置中传递 `num_ctx` 等参数给 Ollama，响应了本地部署用户的深度需求。

## 7. 用户反馈摘要
*   **痛点**: 多数用户抱怨**升级导致的不稳定性**（如 WebSocket 超时、Cron 任务失败、Slack 事件接收）。v2026.3.12 和 v2026.3.13 似乎引入了较多回归问题，导致部分用户被迫降级。
*   **满意度**: 用户对 **Ollama** 集成的改进表示欢迎，但也指出配置灵活性仍有欠缺。
*   **渠道体验**: WhatsApp 和 Signal 用户频繁报告附件发送、文件名保留等问题，细节体验仍需打磨。

## 8. 待处理积压
以下为长期未解决但关注度较高的 Issue，建议维护者优先关注：

*   **[#16629 Brave Search API 不再免费](https://github.com/openclaw/openclaw/issues/16629)**: 状态 CLOSED，但显然需要替代方案（如 Tavily），否则 `web_search` 功能将失效。
*   **[#6156 macOS Gateway 永远未就绪](https://github.com/openclaw/openclaw/issues/6156)**: 影响大量 macOS 用户，导致安装向导卡死。
*   **[#11038 上下文损坏暴露 API 错误](https://github.com/openclaw/openclaw/issues/11038)**: 长期存在的 stale issue，涉及会话损坏时的错误处理机制，不仅丑陋且可能泄露敏感信息。

---

## 横向生态对比

你好！我是专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师。基于 **2026-03-21** 的 GitHub 社区动态，我为您整理了这份横向对比分析报告。

---

# 2026-03-21 AI 智能体开源生态横向对比分析日报

## 1. 生态全景
当前个人 AI 助手开源生态正处于**从“连接器”向“智能体操作系统”转型的关键期**。头部项目（如 OpenClaw、IronClaw）正面临高频迭代带来的技术债务与回归问题，显示出在**模型兼容性**（特别是 OpenAI o1/Claude 3.7 推理模型）和**多模态交互**上的剧烈演进。与此同时，中腰部项目（如 NanoClaw, PicoClaw）通过垂直化切入特定场景（如全平台路由、轻量化部署）展现出强劲的创新力。整体呈现出**去中心化**趋势：从单一 CLI 向 WebUI、Dashboard、多租户 SaaS 演进，且对**数据安全**（内存泄漏、会话串号）和**执行稳定性**（工具调用超时、Cron 任务失效）的关注度达到历史最高点。

---

## 2. 各项目活跃度对比

| 项目名称 | 今日 Issues (新+关) | 今日 PRs (合+开) | 版本发布动态 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500+ | 500+ | 无发布 (v2026.3.14 预备) | 🟡 **高负载**：迭代极快，但 v2026.3.12/13 引入较多回归，需稳住阵脚。 |
| **IronClaw** | 41 | 50 | **v0.21.0** (性能/集成) | 🟢 **稳健**：新版本带来 LRU 缓存和 Webhook，但发现 4 个 Critical 级安全漏洞需警惕。 |
| **LobsterAI** | 35 | 26 (11 合并) | **2026.3.20** | 🔴 **预警**：新版本引发网关频繁重启和会话串号，社区信任度受挑战。 |
| **CoPaw** | 50 | 50 (27 待审) | **v0.1.0.post1** | 🟠 **争议期**：活跃度极高，但多 Agent 编排能力的缺失引发核心用户吐槽。 |
| **NanoClaw** | 7 | 25 (2 合并) | 无 | 🟢 **爆发期**：PR 积压较多，Web/Dashboard 等重量级功能已就绪，待释放。 |
| **Zeroclaw** | ~100 (估) | ~100 (估) | **v0.5.4, v0.5.3, v0.5.2** | 🟢 **激进**：一日三更，快速响应安全策略与 Provider 兼容性。 |
| **PicoClaw** | 23 | 61 | **v0.2.3-nightly** | 🟢 **迭代中**：Cron 任务和空响应问题得到修复，Nightly 版本迭代频繁。 |
| **NullClaw** | 8 | 38 (24 合并) | 无 | 🟢 **高产出**：PR 合并率高，专注于国产模型适配与渠道抽象。 |
| **TinyClaw** | 0 | 5 (4 合并) | **v0.0.16** | 🟢 **精益**：发布 Zero-Config 版本，无 Bug 报告，执行质量极高。 |
| **Moltis** | 少量更新 | 少量更新 | 无 | 🟡 **爬坡**：处于 Windows 兼容性和 Gemini Provider 开发期。 |
| **ZeptoClaw** | 2 (新增) | 0 | 无 | 🔵 **规划期**：无代码合并，处于架构讨论（Firecracker VM）阶段。 |
| **EasyClaw** | 1 (新增) | 0 | **v1.7.3** | 🟡 **维护**：以修复 macOS/Windows 平台兼容性问题为主。 |

---

## 3. OpenClaw 在生态中的定位

*   **生态地位**：作为**核心参照**与**事实标准**，OpenClaw 拥有最大的社区规模（500+ Issues/PRs）和最广泛的模型/渠道支持。其他项目（如 Moltis、NullClaw）在 Issue 讨论中常以“对标 OpenClaw”或“迁移配置自 OpenClaw”作为基准。
*   **技术路线差异**：
    *   **架构**：OpenClaw 采用高度模块化的 Gateway 模式，支持复杂的分布式部署。
    *   **兼容性**：它是模型风向标，今日专门修复了 `gpt-5.4` 和 Azure 的 `reasoning` 模块，显示出对前沿模型 API 的最快响应速度。
*   **社区对比**：相比 Zeroclaw 的“安全优先”和 NanoClaw 的“全能连接”，OpenClaw 更侧重于**企业级落地能力**（如多租户、精细权限）。然而，它目前也背负着最重的历史包袱，今日爆发的 Gateway 心跳失效和 WebSocket 超时问题在复杂度上是其他项目的数倍。

---

## 4. 共同关注的技术方向

通过对今日动态的聚类分析，以下技术方向在多个项目中同时涌现：

1.  **国产大模型深度适配**
    *   **涉及项目**：NullClaw, LobsterAI, PicoClaw, CoPaw
    *   **具体诉求**：
        *   **NullClaw**：全面接入腾讯混元、百川、Kimi（修复 `reasoning_content`）、智谱 GLM。
        *   **PicoClaw**：修复 `glm-4.7` 配置加载问题。
        *   **CoPaw**：用户呼吁加强中文文档和适配。
        *   **信号**：国产模型推理能力（DeepSeek R1, Kimi）的开源生态适配战已打响。

2.  **Rust/性能重构与安全隔离**
    *   **涉及项目**：Zeroclaw, NanoBot, ZeptoClaw
    *   **具体诉求**：
        *   **Zeroclaw**：Rust 原生实现，解决 UTF-8 Panic 问题。
        *   **NanoBot**：新增 `nanobot-rs` crate 探索 Rust 重写。
        *   **ZeptoClaw**：社区发起基于 Firecracker 微虚拟机的沙盒运行讨论，防止 Agent 破坏系统。

3.  **可视化与交互体验**
    *   **涉及项目**：NanoClaw, PicoClaw, IronClaw
    *   **具体诉求**：
        *   **NanoClaw**：合并了 Web Dashboard，支持多租户管理。
        *   **PicoClaw**：WebUI 开发中，用户抱怨缺乏图形化引导。
        *   **IronClaw**：正在进行 UX 大修（PR #1277）。

4.  **推理模型与长思维链支持**
    *   **涉及项目**：OpenClaw, IronClaw, NullClaw, PicoClaw
    *   **具体诉求**：多项目均在修复 `reasoning_content` 字段解析、支持 `thinking` 模式开关、以及解决推理模型在多轮对话中的格式兼容问题。

---

## 5. 差异化定位分析

*   **OpenClaw (巨无霸)**：定位**全能型企业级框架**。优势是功能最全（Gateway、多通道、多模型），劣势是臃肿和稳定性波动。
*   **Zeroclaw (安全派)**：定位**安全优先的个人助手**。强调代码审计和权限控制，但被社区诟病“由于过度安全导致无法安装基本工具（ffmpeg）”。
*   **NanoClaw (连接器)**：定位**全平台消息路由枢纽**。侧重于 Signal、Twilio、WhatsApp 等通讯协议的接入，以及 Agent-to-Agent (A2A) 通信。
*   **IronClaw (构建者)**：定位**软件开发智能体**。提供 LRU 缓存、工作区搜索、Git 集成等开发者特有功能，更像是一个“10倍工程师”助手。
*   **TinyClaw (极简派)**：定位**零配置桌面伴侣**。通过移除 Setup Wizard 和提供一键命令，主打极客和普通用户的零门槛体验。
*   **LobsterAI (桌面应用)**：定位**国人友好的桌面客户端**。基于 OpenClaw，但侧重于 Windows/macOS 的原生打包体验、飞书集成及中文语境优化。
*   **NullClaw (适配器)**：定位**国产模型聚合器**。在支持国产大模型（混元、Kimi、GLM）方面走在最前列。

---

## 6. 社区热度与成熟度

*   **第一梯队 (成熟期/问题爆发期)**：**OpenClaw, IronClaw, CoPaw**。这些项目拥有数千 Stars，活跃度高，但同时也面临复杂的遗留 Bug、数据库迁移难题和日益增长的用户期待（如 CoPaw 的多 Agent 编排争议）。
*   **第二梯队 (快速迭代/创新期)**：**Zeroclaw, NanoClaw, NullClaw, LobsterAI**。这些项目功能日新月异，PR 合并速度快，愿意进行架构重构（如 NanoClaw 的多租户、NullClaw 的消息抽象），是生态中的创新源泉。
*   **第三梯队 (利基/维稳期)**：**TinyClaw, EasyClaw, Moltis**。TinyClaw 追求极致稳定，EasyClaw 和 Moltis 则在特定平台或协议上进行修补。

---

## 7. 值得关注的趋势信号

1.  **“Agentic” 带来的安全危机**：
    今日 **Zeroclaw** (UTF-8 Panic) 和 **LobsterAI** (路径遍历、会话串号) 的严重 Bug，以及 **ZeptoClaw** 社区对 Firecracker VM 的讨论，强烈暗示：**随着 Agent 获得执行 Shell 和文件读写的能力，传统的沙盒机制已不足以应对风险。** 未来的竞争点将从“谁功能多”转向“谁运行得更安全隔离”。

2.  **推理模型 的适配红利**：
    **OpenClaw, IronClaw, NullClaw** 等项目今日都在忙于修复 `reasoning_content` 解析或 `o1` 模型兼容性。谁能最好地支持 DeepSeek R1 / Claude 3.7 Sonnet 等“慢思考”模型的流式输出和思维链展示，谁就能在下一波 AI 浪潮中留住开发者。

3.  **从 CLI 到 GUI 的必然跨越**：
    **NanoClaw** 的 Dashboard、**PicoClaw** 的 WebUI 请求、**IronClaw** 的 UX 大修，标志着纯 CLI 的 AI 助手正在触碰天花板。非技术用户（甚至 C 端用户）的市场需求正在倒逼项目必须提供可视化管理界面。

4.  **国产模型的本地化落地**：
    **NullClaw** 和 **LobsterAI** 的动态表明，中国市场对于使用本地算力（Ollama, LM Studio）运行或通过 API 调用国产大模型有极强的刚需，且对特定字段（如 `reasoning_content`）的解析有特殊要求，国际主流框架（如原版 OpenClaw）可能无法直接满足，催生了专门的 Fork 或适配层。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目日报 (2026-03-21)

## 1. 今日速览
NanoBot 项目今日继续保持极高的活跃度与社区响应速度。过去24小时内，项目共处理了 **107** 个提交项（包括 Issues 和 PRs），其中 Issue 解决率接近 50%（38条中有18条已关闭），PR 合并活跃（32条已合入/关闭）。项目处于快速迭代期，核心重点在于**多模态能力增强**、**渠道特定功能优化**（飞书、Telegram、企业微信）以及**Rust 实现的探索**。尽管没有新版本发布，但从 `nightly` 分支的 PR 密集度来看，下一个功能更新版已在酝酿中。

## 2. 版本发布
*   **当前状态**：无新版本发布。
*   **备注**：大量 PR 正在向 `nightly` 分支合入，建议关注测试版用户的反馈。

## 3. 项目进展
今日合并或接近合并的重要 PR 显示了 NanoBot 在原生体验和基础设施上的稳步推进：

*   **[核心架构] 探索 Rust 实现** (#2313)
    *   **进展**：新增了 `nanobot-rs` crate，实现了基础的 CLI、Provider、Session 和 Agent Loop。
    *   **意义**：项目正式开始尝试用 Rust 重写核心组件，旨在未来提升性能和内存安全性，目前处于 MVP 阶段。
*   **[视觉能力] 原生多模态感知** (#2304)
    *   **进展**：实现了 Agent 原生获取、理解图像等多模态上下文的能力，不再依赖外部纯文本转录。
    *   **意义**：大幅提升了 Agent 处理复杂视觉任务的自主性。
*   **[渠道优化] 飞书话题群支持** (#2307)
    *   **进展**：为飞书渠道添加了基于 `thread_id` 的回复逻辑。
    *   **意义**：修复了在话题群中 Bot 回复错乱的问题，使对话上下文更连贯。
*   **[文件传输] QQ/企微 Base64 上传** (#2306)
    *   **进展**：移除了对公网 URL/IP 的依赖，支持 Base64 格式的媒体文件上传。
    *   **意义**：增强了内网环境下 QQ 和企业微信的文件传输稳定性。
*   **[可观测性] Agent 评估框架** (#2283)
    *   **进展**：引入了无需 API 调用的确定性评估框架，用于测试 Agent 任务完成率和工具使用可靠性。

## 4. 社区热点
今日社区讨论主要集中在配置交互和第三方扩展上：

*   **🔥 配置向导与反馈** (Issue #2018, #2019)
    *   **链接**：[HKUDS/nanobot#2018](https://github.com/HKUDS/nanobot/issues/2018)
    *   **内容**：社区高度关注新的交互式配置向导 (`nanobot onboard`)。虽然其便捷性获得好评，但用户发现在使用 `-c` 指定配置文件时存在参数未识别的 Bug (Issue #2250)。
*   **🔥 第三方 WebUI 面板** (Issue #1922)
    *   **链接**：[HKUDS/nanobot#1922](https://github.com/HKUDS/nanobot/issues/1922)
    *   **内容**：用户 @Good0007 开发了自托管的 Web 管理面板，支持实时聊天和配置管理，获得了 6 个 👍，显示了社区对可视化管理界面的强烈需求。
*   **🔥 WhatsApp 发给自己功能** (Issue #218)
    *   **链接**：[HKUDS/nanobot#218](https://github.com/HKUDS/nanobot/issues/218)
    *   **内容**：关于支持在 WhatsApp 上通过“发消息给自己”来测试 Bot 的讨论热度极高。

## 5. Bug 与稳定性
今日报告的关键 Bug 涉及多个渠道和模型兼容性：

*   **🔴 高危：模型兼容性回归**
    *   **Gemini-3-Flash Preview 失效** ([#2185](https://github.com/HKUDS/nanobot/issues/2185))：从 v0.1.4 升级到 v0.1.4post5 后，特定的 Gemini 模型无法使用。
    *   **DashScope Tool Choice 错误** ([#1927](https://github.com/HKUDS/nanobot/issues/1927))：阿里云 DashScope 不支持 `tool_choice="required"` 导致记忆归档失败。
*   **🟠 中危：渠道交互异常**
    *   **Telegram 消息重复** ([#2235](https://github.com/HKUDS/nanobot/issues/2235))：回复显示两次，疑似伪流式传输导致。
    *   **飞书话题群回复混乱** ([#2256](https://github.com/HKUDS/nanobot/issues/2256))：Bot 未在话题内回复，破坏了上下文（已有 Fix PR #2307）。
*   **🟢 低危：配置与安装**
    *   **Pip 安装转义字符问题** ([#2201](https://github.com/HKUDS/nanobot/issues/2201))：`pip install nanobot-ai[wecom]` 在 zsh 下报错。

## 6. 功能请求与路线图信号
从 PR 和 Issues 中可以窥见未来的开发重点：

*   **LLM Trace (轨迹可观测)** ([#2154](https://github.com/HKUDS/nanobot/issues/2154))：用户强烈希望能通过接口观察 Agent 内部思考过程，这对于调试至关重要。
*   **思考模式开关** ([#2240](https://github.com/HKUDS/nanobot/issues/2240))：请求添加开启或关闭 Chain-of-Thought 的配置选项。
*   **打破无限循环** ([#2298](https://github.com/HKUDS/nanobot/issues/2298))：针对小模型容易陷入工具调用死循环的问题，请求增加检测逻辑。
*   **DingTalk 文件上传支持** ([#1864](https://github.com/HKUDS/nanobot/issues/1864))：用户反馈钉钉渠道尚不支持文件上传。

## 7. 用户反馈摘要
*   **痛点**：
    *   **配置门槛**：尽管有向导，但多模型（Ollama, vLLM, DashScope）的配置细节仍容易出错（API Key, BaseURL 等）。
    *   **本地模型稳定性**：使用本地模型（如 Qwen3-VL, Gemma）时，常遇到 API Key 配置报错或工具调用时的静默失败（连接断开）。
    *   **幻觉问题**：用户反映 Agent 在执行任务时有“假装执行”的幻觉行为（Issue #884）。
*   **好评**：
    *   Docker 部署流程顺畅。
    *   新的 `onboard` 交互式配置大大降低了初学者的上手难度。

## 8. 待处理积压
以下 Issue 长期开放且具有较高关注度，建议维护者介入：

*   **[#2154 LLM Trace 支持](https://github.com/HKUDS/nanobot/issues/2154)** (Open, 评论 5)：核心可观测性需求，涉及架构级改动，需规划。
*   **[#1922 nanobot-webui](https://github.com/HKUDS/nanobot/issues/1922)** (Open, 评论 6)：社区贡献的 WebUI，需官方评估是否纳入主项目或作为官方推荐方案。
*   **[#1418 DingTalk 显示名称](https://github.com/HKUDS/nanobot/issues/1418)** (Open, 评论 3)：钉钉渠道 Agent 只能看到 staffId 看不到人名，影响体验。

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报 (2026-03-21)

## 1. 今日速览
Zeroclaw 项目今日处于**极高活跃度**状态，过去 24 小时内处理了 100 个 Issues/PRs 的更新（包括创建和关闭），并连续发布了 10 个版本迭代。项目正处于 `v0.5.2` 至 `v0.5.4` 的快速迭代期，重点修复了通道交互、内存架构及提供商兼容性问题。从社区反馈看，用户对项目发展的参与度极高，同时也暴露了关于“安全策略限制过严”与“功能缺失”的核心矛盾。

## 2. 版本发布
今日发布了 10 个版本，正式版 `v0.5.4`, `v0.5.3`, `v0.5.2` 及其对应的 beta 版本。

*   **[v0.5.4](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.5.4)** (最新正式版)
    *   **核心更新**：
        *   **Memory (内存)**：新增 `mem0 (OpenMemory)` 后端集成，增强了记忆持久化能力。
        *   **Channel (通道)**：增强 QQ 频道支持富媒体和定时传送；Slack 通道新增“回应”支持。
        *   **Providers (提供商)**：新增 `Avian` 作为 OpenAI 兼容提供商。
        *   **Tools (工具)**：Jira 工具新增 `myself` 和 `list_projects` 动作；`verifiable_intent` 模块生命周期管理。
        *   **Search (搜索)**：Web 搜索工具现在支持通过别名回退进行提供商路由。

*   **[v0.5.3](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.5.3)**
    *   **核心更新**：新增阿里云百炼 支持网关请求超时配置；CI 增加对 ARMv7 (SBCs) 的交叉编译支持。

*   **[v0.5.2](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.5.2)**
    *   **核心更新**：新增 `/stop` 命令取消飞行中任务；Discord/Mattermost 支持新消息中断；Telegram 通道增加 TTS 语音回复。

## 3. 项目进展
今日合并的重要 PR（部分已随今日 Release 发布）：

*   **[feat(memory): add mem0 (OpenMemory) backend integration](https://github.com/zeroclaw-labs/zeroclaw/pull/3965)**: 已合并。引入了 Mem0Memory 结构体，支持带时间戳和元数据的过滤召回，显著提升了 Agent 的记忆管理能力。
*   **[fix(gemini): use default chat()... add vision support](https://github.com/zeroclaw-labs/zeroclaw/pull/3932)**: 已合并。修复了 Gemini 模型在 Prompt 引导工具调用时的失效问题，并增加了多模态视觉支持。
*   **[fix(approval): auto-approve read-only tools in non-interactive mode](https://github.com/zeroclaw-labs/zeroclaw/pull/4094)**: 已合并。解决了非交互模式下（如 Channel）只读工具（Web搜索等）被静默拒绝的问题，改善了非 CLI 用户体验。
*   **[fix(prompt): respect autonomy level in SafetySection](https://github.com/zeroclaw-labs/zeroclaw/pull/4037)**: 已合并。修复了即便设置完全自主，系统提示词仍强制要求批准破坏性命令的 Bug，确保了 `autonomy.level` 配置生效。

## 4. 社区热点
今日讨论热度最高的话题集中在**安全策略的灵活性**与**特定平台的兼容性**上。

*   **[#1478 [enhancement] 除了安全,什么功能也没有](https://github.com/zeroclaw-labs/zeroclaw/issues/1478)** (评论: 43)
    *   **核心诉求**：用户强烈抱怨 Zeroclaw 的安全限制过于死板（如拒绝安装 ffmpeg），导致其相比 OpenClaw 体积小但“什么也做不了”。
    *   **分析**：这反映了极客/个人开发者用户对于“完全控制权”的渴望，与项目默认的“安全优先”策略存在冲突。这可能是项目定位需要调整的关键信号。

*   **[#3540 [bug] Lark/Feishu channel... can't start](https://github.com/zeroclaw-labs/zeroclaw/issues/3540)** (评论: 8)
    *   **核心问题**：用户编译了 `channel-lark` 特性，但 Feishu 通道无法启动，仅出现 Warn 日志。
    *   **分析**：企业级/国内用户（飞书）的需求正在上升，但集成稳定性有待提高。

## 5. Bug 与稳定性
今日报告的关键 Bug 及修复情况：

*   **[S0 - 严重] [Bug] panic at agent/loop_.rs:1984 — byte index not a char boundary...](https://github.com/zeroclaw-labs/zeroclaw/issues/4062)**
    *   **现象**：当工具调用包含中日韩等多字节 UTF-8 字符且参数超过 300 字节时，Zeroclaw 会发生 Panic 崩溃。
    *   **状态**：已识别为代码截断逻辑缺陷。

*   **[S1 - 阻塞] [Bug] Agent can't find mcp server/tools](https://github.com/zeroclaw-labs/zeroclaw/issues/4042)**
    *   **现象**：配置了 MCP 服务器，Agent 无法调用，且 UI 中不显示。
    *   **相关修复**：PR [#4096](https://github.com/zeroclaw-labs/zeroclaw/pull/4096) 已尝试将 MCP 工具接入 WebSocket 聊天和 Gateway。

*   **[S1 - 阻塞] [Bug] Lark/Feishu channel... can't start](https://github.com/zeroclaw-labs/zeroclaw/issues/3540)**
    *   **现象**：Feishu 通道编译后无法启动。
    *   **状态**：Open issue，待修复。

*   **[S2 - 降级] [Bug] Can't get web search tool working on channels](https://github.com/zeroclaw-labs/zeroclaw/issues/4083)**
    *   **现象**：在 Telegram 等通道无法使用 web_search，但在 CLI 模式正常。
    *   **相关修复**：PR [#4094](https://github.com/zeroclaw-labs/zeroclaw/pull/4094) (自动批准只读工具) 可能已缓解此问题。

## 6. 功能请求与路线图信号
从新提交的 Issues 和 PRs 中观察到的未来趋势：

*   **MCP Server 集成**：Issue [#2856](https://github.com/zeroclaw-labs/zeroclaw/issues/2856) 提出将 OpenClaw 的 MCP Server 配置迁移至 Zeroclaw。PR [#4102](https://github.com/zeroclaw-labs/zeroclaw/pull/4102) 提出增加本地 Whisper STT 提供商，显示用户对“本地化/私有化部署”的强烈需求。
*   **工具与渠道增强**：
    *   PR [#4104](https://github.com/zeroclaw-labs/zeroclaw/pull/4104): 提议集成 wttr.in 天气工具。
    *   PR [#3911](https://github.com/zeroclaw-labs/zeroclaw/pull/3911): 升级 `claude-code` 提供商至完全 Agent 模式，支持 Bash 等工具的自主使用。
*   **成本优化**：Issue [#3892](https://github.com/zeroclaw-labs/zeroclaw/issues/3892) 提出“Token Efficiency”，希望能自动过滤上下文以减少 Token 消耗，这对于本地小显存模型用户至关重要。

## 7. 用户反馈摘要
*   **痛点**：用户对“过度安全”感到沮丧（Issue #1478），认为 Agent 过于被动，甚至拒绝执行基本安装任务。
*   **兼容性**：Windows 用户（Issue #3693）抱怨配置流程混乱，特别是关于 Feishu 和 Web-GUI 的 Feature Flag 选择。
*   **幻觉问题**：有用户报告（Issue #3982）在 Raspberry Pi 上出现严重的系统信息幻觉，模型在命令不存在时胡乱解释。

## 8. 待处理积压
提醒维护者关注以下长期未决或新出现的关键问题：

*   **Branch Sync Issue**: Issue [#4093](https://github.com/zeroclaw-labs/zeroclaw/issues/4093) 指出关于 Provider streaming 的三个 PR (#2868, #2873, #2875) 曾被合并到已删除的 `dev` 分支，导致代码丢失且从未到达 `master`。
*   **Security Regression**: Issue [#3818](https://github.com/zeroclaw-labs/zeroclaw/issues/3818) 指出从 `main` 迁移到 `master` 时丢失了关键的安全参数和 Copilot onboarding provider。
*   **Feature Parity**: Issue [#3839](https://github.com/zeroclaw-labs/zeroclaw/issues/3839) 请求提供与 OpenClaw 的功能对比矩阵。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目日报 (2026-03-21)

## 1. 今日速览
PicoClaw 项目今日呈现**极高活跃度**，处于快速迭代期。过去 24 小时内共处理了 **84 条代码与事务更新**（Issues: 23, PRs: 61），这种提交频率通常发生在重大版本发布前夕或核心功能重构阶段。社区讨论焦点集中在 **Agent 智能体的核心稳定性**（如空响应处理、Cron 任务投递）与 **多模态通道扩展**（如 TTS/ASR、Matrix 加密、OpenAI 兼容接口）。同时，项目发布了新的 Nightly 版本，表明开发者正在积极集成最新修复。

## 2. 版本发布
**版本号**：`v0.2.3-nightly.20260321.100720bb`
- **类型**：Nightly Build (自动构建，可能不稳定)
- **主要更新**：基于 `main` 分支的最新构建，主要包含近期针对 Agent 循环逻辑、OpenAI 兼容性提供商及 Docker 部署的修复。
- **注意事项**：Nightly 版本仅供尝鲜测试，生产环境请谨慎使用。
- **Full Changelog**: [v0.2.3...main](https://github.com/sipeed/picoclaw/compare/v0.2.3...main)

## 3. 项目进展
今日代码合并与修复主要围绕**提高核心 Agent 的可靠性**和**增强连接稳定性**：
*   **[FIX] Agent 空响应与工具调用逻辑优化** (#1818): 修复了当模型返回空响应时误导性的错误提示（此前提示调整 `max_tool_iterations`），将其与真正的工具迭代超限区分开来，并增加了回归测试。
*   **[FIX] Cron 任务响应丢失问题** (#1839): 修复了 Cron 任务在处理完成后无法将响应发送回 Channel 的严重 Bug。原因是 `InboundMessage` 未正确绑定 `Peer` 字段，导致路由失败。
*   **[FIX] CLI 提供商超时设置生效** (#1847): 修复了 `claude-cli`、`codex-cli` 等提供商长期忽略 `request_timeout` 配置的问题，防止子进程无限期挂起。
*   **[DOCS] 文档国际化与准确性** (#1837, #1819): 修复了 25+ 处文档错误，补全了 5 种语言的缺失翻译，并扩展了 12 个频道的接入文档。

## 4. 社区热点
*   **[Feature] 为 PicoClaw 添加 TTS 和 ASR 支持** (#1648)
    *   **状态**: [OPEN] | 👍 16 条评论
    *   **分析**: 这是一个高关注度的高级功能需求。虽然已有相关 PR (#1642)，但尚未集成到网关中。社区正在讨论 TTS/ASR 的架构设计，如何将其无缝接入现有的消息流中是关键。
    *   [链接](https://github.com/sipeed/picoclaw/issues/1648)

*   **[Feature] 添加 WebUI 支持 (正在重构中)** (#806)
    *   **状态**: [OPEN] | 👍 7
    *   **分析**: 降低非技术用户门槛的长期核心需求。作者正在重构中，评论区和 PR 活动表明这是项目迈向大众化的重要一步，目前处于开发攻坚阶段。
    *   [链接](https://github.com/sipeed/picoclaw/issues/806)

*   **[PR] QQ 通道连接稳定性优化** (#1780)
    *   **状态**: [OPEN]
    *   **分析**: 针对国内用户常用的 QQ 通道，开发者提交了重要更新，允许自定义重连间隔、重试次数和速率限制。该 PR 讨论热烈，直接关系着大量国内用户的体验。
    *   [链接](https://github.com/sipeed/picoclaw/pull/1780)

## 5. Bug 与稳定性
*   **[CRITICAL] `deliver=false` 的 Cron 任务静默丢弃 LLM 响应** (#1058)
    *   **严重程度**: 高
    *   **现状**: 已有修复 PR (#1839) 待合并。
    *   **影响**: 定时任务执行成功但用户无感知，造成信息丢失。
    *   [链接](https://github.com/sipeed/picoclaw/issues/1058)

*   **[BUG] 配置加载失败提示 "no API key configured for model: glm-4.7"** (#1491)
    *   **严重程度**: 中
    *   **现状**: 仍未解决。
    *   **影响**: 部分用户（特别是使用 GLM 模型）遇到配置文件无法正确加载的问题，阻塞性较强。
    *   [链接](https://github.com/sipeed/picoclaw/issues/1491)

*   **[BUG] OpenRouter Free 模型调用失败** (#1790)
    *   **严重程度**: 中
    *   **现状**: 刚报出，待修复。
    *   **影响**: 错误地将 `minimax-m2.5:free` 识别为无效 ID，涉及免费模型提供商的兼容性。
    *   [链接](https://github.com/sipeed/picoclaw/issues/1790)

*   **[BUG] aarch64 .deb 安装包依赖问题** (#1763)
    *   **严重程度**: 低
    *   **现状**: 待处理。
    *   **影响**: ARM 架构用户安装 deb 包时遇到依赖冲突。
    *   [链接](https://github.com/sipeed/picoclaw/issues/1763)

## 6. 功能请求与路线图信号
*   **[Channel] 添加 OpenAI API 格式的 channel 支持** (#1738)
    *   **分析**: 这是一个非常实用的“中间件”需求。用户希望将 PicoClaw 作为一个微服务嵌入到现有系统中，通过标准 OpenAI API 格式调用 PicoClaw 的能力（如多平台路由、Agent 能力），而不需要修改现有代码架构。
*   **[Agent] 事件驱动钩子系统** (#1796)
    *   **分析**: 用户希望参考 OpenClaw，增加 Hooks 系统，以支持被动的消息监听和自动化工作流，弥补当前仅支持主动调用和定时的不足。
*   **[Security] 允许 `curl` 工具调用** (#1845)
    *   **分析**: 出于安全考虑，`curl` 在黑名单中，但部分高级用户（如调用 Clawdfeed API）需要此功能。讨论点在于如何在安全性与灵活性之间取得平衡（如配置项控制）。
*   **[Channel] Matrix 加密消息支持** (#1840)
    *   **分析**: 隐私保护需求。已有对应 PR (#1841) 在开发中，支持 E2EE 将提升 Matrix 通道的可用性。

## 7. 用户反馈摘要
*   **痛点 - 门槛与文档**: 新用户普遍反映 "Insufficient guidance" (#1830)。虽然 TUI 很棒，但 WebUI 缺失导致非技术用户（试图在 Android 或 Docker 上运行的人）上手困难。
*   **痛点 - 稳定性**: 长时间任务或网络波动（LLM HTTP 500 错误）导致 Agent 挂起且不重试 (#629) 是主要抱怨点。
*   **场景 - 私有化部署**: 大量用户致力于在局域网环境（如 LM Studio, Ollama）部署 PicoClaw，这解释了为什么对 LM Studio 连接 (#28) 和 OpenAI API 接口 (#1738) 有强烈需求。

## 8. 待处理积压
*   **#28 [Feat Request] LM Studio Easy Connect**: 开放已久，虽有不少讨论但尚未有明确 PR，建议社区开发者优先认领。
*   **#629 [BUG] Retry on LLM failed**: 2 月份提出的重试机制缺失问题，至今未关闭，影响生产环境的鲁棒性。
*   **#1058 [BUG] Cron deliver=false**: 影响严重，虽有 PR 但尚未合并，需优先审查。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 (2026-03-21)

## 1. 今日速览
NanoClaw 项目今日（2026-03-21）展现出**极高的活跃度**，社区贡献热情高涨。在过去 24 小时内，项目共收到了 **25 条 PR** 和 **7 条 Issue**，显示出功能开发正处于快速迭代期。虽然没有新版本发布，但大量新增的 PR 涵盖了从底层基础设施（Web 通道、多租户、Dashboard）到多样化技能扩展（Signal、Twilio、A2A 通信、CLI 工具）的方方面面。项目正致力于解决早期积累的 Bug（如数据库迁移错误），同时通过新增技能快速扩大生态系统覆盖范围。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
尽管今日 **23 个 PR** 仍处于待合并状态，但已有两个关键更新完成合并/关闭，标志着项目功能的完善与稳定性的提升：

*   **基础设施与安全加固 ([#1298](https://github.com/qwibitai/nanoclaw/pull/1298)) - CLOSED/MERGED**
    *   **内容**: 引入了重大的 Web 通道 (`WebClaw`)、可视化 Dashboard 以及多租户支持架构。同时包含了对各通道安全性和竞态条件的修复。
    *   **意义**: 这标志着 NanoClaw 从纯聊天机器人向 **可视化、多租户 SaaS 平台** 迈出了关键一步，极大地提升了项目的可管理性和企业级潜力。
*   **生态兼容性修复 ([#1203](https://github.com/qwibitai/nanoclaw/pull/1203)) - CLOSED/MERGED**
    *   **内容**: 修复了 `ANTHROPIC_BASE_URL` 路径处理问题，确保第三方 API 端点（非官方 Anthropic API）能正确通过子路径调用。
    *   **意义**: 改善了对第三方兼容模型的支持，降低了用户部署成本。

## 4. 社区热点
今日讨论热度集中在 **通信协议的扩展** 与 **工具链的完善** 上，反映出社区对 NanoClaw 成为“全能连接器”的期待：

*   **[#1057](https://github.com/qwibitai/nanoclaw/pull/1057) - feat(skill): add Signal messenger channel**
    *   **热度**: 待审核中的功能 PR。
    *   **分析**: 社区强烈渴望接入更注重隐私的 Signal 协议。该 PR 通过引入 `signal-cli` 后端，旨在实现与 WhatsApp/Telegram 同等的消息处理能力。
*   **[#1298](https://github.com/qwibitai/nanoclaw/pull/1298) - feat: Add web channel, dashboard, and multi-tenant support**
    *   **热度**: 已关闭（推测为合并或完成后关闭）。
    *   **分析**: 作为今日最大的架构变更，Dashboard 的引入解决了长期以来的“黑盒”管理痛点，用户终于可以通过 UI 监控和配置 Agent。
*   **[#1111](https://github.com/qwibitai/nanoclaw/pull/1111) - feat: add API usage tracking**
    *   **热度**: 长期待审核 PR，今日持续活跃。
    *   **分析**: 成本控制是企业级用户的核心诉求。该功能引入了精细的 Token 和成本追踪，是走向生产环境的关键一环。

## 5. Bug 与稳定性
今日报告的 Bug 涉及**数据一致性**和**系统初始化流程**，建议优先关注：

*   **[高严重度] 数据库迁移错误 ([#1272](https://github.com/qwibitai/nanoclaw/issues/1272)) - OPEN**
    *   **问题**: Telegram 迁移脚本将所有聊天类型（包括私聊）错误地标记为 `is_group=1`。这会导致 Agent 将个人私信视为群组处理，破坏了基本的聊天逻辑。
    *   **状态**: 无修复 PR，急需开发者介入编写数据修复脚本。
*   **[中严重度] 跨房间指令串扰 ([#1284](https://github.com/qwibitai/nanoclaw/issues/1284)) - CLOSED**
    *   **问题**: IC01 中继错误地响应了 IC00 房间的指令，原因在于共享了同一个 Operator 账号。
    *   **状态**: 已关闭，推测已通过配置调整或逻辑修复解决。
*   **[中严重度] 缺乏启动前的凭证校验 ([#1289](https://github.com/qwibitai/nanoclaw/issues/1289)) - OPEN**
    *   **问题**: 缺少配置时（如 `TELEGRAM_BOT_TOKEN`）容器仍会启动，导致产生无效或损坏的状态文件。
    *   **状态**: 已有修复 PR [#1290](https://github.com/qwibitai/nanoclaw/pull/1290) 正在审核中。

## 6. 功能请求与路线图信号
从 Issues 和 PRs 中可以窥见 NanoClaw 未来的进化方向：**全平台覆盖** 与 **Agent 互操作性**。

*   **WhatsApp 群组画像**: Issue [#1291](https://github.com/qwibitai/nanoclaw/issues/1291) 提议利用群组描述作为 Agent 的 System Prompt。相关 PR [#1292](https://github.com/qwibitai/nanoclaw/pull/1292) 已提交，预计将纳入下个版本。
*   **Agent 间通信 (A2A)**: PR [#1295](https://github.com/qwibitai/nanoclaw/pull/1295) 提议增加 Agent-to-Agent 通道，允许 Cursor/Windsurf 等工具向 NanoClaw 发送任务。这预示着 NanoClaw 试图成为 AI 工具链的中间件枢纽。
*   **CLI 交互模式**: PR [#1296](https://github.com/qwibitai/nanoclaw/pull/1296) 提出增加 CLI 工具 `claw`，允许用户通过命令行直接与 Agent 交互或管理会话。

## 7. 用户反馈摘要
*   **痛点**:
    *   **文档不一致**: [#1075](https://github.com/qwibitai/nanoclaw/issues/1075) 指出 README 和官网关于 Linux 支持的描述互相矛盾，造成用户困惑。
    *   **新用户引导缺失**: [#1275](https://github.com/qwibitai/nanoclaw/issues/1275) 反映 Bot 被添加到新群组时没有任何提示，用户不知道需要注册，导致体验受阻。
    *   **表情交互盲区**: [#1288](https://github.com/qwibitai/nanoclaw/issues/1288) 提到 Agent 目前无法读取用户在消息上的表情反应，这在即时通讯场景中是一个显著的情感缺失。
*   **正面反馈**: 用户正在积极尝试将 NanoClaw 接入更多平台（Twilio, ProtonMail, White Noise），显示出对核心架构的信任。

## 8. 待处理积压
*   **[#586](https://github.com/qwibitai/nanoclaw/pull/586) - feat: allow agents to send cross-group messages**
    *   创建于 2026-02-28，至今未合并。这是一个非常核心的功能（跨群组通知），长期积压可能意味着实现难度较大或存在架构阻碍，建议维护者优先评估。
*   **[#565](https://github.com/qwibitai/nanoclaw/pull/565) - feat: add PID lockfile guard**
    *   创建于 2026-02-27，用于防止多实例冲突。虽然 Docker 环境下较少见，但在物理机部署中至关重要，建议合并以防数据损坏。

---
**分析总结**: NanoClaw 目前处于**功能爆发期**。虽然 Web/Dashboard 这一重量级功能已经合并，但大量优秀的技能扩展（Signal, Twilio, A2A）正排队等待审核，开发/审核流程可能存在瓶颈。同时，生产环境的稳定性问题（如数据库迁移 Bug）需要尽快解决，以免积累技术债务。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 (2026-03-21)

## 📊 1. 今日速览
NullClaw 项目今日处于**极高活跃度**状态，代码提交与社区互动均表现强劲。
过去 24 小时内共处理了 **38 条 PR**，其中 **24 条已完成合并**，显示项目推进速度极快。Issues 方面处理了 8 条，关闭了 5 个旧案，主要集中在对第三方 LLM 提供商（如 Kimi、GLM）的兼容性修复上。项目核心进展集中在**富媒体消息渠道抽象**、**多模态 LLM 兼容性增强**以及**子代理能力完善**。目前无新版本发布，但鉴于大量功能型 PR 的合并，预计近期可能会有版本更新。

## 📦 2. 版本发布
**暂无新版本发布**。

## 🚀 3. 项目进展
今日合并的 PR 显示项目在**生态系统扩展**和**稳定性**两方面取得了重大突破：

*   **消息渠道架构升级**: PR #596 (Open) 与 PR #593 (Closed) 引入了 `OutboundPayload` 抽象层及腾讯系加密原语，为统一 DingTalk、Lark 等企业级 IM 的交互打下了基础。
*   **国产大模型兼容性补齐**:
    *   **Hunyuan (混元) & Baichuan**: PR #595 正式接入腾讯混元与百川 AI，支持原生工具调用。
    *   **Moonshot Kimi**: PR #578 修复了 `kimi-k2.5` 模型特有的 `reasoning_content` 字段解析失败问题，并修复了该提供商的 API 错误。
    *   **Zhipu (智谱) GLM**: PR #577 为 `z.ai` 和 `glm` 系列模型启用了 `native_tools`，解决了此前无法使用工具的问题。
*   **子代理与 WASM 运行时增强**: PR #558 修复了子代理无法使用主代理技能的问题；PR #568 内置了 `wasm3` 解释器，提供了更快且无需外部依赖的 WebAssembly 运行环境。

## 🔥 4. 社区热点
*   **[PR #596] 抽象富消息端口** (作者: manelsen)
    *   **链接**: [#596](https://github.com/nullclaw/nullclaw/pull/596)
    *   **热度**: ⭐⭐⭐⭐⭐
    *   **分析**: 该 PR 正在重构消息发送机制，旨在统一不同平台（钉钉、飞书）的卡片消息格式。评论活跃度极高，涉及复杂 API 设计，是当前开发的核心焦点。
*   **[Issue #659] 如何在自定义 OpenAI 兼容提供商中启用推理?** (作者: montvid)
    *   **链接**: [#659](https://github.com/nullclaw/nullclaw/issues/659)
    *   **热度**: ⭐⭐⭐
    *   **分析**: 用户反映自定义提供商配置下模型产生的幻觉问题，询问如何启用推理模式。这反映了社区对高级推理模型（DeepSeek R1 等）接入的强烈需求。

## 🐛 5. Bug 与稳定性
*   **[CRITICAL] Tool Parsing JSON Error (#407)**
    *   **状态**: 已关闭
    *   **描述**: 工具解析在处理名称中包含冒号的合法 JSON 时会中断。该问题已在今日修复，维护了工具调用的鲁棒性。
*   **[HIGH] Provider API Errors (#576)**
    *   **状态**: 已修复
    *   **描述**: Moonshot 国际版提供商因无法解析 `reasoning_content` 而崩溃。**Fix PR** #578 已合并。
*   **[MEDIUM] SSE Streams Stalling (#597)**
    *   **状态**: 修复中
    *   **描述**: 针对某些提供商 SSE 流传输会静默挂起的问题，提出了使用 `curl speed-limit` 的检测机制（PR #597 目前仍 Open，待合并）。
*   **[LOW] Timezone Hardcoded UTC (#540)**
    *   **状态**: 已修复
    *   **描述**: 系统提示词中的时区硬编码为 UTC。**Fix PR** #546 已合并，现支持可配置时区。

## 💡 6. 功能请求与路线图信号
*   **Qwen Code Cli 支持 (#647)**
    *   **链接**: [#647](https://github.com/nullclaw/nullclaw/issues/647)
    *   **分析**: 用户请求添加通义千问代码模型作为提供商，理由是额度慷慨。目前尚无对应 PR，是一个潜在的新增点。
*   **Subagent Skill Access (#553)**
    *   **链接**: [#553](https://github.com/nullclaw/nullclaw/issues/553)
    *   **分析**: 用户希望子代理能继承主代理的技能。**信号确认**：PR #558 已合并并修复了此功能，说明该需求已被纳入且完成。

## 🗣️ 7. 用户反馈摘要
*   **痛点**: 多个 Issue 反映国内大模型 API 的非标准响应格式（如 `reasoning_content` 字段、数组类型的 `content`）导致解析失败。用户强烈希望能无缝接入 DeepSeek R1、Kimi 等推理模型。
*   **场景**: 用户倾向于使用容器化部署，并且在尝试将 NullClaw 与 OTel (OpenTelemetry) 集成时遇到了配置连通性问题。

## 🗄️ 8. 待处理积压
*   **[Issue #638] Otel diagnostics issue**
    *   **链接**: [#638](https://github.com/nullclaw/nullclaw/issues/638)
    *   **提醒**: 关于 Open Telemetry 诊断功能的连通性问题，已持续两天且有 8 条评论，技术支持需介入排查网络或配置层面的阻碍。
*   **[PR #597] Stalled SSE streams fix**
    *   **链接**: [#597](https://github.com/nullclaw/nullclaw/pull/597)
    *   **提醒**: 这是一个关于稳定性修复的重要 PR，目前仍处于 Open 状态，建议尽快合并以解决生产环境中的挂起问题。

---
*日报生成时间: 2026-03-21*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

你好！我是 IronClaw (nearai/ironclaw) 开源项目的 AI 分析师。以下是根据 **2026-03-21** 的 GitHub 数据生成的项目动态日报。

---

### 📅 IronClaw 项目日报 | 2026-03-21

#### 1. 今日速览
IronClaw 项目今日处于**极高活跃度**状态。过去 24 小时内共处理了 **91** 个代码和问题更新（41 个 Issues，50 个 PRs），显示出强劲的开发迭代速度。
*   **核心进展**：项目刚刚发布了 **v0.21.0** 版本，引入了 LRU 缓存和 Webhook 支持等关键性能与功能特性。
*   **安全焦点**：自动化 CI 发现并标记了 4 个 **Critical/High** 严重级别的安全问题，主要集中在并发竞态条件（TOCTOU）和授权绕过风险上，需引起高度重视。
*   **代码质量**：社区贡献了大量工具链修复（如 Dockerfile、Cron 格式、OAuth），同时核心团队正大力推进大型 UX 改造和会话导入功能。

---

#### 2. 版本发布
**v0.21.0** (发布于: 2026-03-20)
本次迭代主要侧重于任务恢复机制、搜索性能提升及集成能力扩展。
*   **新增功能**：
    *   **故障恢复结构化交付**：为失败或卡住的任务添加了结构化的回退交付物 ([#236](https://github.com/nearai/ironclaw/pull/236))，提高了任务系统的健壮性。
    *   **搜索性能优化**：引入了 **LRU (最近最少使用) 嵌入缓存** 用于工作区搜索 ([#1423](https://github.com/nearai/ironclaw/pull/1423))，将显著降低向量数据库的调用开销。
    *   **Webhook 回调**：支持通过 Webhook 回调接收中继事件 ([#1254](https://github.com/nearai/ironclaw/pull/1423))，增强了外部系统的集成能力。
*   **潜在风险**：Release Notes 截断处包含未显示的链接，建议用户查看完整 Changelog 确认是否有其他隐藏的破坏性变更。

---

#### 3. 项目进展

今日合并和关闭的 PR 显示项目在**基础稳定性**和**开发者体验**上有明显提升：

*   **安全与并发修复**：
    *   修复了 **跨频道审批线程劫持** 漏洞，防止一个频道的消息劫持其他频道的审批权限 ([#1495](https://github.com/nearai/ironclaw/pull/1495))。
    *   解决了审批线程解析中的**锁竞争**问题 ([#1497](https://github.com/nearai/ironclaw/pull/1497))。
*   **工具链与构建修复**：
    *   修复了 Dockerfile 构建失败问题（缺少 build.rs）([#332](https://github.com/nearai/ironclaw/pull/332))。
    *   修复了 Cron 任务的 5 字段与 6 字段格式不兼容问题 ([#668](https://github.com/nearai/ironclaw/pull/668))。
    *   优化了 WASM 工具的 schema 提取逻辑 ([#343](https://github.com/nearai/ironclaw/pull/343))。
*   **配置与环境**：
    *   清理了 bootstrap `.env` 中的冗余 LLM 配置 ([#1448](https://github.com/nearai/ironclaw/pull/1448))，简化了初始设置。

---

#### 4. 社区热点

今日讨论热度最高的问题主要集中在**升级障碍**和**核心功能缺失**：

*   **[#1328](https://github.com/nearai/ironclaw/issues/1328) - 升级失败:** 从 v0.18.0 升级至 v0.19.0 时，由于 Postgres 数据库迁移脚本的 Checksum 不匹配导致启动失败。这是典型的数据库迁移管理问题，影响已有用户升级。
*   **[#902](https://github.com/nearai/ironclaw/issues/902) - OAuth 屏蔽:** 用户反馈 Google Workspace 工具在 OAuth 时被 Google 屏蔽。这涉及到 IronClaw 的应用注册与 Google 安全策略的兼容性。
*   **[#1174](https://github.com/nearai/ironclaw/issues/1174) - 文档缺失:** 用户抱怨找不到关于如何配置、工具限制和技能的文档，反映出项目文档建设滞后于功能开发。

---

#### 5. Bug 与稳定性

今日由 CI Bot 和用户报告了多个**严重** Bug，需立即处理：

*   **[CRITICAL] 并发安全漏洞:**
    *   **TOCTOU 竞态条件** ([#1486](https://github.com/nearai/ironclaw/issues/1486)): 审批线程解析中存在检查与使用的时间竞争。
    *   **授权绕过** ([#1485](https://github.com/nearai/ironclaw/issues/1485)): 跨频道审批线程可能被劫持。
    *   **已有 Fix**: 是，见 PR #1495, #1497。
*   **[CRITICAL] 性能崩溃:**
    *   **Embedding 克隆问题** ([#1429](https://github.com/nearai/ironclaw/issues/1429)): 缓存命中时发生克隆操作，可能导致高频操作下的性能下降。
*   **[HIGH] 数据一致性与逻辑错误:**
    *   **不完整的 Fallback 逻辑** ([#1487](https://github.com/nearai/ironclaw/issues/1487)): 当审批线程不存在时，Fallback 逻辑不完整。
    *   **SSRF 风险** ([#1103](https://github.com/nearai/ironclaw/issues/1103)): 配置的 Embedding Base URL 缺乏验证，存在服务端请求伪造风险。
    *   **Gemini 函数调用失败** ([#1510](https://github.com/nearai/ironclaw/issues/1510)): 新版报告 Gemini 3.1 Flash 模型在工具调用时缺少 `thought_signature` 导致请求失败。

---

#### 6. 功能请求与路线图信号

从活跃的 Issues 中，我们可以窥见项目未来的路线图：

*   **工作区与存储演进**:
    *   [#1504](https://github.com/nearai/ironclaw/issues/1504): **重大变革提议** - 使工作区成为技能存储的唯一真实来源，取代文件系统。这将极大改变 IronClaw 的数据管理架构。
*   **可观测性增强**:
    *   [#1493](https://github.com/nearai/ironclaw/issues/1493): 请求在 Web Gateway 添加调试面板，以查看系统提示、工具参数和 Token 计数。
*   **协议支持扩展**:
    *   [#1506](https://github.com/nearai/ironclaw/issues/1506): 提议支持 **Agent Client Protocol (ACP)**，允许代理任务委托给任何兼容的编码代理（如 Cursor 等）。
    *   [#1501](https://github.com/nearai/ironclaw/issues/1501): 请求添加 **AWS Bedrock** 作为原生的 Embedding 提供商。

---

#### 7. 用户反馈摘要

*   **痛点**:
    *   **Google 集成不稳定**: 多个 Issues (#1500, #1502, #1503) 指出 Google Slides 和 Auth 在连续使用多个工具时存在链接失效和授权问题。
    *   **数据库脆弱性**: [#1278](https://github.com/nearai/ironclaw/issues/1278) 用户抱怨数据库重置会导致配置文件（如 MEMORY.md）永久丢失，建议支持磁盘自动导出。
*   **期望**:
    *   用户希望拥有**浅色主题** (#761) 和**邮箱注册** (#1494) 方式，以适应更多样化的使用环境。

---

#### 8. 待处理积压

以下为已提出一段时间但尚未完全解决的高优先级/大型任务：

*   **[#1277](https://github.com/nearai/ironclaw/pull/1277) - UX 大修**: 这是一个进行中的超大型 PR (XL)，涉及设计系统、入职流程和 Web 界面打磨。虽然未合并，但代表了未来 UI 的方向。
*   **[#1498](https://github.com/nearai/ironclaw/pull/1498) / [#1505](https://github.com/nearai/ironclaw/pull/1505) - 历史记录导入**: 分别针对 Claude 和 OpenAI 的对话历史导入功能正在开发中，这是用户迁移工作流的关键功能。
*   **[#1151](https://github.com/nearai/ironclaw/pull/1151) 相关**: 数据库迁移脚本 Checksum 问题 (#1328) 的根源在于此 PR，需尽快发布修复版本或迁移指南。

---
*日报生成结束。数据基于 2026-03-21 00:00 - 24:00 (UTC) 的 GitHub 活动。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 (2026-03-21)

## 1. 今日速览
LobsterAI 项目今日迎来了**极高活跃度**的开发与社区互动。过去 24 小时内产生了 **35 条新 Issues** 和 **26 条 PRs**，显示项目正处于快速迭代与问题修复的并发期。虽然发布了 `2026.3.20` 版本修复了构建依赖问题，但社区反馈显示该版本引入了较为严重的服务稳定性与多线程/数据一致性 Bug。核心关注点集中在 OpenClaw 网关的频繁重启、IM 通道的异常行为以及数据安全性上。

## 2. 版本发布
- **版本号**：`2026.3.20`
- **发布时间**：2026-03-20
- **核心更新**：
  - **修复构建问题**：修复了 OpenClaw 运行时因错误 stubbing `playwright-core` 和 `pdfjs-dist` 导致的潜在问题 ([PR #548](https://github.com/netease-youdao/LobsterAI/pull/548))。
- **注意事项**：虽然构建层面有所修复，但该版本在用户侧引发了较多关于网关稳定性的反馈，建议团队关注后续 Hotfix。

## 3. 项目进展
今日共有 11 个 PR 被合并或关闭，显著推动了工程的健壮性与基础设施：

- **工程化基础设施**：
  - [PR #589](https://github.com/netease-youdao/LobsterAI/pull/589) (OPEN): 计划搭建完整的 CI/CD 流水线、安全扫描及代码格式化配置，这将大幅提升项目的长期可维护性。
  - [PR #569](https://github.com/netease-youdao/LobsterAI/pull/569) (CLOSED): **日志系统重构**。实现日志按日切割（Daily Rotation）、单文件 80MB 限制、保留 7 天，并支持日志导出，极大优化了问题排查能力。
  - [PR #591](https://github.com/netease-youdao/LobsterAI/pull/591) (CLOSED): **安全性增强**。移除了 `openclaw.json` 中的明文密钥，改为环境变量注入方式，提升了本地存储的安全性。

- **核心体验修复**：
  - [PR #565](https://github.com/netease-youdao/LobsterAI/pull/565) (CLOSED): 修复了手动停止任务时错误显示 `[任务超时]` 提示的逻辑 Bug。
  - [PR #520](https://github.com/netease-youdao/LobsterAI/pull/520) (CLOSED): 修复了 macOS 清理 stub 包后导致的签名失败问题。

- **新功能接入**：
  - [PR #558](https://github.com/netease-youdao/LobsterAI/pull/558) (CLOSED): **飞书机器人一键配置**。新增扫码创建机器人功能，极大降低了企业 IM 的接入门槛。
  - [PR #556](https://github.com/netease-youdao/LobsterAI/pull/556) (CLOSED): **泡泡 IM WebSocket 长连接**。新增 WebSocket 模式作为 Webhook 的替代方案，简化了配置并提升了连接稳定性。

## 4. 社区热点
今日讨论热度最高的议题集中在由于新版本引发的稳定性问题及潜在安全漏洞：

- **网关频繁重启** ([Issue #540](https://github.com/netease-youdao/LobsterAI/issues/540), [Issue #572](https://github.com/netease-youdao/LobsterAI/issues/572)): 多位用户反馈 3.19/3.20 版本中 OpenClaw Gateway 每隔几十秒自动重启，导致无法使用，这是目前最高优的痛点。
- **数据安全与隐私**:
  - **路径遍历漏洞** ([Issue #543](https://github.com/netease-youdao/LobsterAI/issues/543)): 社区成员指出存在高危路径遍历风险，可导致任意文件读取。
  - **会话串号** ([Issue #561](https://github.com/netease-youdao/LobsterAI/issues/561)): 出现严重的“在个人 LobsterAI 中看到他人对话”问题，引发了用户恐慌。
- **IM 通道异常**: [Issue #594](https://github.com/netease-youdao/LobsterAI/issues/594) 反映从飞书发送消息时，客户端会自动频繁发送历史提问；[Issue #511](https://github.com/netease-youdao/LobsterAI/issues/511) 指出飞书机器人不回复但企微正常。

## 5. Bug 与稳定性
今日报告的 Bug 数量激增，部分属于严重等级：

- **严重**:
  - **Windows 开机启动失败** ([Issue #595](https://github.com/netease-youdao/LobsterAI/issues/595)): 进程启动 3 秒后退出且无日志。
  - **会话删除后状态残留/无法发送** ([Issue #570](https://github.com/netease-youdao/LobsterAI/issues/570)): 删除正在运行的对话后，输入卡死在 "Stop" 状态。已有 PR [554](https://github.com/netease-youdao/LobsterAI/pull/554) 尝试修复。
  - **内存泄漏** ([Issue #571](https://github.com/netease-youdao/LobsterAI/issues/571)): `stoppedSessions` 集合无限增长导致长期运行内存占用飙升。
  - **路径遍历漏洞** ([Issue #543](https://github.com/netease-youdao/LobsterAI/issues/543)): 代码中直接使用用户参数构建路径，未做校验。
  - **主线程阻塞** ([Issue #562](https://github.com/netease-youdao/LobsterAI/issues/562)): SQLite 同步写入阻塞主进程。已有 PR [573](https://github.com/netease-youdao/LobsterAI/pull/573) 提交异步 IO 方案。

- **中等**:
  - Mac (Intel) 重启后图标变问号 ([Issue #551](https://github.com/netease-youdao/LobsterAI/issues/551))。
  - 模型配置热更新失效，切换模型后仍调用旧模型 ([Issue #585](https://github.com/netease-youdao/LobsterAI/issues/585))。
  - 对话标题显示乱码 ([Issue #563](https://github.com/netease-youdao/LobsterAI/issues/563))。

## 6. 功能请求与路线图信号
从活跃的 Issues 和 PRs 中可以窥见未来的开发方向：

- **成本监控**: [Issue #582](https://github.com/netease-youdao/LobsterAI/issues/582) 请求增加各模型 Token 用量统计功能，这对于企业用户控制成本至关重要。
- **离线部署**: [Issue #587](https://github.com/netease-youdao/LobsterAI/issues/587) 提出对企业内网离线环境的需求。
- **Agent 人设**: [PR #544](https://github.com/netease-youdao/LobsterAI/pull/544) 正在添加“技术专家”、“虚拟女友”等人设选择功能，旨在增强 C 端用户的趣味性。
- **引用系统**: [PR #557](https://github.com/netease-youdao/LobsterAI/pull/557) 正在优化附件 @mention 引用系统，对标 Claude Code/Cursor，提升多模态交互体验。
- **技能操作优化**: [Issue #567](https://github.com/netease-youdao/LobsterAI/issues/567) 希望在输入框输入 `/` 时能快速选择已有技能。

## 7. 用户反馈摘要
- **痛点**：
  - **工作空间概念困惑** ([Issue #579](https://github.com/netease-youdao/LobsterAI/issues/579)): 用户误以为工作区仅用于读取，实际上会在该目录创建文件（`.openclaw`, `SOUL.md`），且难以重置。
  - **配置隐蔽** ([Issue #588](https://github.com/netease-youdao/LobsterAI/issues/588)): 图片输入配置入口太深，难以发现。
  - **错误提示误导** ([Issue #592](https://github.com/netease-youdao/LobsterAI/issues/592)): 模型连接测试显示失败，实际已可用（GLM-4.7 vs GLM-5）。
- **稳定性恐慌**: 频繁的自动重启和“串号”问题严重影响了用户对软件安全性的信任。

## 8. 待处理积压
- **长期未解决**: [Issue #551](https://github.com/netease-youdao/LobsterAI/issues/551) (Mac 图标问号) 和 [Issue #562](https://github.com/netease-youdao/LobsterAI/issues/562) (SQLite 阻塞) 虽有讨论或 PR，但尚未完全合入发布版，需持续关注。
- **高风险 PR 审查**: [PR #576](https://github.com/netease-youdao/LobsterAI/pull/576) 正在尝试解决 Windows 网关启动可靠性问题，这对于修复大量 Windows 用户的崩溃反馈至关重要，建议优先 Review。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw 项目日报 - 2026-03-21

## 1. 今日速览
TinyClaw 项目在 2026-03-21 迎来了重要的里程碑更新 **v0.0.16**，标志着项目从“配置驱动”转向“开箱即用”阶段。过去 24 小时内，项目活跃度**极高**：虽然没有新的 Issues 提出，但代码库经历了大规模重构，5 个 Pull Requests 中有 4 个已成功合并关闭。核心开发重点集中在 CLI 体验的极简化（Zero-Config）以及 Web 端交互的重构上。目前仅有 1 个关于新增 LLM 提供商的 PR 处于待合并状态，项目整体迭代速度与健康度表现优异。

## 2. 版本发布
**v0.0.16 (最新发布)**
- **核心亮点：Zero-Config Onboarding（零配置入门）**
  - **彻底简化首次运行体验**：移除了原有的设置向导，用户现在只需运行 `tinyagi` 命令即可自动创建默认设置、引导代理工作区目录（`~/tinyagi-workspace`）、检查依赖并启动守护进程。
  - **即插即用**：默认配置下无需手动设置即可获得完全功能的守护进程，大幅降低了新用户的上手门槛。
  - **变更影响**：这是一个破坏性较小的用户体验更新，旨在减少“安装-运行”之间的摩擦。现有用户升级后可能需要关注默认工作区路径的变化。

## 3. 项目进展
今日合并的 4 个 PR 展示了项目在底层架构和前端体验上的双重推进：
*   **[CLOSED] #244: Streamline onboarding to single 'tinyagi' command** ([链接](https://github.com/TinyAGI/tinyagi/pull/244))
    *   **推进内容**：直接对应 v0.0.16 版本的核心功能。移除了 Setup Wizard，实现了依赖自动检查，确保 `tinyagi` 命令能直接启动。
*   **[CLOSED] #242: Extract CLI logic into adapter pattern** ([链接](https://github.com/TinyAGI/tinyagi/pull/242))
    *   **推进内容**：核心代码重构。将 `invoke.ts` 中的 CLI 调用逻辑提取为独立的适配器模块（`AgentAdapter`），支持不同 Provider 自动注册。这使得 `invoke.ts` 文件大幅精简，提升了代码的可维护性和扩展性。
*   **[CLOSED] #245: Redesign SSE events and extract page components** ([链接](https://github.com/TinyAGI/tinyagi/pull/245))
    *   **推进内容**：前端与通信层优化。简化了事件系统命名（移除 `chain_*`，改为更清晰的 `message:*` 和 `agent:*`），并将 Office 页面重构为可组合的 Hooks 和组件。
*   **[CLOSED] #212: Redesign the live office workspace** ([链接](https://github.com/TinyAGI/tinyagi/pull/212))
    *   **推进内容**：UI/UX 重大升级。重新设计了 `/office` 工作区的实时交互体验，配合 #245 提升了前端整体架构质量。

## 4. 社区热点
今日社区讨论主要集中在“自动化”与“架构优化”上，未发现激烈的争议或负面反馈。
*   **最热 PR**：#244 (Zero-Config) 虽然评论数较少，但作为版本核心亮点，其理念“无需向导，开箱即用”是社区最受关注的改进点。
*   **待关注 PR**：#243 (Novita AI Provider) 目前处于开放状态，作为对 LLM 能力的扩展，吸引了模型服务商集成者的目光。

## 5. Bug 与稳定性
*   **今日无新增 Bug 报告**：过去 24 小时内没有新提交的 Issues。
*   **稳定性提升**：通过 #242 的重构，CLI 逻辑更加模块化，理论上降低了因单一文件逻辑过重导致的维护风险；#245 的事件系统重命名有助于减少未来开发中的逻辑混淆。

## 6. 功能请求与路线图信号
*   **新增 LLM 提供商支持**：**PR #243** ([链接](https://github.com/TinyAGI/tinyagi/pull/243)) 由 Alex-wuhu 提出，请求添加 **Novita AI** 作为内置提供商。
    *   **分析**：该 PR 复用了现有的 Codex harness（OpenAI 兼容 API），这表明项目路线图正在积极吸纳兼容 OpenAI 协议的生态伙伴，丰富用户的模型选择。
*   **前端体验现代化**：从 #212 和 #245 的合并来看，项目正在加强对 Web 端 `/office` 工作区的投入，未来可能会看到更多基于组件化的 UI 更新。

## 7. 用户反馈摘要
由于今日无新增 Issues 和 PR 评论，用户反馈主要体现为维护者的主动改进：
*   **痛点解决**：之前的用户痛点可能是“配置繁琐”和“启动流程不直观”，v0.0.16 版本直接回应了这一痛点，通过 Zero-Config 极大改善了体验。
*   **正面期待**：社区对 Novita AI 的集成（PR #243）持开放态度，目前代码已就绪，等待合并测试。

## 8. 待处理积压
*   **需关注 PR**：
    *   **#243 [OPEN] feat: add Novita AI as a built-in LLM provider** ([链接](https://github.com/TinyAGI/tinyagi/pull/243))
    *   **状态**：代码变更已提交，目前处于待合并状态。
    *   **建议**：维护者应尽快审查该 PR 的集成测试情况，以确保新 Provider 能在 v0.0.16 之后的版本中顺利上线。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 (2026-03-21)

**报告生成时间**：2026-03-21
**数据来源**：GitHub.com/moltis-org/moltis
**分析师**：AI 智能体与个人助手领域专家

---

### 1. 今日速览
Moltis 项目在过去 24 小时内显示出**中等活跃度**。虽然代码层面暂无新版本发布，但社区维护积极，共处理了 9 条更新记录。项目当前处于**功能迭代与 Bug 修复并行**的阶段：核心功能方面正在推进 Google Gemini 提供商的集成及 Windows 平台的兼容性修复；依赖库管理方面，Dependabot 自动更新了包括 `quinn-proto` 在内的关键依赖。值得注意的是，今日新增了两个关于 Windows 平台兼容性的 Bug（#457, #458），以及一个长期活跃的功能请求（Matrix Support），这表明跨平台稳定性和协议互操作性是当前社区关注的焦点。

### 2. 版本发布
**状态**：无新版本发布。
当前代码库处于活跃开发状态，多个 PR 处于待合并状态，建议关注后续 Release Notes 以获取正式变更通知。

### 3. 项目进展
今日虽无 PR 直接合并，但以下代码提交正在推进中，预示着项目功能的演进：
*   **AI 供应商扩展**：PR #33 正在添加 **Google Gemini** 原生支持，包含 API Key 和 OAuth 认证，并完善了工具调用功能，这将显著增强 Moltis 的模型接入能力。
    *   *链接*：[moltis-org/moltis#33](https://github.com/moltis-org/moltis/pull/33)
*   **安全性增强**：PR #449 优化了网关层的配置访问，增加了对敏感信息的脱敏处理，提升了系统安全性。
    *   *链接*：[moltis-org/moltis#449](https://github.com/moltis-org/moltis/pull/449)
*   **跨平台修复**：PR #436 针对性解决了 Windows 下的文件锁死问题，通过调整文件读写逻辑修复了 `LockFileEx os error 5`，这对 Windows 用户体验至关重要。
    *   *链接*：[moltis-org/moltis#436](https://github.com/moltis-org/moltis/pull/436)
*   **依赖维护**：PR #456 和 #390 持续更新 Rust 生态依赖（`tar`, `aws-lc-sys`, `quinn-proto`），确保底层库的安全性和稳定性。

### 4. 社区热点
*   **[#233: Matrix Support](https://github.com/moltis-org/moltis/issues/233)**
    *   **热度**：👍 1，评论 2 条。虽然创建于 2 月底，但在过去 24 小时内有更新。
    *   **分析**：这是一个协议互通性的 Feature Request。用户希望 Moltis 能支持 Matrix 协议。这反映了用户对于将 Moltis 接入去中心化通信网络的强烈需求，是构建通用 AI Agent 入口的重要一步。

### 5. Bug 与稳定性
今日新增 2 个 Bug 报告，均涉及 Windows/配置导入流程，严重程度：**中等**：
*   **[#457: windows installer handler.sh not found](https://github.com/moltis-org/moltis/issues/457)**
    *   **描述**：Windows 安装程序报错找不到 `handler.sh`。
    *   **分析**：典型的脚本跨平台兼容问题，可能是安装脚本未正确区分 Windows Shell 环境。
*   **[#458: Onboarding - Config examples missing when importing from openclaw](https://github.com/moltis-org/moltis/issues/458)**
    *   **描述**：从 openclaw 导入配置时，`moltis.toml` 中缺少配置示例，导致新用户上手困难。
    *   **分析**：属于用户体验（UX）缺失，可能影响新用户的转化率。

### 6. 功能请求与路线图信号
*   **[feat(agents): add Google Gemini provider](https://github.com/moltis-org/moltis/pull/33)**：该 PR 已存在较长时间且仍在活跃更新（最新 2026-03-20），暗示 Google Gemini 集成是高优先级路线图项目。
*   **[[Feature]: Matrix Support](https://github.com/moltis-org/moltis/issues/233)**：目前处于 OPEN 状态且讨论较少，可能需要更多社区推动才能进入开发阶段。

### 7. 用户反馈摘要
*   **痛点**：Windows 用户的体验目前较为粗糙，不仅存在文件锁死问题，还有安装脚本错误。
*   **场景**：用户正在尝试从其他工具（如 openclaw）迁移配置，这表明 Moltis 正在被考虑作为现有工作流的替代品，但迁移过程中的配置文档缺失阻碍了这一过程。
*   **期待**：社区期待更广泛的协议支持（Matrix）和更完善的 AI 模型接入（Google Gemini）。

### 8. 待处理积压
*   **长期开放的 PR**：
    *   **[#436 fix(sessions): ... to fix Windows file lock](https://github.com/moltis-org/moltis/pull/436)**：创建于 3 月 14 日，目前仍在 OPEN 状态。鉴于其修复了严重的 Windows 崩溃问题，建议优先合并。
    *   **[#33 feat(agents): add Google Gemini](https://github.com/moltis-org/moltis/pull/33)**：创建于 2 月 5 日，功能虽大但进度缓慢，建议维护者评估是否需要协助或拆分任务。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报：2026-03-21

**数据概览**
*   **活跃度评估：** 🟢 **极高**
    *   过去 24 小时内有 **50 条 PR** 和 **50 条 Issue** 发生变动，社区贡献者提交活跃，修复速度与反馈速度均处于高位。
*   **版本发布：** v0.1.0.post1

---

### 1. 今日速览
CoPaw 项目今日迎来了极高频次的开发活动，共有 50 个 PR 处于活跃状态（其中 27 个待合并），这表明项目正处于快速迭代阶段。尽管刚刚发布了 v0.1.0.post1 版本，但团队和社区迅速跟进了一系列针对关键功能的修复，包括内存管理时区问题、MCP 集成改进以及 Windows 安装体验的优化。社区讨论热度集中在 v0.1.0 版本的兼容性问题和多智能体编排的架构诉求上。

### 2. 版本发布
**v0.1.0.post1** ([Release Link](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0.post1))
*   **核心修复：**
    *   **网络层稳定性：** 新增针对 Anthropic API HTTP 529 错误（过载）的重试机制 ([PR #1891](https://github.com/agentscope-ai/CoPaw/pull/1891))，这解决了用户在使用 Claude 模型时偶发的连接失败问题。
    *   **Token 统计：** 改进了 Token 使用量的统计逻辑。

### 3. 项目进展
今日多个关键功能的 PR 正在积极审查或合并中，项目在以下几个方面取得了实质性进展：

*   **MCP (Model Context Protocol) 深度集成：**
    *   [PR #1978](https://github.com/agentscope-ai/CoPaw/pull/1978) 引入了 MCP 导入预览和运行时状态诊断功能，大幅提升了调试可见性。
    *   [PR #1883](https://github.com/agentscope-ai/CoPaw/pull/1883) 添加了 Agents Square 的源浏览和导入流程，为生态扩展做准备。
*   **运行时稳定性增强：**
    *   [PR #1977](https://github.com/agentscope-ai/CoPaw/pull/1977) 加强了 MCP 拆解和定时任务/通道异常处理的健壮性，减少了后台任务崩溃的风险。
    *   [PR #1814](https://github.com/agentscope-ai/CoPaw/pull/1814) 修复了 ReMe 内存总结中的时区传递问题，确保日志时间对用户准确。
*   **控制台与 Web 体验：**
    *   [PR #1791](https://github.com/agentscope-ai/CoPaw/pull/1791) 支持为 Agent 上传头像，增强了多 Agent 视觉识别度。
    *   [PR #1989](https://github.com/agentscope-ai/CoPaw/pull/1989) 增加了 Web 端账号管理（修改用户名/密码）和登录页深色模式支持。

### 4. 社区热点
*   **🔥 架构争议：多 Agent 编排缺失**
    *   **Issue [#1990](https://github.com/agentscope-ai/CoPaw/issues/1990)**：用户强烈质疑为什么 CoPaw 不像其他框架一样支持“主 Agent 自动调度 Sub Agent”，目前需要手动复制粘贴切换。这反映了用户从单 Agent 向 Multi-Agent 工作流过渡时的核心痛点。
    *   **Issue [#1587](https://github.com/agentscope-ai/CoPaw/issues/1587)**：类似的关于多 Agent 支持的讨论依然在被顶起，显示出这一功能的迫切性。
*   **🔥 文档与本地化**
    *   **Issue [#1586](https://github.com/agentscope-ai/CoPaw/issues/1586)**：社区呼吁加强中文适配（文档、更新日志），指出当前主要用户群为中文用户，但文档体验偏向英文。

### 5. Bug 与稳定性
*   **🔴 严重：Task 取消异常**
    *   **Issue [#1976](https://github.com/agentscope-ai/CoPaw/issues/1976)**：报告了 `RuntimeError: Task has been cancelled` 错误，虽然开发者标记为已在 #1956 修复，但大量用户仍在反馈，暗示该问题可能在不同场景下仍有复现（11条评论）。
*   **🟠 中等：飞书/音频处理 Bug**
    *   **Issue [#1835](https://github.com/agentscope-ai/CoPaw/issues/1835)**：使用飞书发送音频后，后续所有交互（包括文字）均报错 `No connection adapters found for 'file://...'`。这是典型的本地文件路径处理与远程通道不兼容问题。
*   **🟠 中等：循环引用导致的 CPU 100%**
    *   **Issue [#1774](https://github.com/agentscope-ai/CoPaw/issues/1774)**：内存压缩钩子在某些后台任务触发下陷入死循环，导致 CPU 占用飙升。
*   **🟠 中等：Docker 数据丢失**
    *   **Issue [#1752](https://github.com/agentscope-ai/CoPaw/issues/1752)**：使用创空间部署后工作区整体文件夹丢失，涉及数据持久化的严重问题。
*   **✅ 已修复：通道消息分段**
    *   [PR #1937](https://github.com/agentscope-ai/CoPaw/pull/1937) 修复了 QQ 和企微通道在长文本消息下的截断/报错问题。

### 6. 功能请求与路线图信号
*   **Token 细粒度统计：** [Issue #1751](https://github.com/agentscope-ai/CoPaw/issues/1751) 请求按“会话维度”统计 Token 消耗，而不仅仅是全局统计。
*   **历史对话搜索：** [Issue #1578](https://github.com/agentscope-ai/CoPaw/issues/1578) 请求增加历史记录搜索功能，随着使用时间增长，检索效率成为瓶颈。
*   **自定义通道支持：** [Issue #1987](https://github.com/agentscope-ai/CoPaw/issues/1987) 及其对应的 [PR #1991](https://github.com/agentscope-ai/CoPaw/pull/1991) 显示，自定义通道因 `dict` 类型处理不当无法启动，该 PR 正在尝试修复。

### 7. 用户反馈摘要
*   **升级体验不佳：** 多位用户 ([#1555](https://github.com/agentscope-ai/CoPaw/issues/1555), [#1694](https://github.com/agentscope-ai/CoPaw/issues/1694)) 反映 `pip install --upgrade` 升级后出现前端无法打开或依赖冲突问题，Windows 桌面版升级指引缺失 ([#1683](https://github.com/agentscope-ai/CoPaw/issues/1683))。
*   **网络与依赖问题：** 用户对从 `huggingface.co` 下载配置文件导致的网络不可达错误表示困扰 ([#1708](https://github.com/agentscope-ai/CoPaw/issues/1708))。
*   **产品对比情绪：** 部分用户在 [Issue #1551](https://github.com/agentscope-ai/CoPaw/issues/1551) 中将 CoPaw 与 AutoClaw, MaxClaw 对比，批评其缺乏多 Agent 编排、节点管理（手机/电脑）等企业级功能，认为“产品思维不足”。

### 8. 待处理积压
*   **长期 Bug (Memory)：** [Issue #1596](https://github.com/agentscope-ai/CoPaw/issues/1596) 关于记忆压缩机制导致“失忆”和回复延迟的问题，虽然已关闭但似乎仍有用户在 v0.1.x 系列中反馈类似体验。
*   **功能积压：** 增加腾讯 Skillhub 导入支持 ([#1589](https://github.com/agentscope-ai/CoPaw/issues/1589)) 和 browser_use 优化 ([#1565](https://github.com/agentscope-ai/CoPaw/issues/1565)) 目前讨论较少，可能处于积压状态。

---
**分析师备注：**
今日项目非常活跃，大量 `first-time-contributor` 的出现说明社区正在不断扩大。建议维护者重点关注 **v0.1.x 版本的升级稳定性** 和 **多 Agent 编排** 的产品路线图沟通，以回应用户对核心功能的质疑。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目日报 (2026-03-21)

**报告生成时间**：2026-03-21  
**数据来源**：GitHub.com/qhkm/zeptoclaw  
**项目状态**：🟢 正常演进中

---

### 1. 今日速览
ZeptoClaw 项目在过去 24 小时内保持了**活跃的讨论**状态，但代码提交暂缓。今日无 Pull Requests 合并或新版本发布，开发重点似乎处于架构探讨与功能验证阶段。项目新增了 2 个功能导向的 Issue，分别聚焦于底层虚拟化安全与工具链测试规范性。虽然主仓库代码暂未更新，但维护者与社区在 Issue 中的高频互动表明项目正在为下一阶段的迭代进行深度规划。

---

### 2. 版本发布
**暂无新版本发布**

---

### 3. 项目进展
**无代码合并**
今日没有新的 PR 被合并或关闭。虽然缺乏代码层面的直接推进，但新提出的 Issue #391 显示维护者正在积极吸纳 `pi_agent_rust` 项目的评估经验，通过“Cherry-pick（挑选）”模式改进现有工具链，这表明项目正在优化其内部开发与测试流程。

---

### 4. 社区热点
今日最活跃的讨论集中在 **Issue #387**，该话题引发了社区对“Coding Agent”与“Virtual Machine”结合的深度思考。

*   **🔥 核心议题：[feat] Core templates based on Containerfiles mapped-to/launched-in orchestrated Firecracker VM's**
    *   **链接**：[qhkm/zeptoclaw#387](https://github.com/qhkm/zeptoclaw/issues/387)
    *   **热度**：6 条评论，标签为 `[feat]`
    *   **摘要**：作者 `taqtiqa-mark` 提出基于 Firecracker VM 运行 Containerfiles 的核心模板功能，旨在解决“功能蔓延”和“安全面扩大”的问题。该提案具有争议性，试图将各类 Coding Agent Frameworks（如 claude-code, copilot-cli 等）视为运行在节点上的普通应用。
    *   **分析**：这反映出社区对 AI 智能体运行环境**安全性**与**隔离性**的强烈关注。利用 Firecracker 微虚拟机来遏制 AI Agent 可能带来的风险，是当前 AI Infra 领域的前沿探索方向。

---

### 5. Bug 与稳定性
**今日无新增 Bug 报告**
新开放的 Issue 均为功能增强或测试工具优化，未发现关于崩溃、死锁或严重回归问题的报告。

---

### 6. 功能请求与路线图信号
今日新增的两个 Issue 为未来的路线图提供了重要信号：

1.  **微虚拟机架构支持** [qhkm/zeptoclaw#387](https://github.com/qhkm/zeptoclaw/issues/387)  
    *   **信号**：项目可能正在考虑引入或强化 Firecracker 轻量级虚拟机技术，以构建更安全的 Agent 运行沙盒。
2.  **工具链一致性测试** [qhkm/zeptoclaw#391](https://github.com/qhkm/zeptoclaw/issues/391)  
    *   **信号**：维护者 (`qhkm`) 正着手引入 JSON Fixture 运行器，用于工具的回归测试。这意味着未来的版本将更加注重工具调用的准确性与可测试性，可能会伴随引入新的测试框架。

---

### 7. 用户反馈摘要
由于今日新增 Issue 主要由核心贡献者提出，反馈主要体现为**技术层面的改进意图**：
*   **痛点**：现有的 Coding Agent 框架过于庞杂，安全边界不清晰（来自 #387）。
*   **改进需求**：测试工具过于依赖 Rust 代码编写，希望通过 JSON Fixture 降低测试门槛（来自 #391）。
*   **决策倾向**：对于 `pi_agent_rust` 的评估结果是“不采纳整体，仅采纳模式”，显示出项目在架构选型上保持了高度的克制和选择性。

---

### 8. 待处理积压
*   **关注重点**：[qhkm/zeptoclaw#387](https://github.com/qhkm/zeptoclaw/issues/387)  
    尽管该 Issue 讨论热烈（6条评论），但标记仍为 `[OPEN]`。由于涉及底层核心架构变动（引入 Firecracker），建议维护者尽快评估技术可行性并决定是否纳入 Roadmap，以避免讨论长期悬而未决。

---

**日报生成者：AI 开源项目分析师**  
*数据基于 UTC 时间 2026-03-21 00:00 - 24:00*

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

你好！我是 EasyClaw 项目分析师。以下是基于 2026-03-21 GitHub 数据生成的项目动态日报。

---

# EasyClaw 项目日报 (2026-03-21)

> **数据范围**: 2026-03-20 20:00 - 2026-03-21 20:00 (UTC+8)
> **项目仓库**: [gaoyangz77/easyclaw](https://github.com/gaoyangz77/easyclaw)

## 1. 今日速览
EasyClaw 项目今日处于 **“版本维护 + 跟进修复”** 阶段。核心动态是发布了 **v1.7.3** 版本，该版本重点解决了 macOS 平台的“已损坏”安全拦截问题，改善了一键安装体验。与此同时，社区反馈了 Windows 11 平台在 v1.7.2 版本下存在的配置解析错误（400 报错），尽管此 Issue 在旧版本中提出，但目前未有 PR 关联修复，需关注维护者是否会在后续补丁中解决。整体来看，项目活跃度侧重于客户端适配与问题修复。

## 2. 版本发布
**[v1.7.3: RivonClaw v1.7.3](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.7.3)**
- **发布时间**: 2026-03-21
- **核心变更**: 主要针对 macOS 用户的安装体验进行了修复与文档增强。
- **关键修复**:
  - **macOS Gatekeeper 适配**: 解决了 macOS 系统提示“'RivonClaw' is damaged and can't be opened”的问题。这是由于未签名应用被 macOS 安全机制拦截所致。虽然更新日志未提供完整的终端修复命令（内容截断），但这表明维护者已意识到并正在指导用户绕过此限制。
- **影响范围**: 提升 macOS 新用户的初次启动成功率，降低因系统安全策略导致的试用门槛。

## 3. 项目进展
今日 **无 Pull Requests** 合并或更新。项目代码库在今日处于静态，所有进展体现在 Release 层面的文档与部署流程优化。

## 4. 社区热点
**[#25 Windows11系统，1.7.2版本，发生⚠ 400 [] is too short - 'tools'这个问题](https://github.com/gaoyangz77/rivonclaw/issues/25)**
- **状态**: Open (新开)
- **热度**: 🔥 关注点较高（涉及核心报错）
- **问题分析**: 用户在 Windows 11 环境下运行 v1.7.2 版本时，收到 `400 [] is too short - 'tools'` 的错误提示。
- **背后诉求**: 这是一个典型的后端验证或客户端请求体构造错误。用户可能未正确配置 `tools` 参数（可能为空列表），或者客户端在特定请求中未携带必需的工具定义。由于日志显示“对话内容的回复只有这个”，说明错误阻断了 AI 的正常交互流程，属于阻塞性 Bug。

## 5. Bug 与稳定性
**严重程度: 高**
- **Windows 配置验证缺陷**: [Issue #25](https://github.com/gaoyangz77/rivonclaw/issues/25) 报告的 `400` 错误。这表明应用在发送请求前未进行有效的本地预校验，或者默认配置存在缺失。
  - **状态**: 🔴 **暂无 Fix PR**。维护者尚未发布针对 Windows 平台的 v1.7.3 修复补丁（v1.7.3 主要针对 macOS）。

**稳定性**:
- macOS 平台因 Gatekeeper 问题导致安装/打开受阻（稳定性下降），但已通过 v1.7.3 的说明进行了缓解。

## 6. 功能请求与路线图信号
今日无新的功能请求（Feature Request）。社区焦点集中在现有功能的**跨平台稳定性**上。
- **信号**: 维护者目前的优先级是确保 RivonClaw 在主流操作系统（特别是 macOS）上的可用性，而非开发新特性。

## 7. 用户反馈摘要
- **Windows 用户 (slowayear)**: 遭遇严重的交互阻断问题，无法进行正常对话，用户体验受阻。
- **macOS 用户 (隐含)**: 反映安装包被系统拦截，虽然已提供解决方案，但未签名应用依然是企业级或新手用户采用的障碍。

## 8. 待处理积压
- **Issue #25 (Windows 400 Error)**: 尽管是在 v1.7.2 提出，但在最新的 v1.7.3 Release 中未提及修复。建议维护者尽快排查 `tools` 参数的验证逻辑，确保 Windows 用户在升级或安装新版时不会遇到相同问题。

---
*日报生成时间: 2026-03-21 | 数据来源: GitHub API*

</details>

---
*本日报由 [agents-radar](https://github.com/yinwm/agents-radar) 自动生成。*