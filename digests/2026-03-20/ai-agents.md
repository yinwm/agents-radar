# OpenClaw 生态日报 2026-03-20

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-03-20 01:18 UTC

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

# OpenClaw 项目日报 (2026-03-20)

## 1. 今日速览
OpenClaw 项目今日维持极高的开发活跃度，社区讨论热烈。过去 24 小时内共有 **500 条 Issues** 更新（其中新开/活跃 347 条）和 **500 条 PRs** 更新（待合并 339 条），显示出庞大的代码吞吐量和用户参与度。今日没有新版本发布，正处于 v2026.3.12/v2026.3.13 系列的持续迭代周期。核心议题集中在 **WhatsApp 连接稳定性回归**、**多 LLM 提供商兼容性问题** 以及 **新功能（如 Agent Teams、MCP 协议）的探讨**。同时，社区出现关于钓鱼诈骗的安全警示，维护者需关注。

## 2. 版本发布
*   **当前状态**：无新版本发布。
*   **背景**：项目目前正在维护 2026.3.x 版本线。根据 Issues 反馈，近期 v2026.3.12 和 v2026.3.13 版本引入了若干回归问题，主要集中在 WhatsApp 消息发送和本地网关握手超时方面。

## 3. 项目进展
今日 PR 列表中有大量关键修复正在审查或待合并，主要集中在提升稳定性与连接兼容性：

*   **[PR #49420](https://github.com/openclaw/openclaw/pull/49420)**: `fix(acp)`: 防止"幽灵会话"（Ghost Turns）和会话卡死。通过引入超时中止信号和交付守卫，修复了调度路径中的潜在死锁问题。
*   **[PR #43497](https://github.com/openclaw/openclaw/pull/43497)**: `fix(agents)`: 修复网关重启后子代理会话丢失的问题。确保子代理在网关重启后能恢复运行状态，提升了系统的鲁棒性。
*   **[PR #49200](https://github.com/openclaw/openclaw/pull/49200)**: 集成 **Tavily** 作为内置 Web 搜索插件。增加了对 Tavily Search API 的原生支持，为用户提供了除 Brave/Kimi 之外的新搜索选项。
*   **[PR #50720](https://github.com/openclaw/openclaw/pull/50720)**: `feat(sessions)`: 支持 `sessions_send` 的私有投递模式，并优化了多代理间通信的文档和提示词。
*   **[PR #50725](https://github.com/openclaw/openclaw/pull/50725)**: 统一插件运行时状态，修复了因重复导入导致的状态分离（如监听器和队列），属于底层架构优化。

## 4. 社区热点
今日讨论热度最高的话题覆盖了安全、跨平台支持、核心 Bug 及新架构构想：

*   **⚠️ [Security] 钓鱼诈骗警告 ([#49836](https://github.com/openclaw/openclaw/issues/49836))**:
    *   **热度**: 32 💬
    *   **内容**: 用户报告有恶意仓库利用 OpenClaw 名义进行钓鱼活动。社区迅速响应，广泛传播警示信息。
*   **🍏 Linux/Windows 桌面客户端需求 ([#75](https://github.com/openclaw/openclaw/issues/75))**:
    *   **热度**: 63 👍, 46 💬
    *   **内容**: 作为一个长期悬而未决的 Enhancement，用户强烈呼吁开发 Linux 和 Windows 版本的 Clawdbot，以补齐移动端和 macOS 端的生态拼图。
*   **🔧 WhatsApp 回归问题集中爆发**:
    *   多个高赞 Issue ([#34741](https://github.com/openclaw/openclaw/issues/34741), [#45171](https://github.com/openclaw/openclaw/issues/45171), [#46659](https://github.com/openclaw/openclaw/issues/46659)) 反馈升级后 WhatsApp 出现 "No active listener" 错误。症状多为自动回复正常，但主动发送失败。
*   **🚀 Agent Teams 与 MCP 集成愿景**:
    *   [#10010](https://github.com/openclaw/openclaw/issues/10010) 提出了受 Claude Code 启发的"并行代理协调"功能；
    *   [#29053](https://github.com/openclaw/openclaw/issues/29053) 建议原生支持 Model Context Protocol (MCP)，以标准化工具调用。

## 5. Bug 与稳定性
今日报告的 Bug 呈现出明显的"版本回归"特征，涉及认证、网络和兼容性：

*   **[CRITICAL] WhatsApp 连接性回归**:
    *   **描述**: v2026.3.12/v2026.3.13 版本中，WhatsApp 状态显示连接，但 CLI 或 Agent 主动发送消息时报错 `No active WhatsApp Web listener`。
    *   **相关 Issues**: [#45171](https://github.com/openclaw/openclaw/issues/45171), [#45232](https://github.com/openclaw/openclaw/issues/45232), [#48109](https://github.com/openclaw/openclaw/issues/48109)。
    *   **状态**: 正在修复中（部分已在 Draft PR 中处理）。
*   **[HIGH] 网关握手超时**:
    *   **描述**: 本地网关 CLI 命令 (如 `devices list`) 在 v2026.3.12 后频繁失败，报错 `Gateway closed (1000)`。
    *   **相关 Issues**: [#45504](https://github.com/openclaw/openclaw/issues/45504), [#46892](https://github.com/openclaw/openclaw/issues/46892), [#45173](https://github.com/openclaw/openclaw/issues/45173)。
    *   **Fix**: [#46892](https://github.com/openclaw/openclaw/issues/46892) 提出将 3 秒握手超时延长。
*   **[MEDIUM] LLM 提供商认证失败**:
    *   **Anthropic**: [#23538](https://github.com/openclaw/openclaw/issues/23538) 报告 setup-token 在运行时返回 401。
    *   **Mistral**: [#41293](https://github.com/openclaw/openclaw/issues/41293) 报告直接调用 API 成功但 OpenClaw 调用失败 (422)。
    *   **Ollama**: [#50713](https://github.com/openclaw/openclaw/issues/50713) 工具调用参数序列化问题 (PR #50729 已修复)。
*   **[MEDIUM] Matrix E2EE 与插件加载**: [#7649](https://github.com/openclaw/openclaw/issues/7649) (Bot 无法验证自身), [#47717](https://github.com/openclaw/openclaw/issues/47717) (Docker 下缺少依赖)。

## 6. 功能请求与路线图信号
社区对 OpenClaw 的扩展性和生态整合有明确期待：

*   **Agent Teams (并行协调)**: [#10010](https://github.com/openclaw/openclaw/issues/10010)。用户希望能让多个 Agent 并行工作并相互通信。鉴于 OpenClaw 已有 `sessions_spawn` 基础，这是高优先级的架构演进方向。
*   **MCP 协议原生支持**: [#29053](https://github.com/openclaw/openclaw/issues/29053)。用户希望直接连接外部 MCP 服务器，而非仅限于 OpenClaw 内部工具系统。
*   **MiniMax M2.7 支持**: [#50234](https://github.com/openclaw/openclaw/issues/50234)。跟进最新模型。
*   **外部内存提供者 API**: [#49233](https://github.com/openclaw/openclaw/issues/49233)。提议引入外部内存系统以消除上下文压缩时的 30-60 秒"黑障期"，实现零停机压缩。

## 7. 用户反馈摘要
*   **痛点**:
    *   **Web Search 付费墙**: [#16629](https://github.com/openclaw/openclaw/issues/16629) 用户抱怨 Brave Search API 不再免费，急需替代方案（如 DuckDuckGo, PR #47279 正在推进）。
    *   **时间感知缺失**: [#10841](https://github.com/openclaw/openclaw/issues/10841) Agent 无法准确获取当前时间，导致闹钟和提醒功能失效。
    *   **安装/构建复杂性**: Ubuntu 24.04 安装失败 ([#39447](https://github.com/openclaw/openclaw/issues/39447))，Docker 构建依赖问题 ([#47717](https://github.com/openclaw/openclaw/issues/47717))。
*   **正面反馈**: 用户对 Matrix、Feishu 等多平台集成功能表示认可，但在高频更新周期中遭遇了稳定性倒退（特别是 WhatsApp 用户）。

## 8. 待处理积压
以下长期未解决的 Issue 仍需维护者关注：

*   **[#75 (Linux/Windows Apps)](https://github.com/openclaw/openclaw/issues/75)**: 开始于 1 月初，虽是 enhancement 但拥有极高的社区关注度，尚未有明确的 PR。
*   **[#16918 (WhatsApp Socket Race Condition)](https://github.com/openclaw/openclaw/issues/16918)**: 陈旧 Issue，描述了 socket 竞态条件导致消息丢失，今日的回归问题可能与之相关。
*   **[#26322 (OAuth Token Refresh Race)](https://github.com/openclaw/openclaw/issues/26322)**: 多 Agent 共用 OAuth 配置时的 Token 刷新竞态问题。
*   **[#25359 (Per-agent Plugin Slots)](https://github.com/openclaw/openclaw/issues/25359)**: 多 Agent 架构下插件配置隔离的需求。

---
*数据来源：OpenClaw GitHub Activity (2026-03-20)*

---

## 横向生态对比

# 2026-03-20 个人 AI 助手开源生态横向对比分析报告

**分析师**：AI 智能体与个人助手领域观察员
**基准日期**：2026-03-20
**参照对象**：OpenClaw (Core)

---

## 1. 生态全景
2026 年 3 月的个人 AI 助手开源生态正处于**从“单体应用”向“多模态、多智能体协作平台”剧烈转型**的阶段。社区对**长对话记忆**、**端到端隐私安全**以及**多平台工作流自动化**的需求已超越简单的聊天功能。虽然行业整体呈现出极高的开发活跃度，但各项目普遍面临着**模型兼容性碎片化**（如 OpenAI API 变更）和**系统稳定性**（如网关重启、上下文溢出）的共性技术挑战。

---

## 2. 各项目活跃度对比 (2026-03-20)

| 项目 | Issues (活跃/新增) | PRs (合并/更新) | Release 发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** (参照) | 500 (极高) | 500 (极高) | 无 (v2026.3.13 迭代中) | **⚠️ 警戒**：吞吐量巨大，但面临严重的版本回归Bug (WhatsApp/Gateway)，急需发布补丁。 |
| **CoPaw** | 50 | 50 | **v0.1.0 (Major)** | **🔥 爆发期**：正式版发布引发大量升级兼容性问题，多智能体架构带来阵痛。 |
| **Zeroclaw** | 32 (Closed 32) | 40 | **v0.5.1** | **🟢 稳健**：Issue 清理效率极高，发布节奏稳定，本地模型集成有亮点。 |
| **LobsterAI** | 19 | 33 | **v2026.3.19** | **🟡 波动**：版本频繁，但频繁重启和兼容性问题导致用户信任度波动。 |
| **IronClaw** | 50 | 50 | **v0.20.0** | **⚠️ 回退**：新版本引入了严重的缓存性能回退和数据库迁移失败问题。 |
| **NanoBot** | 24 | 52 | 无 | **🚀 活跃**：PR数量是Issues的两倍，正在进行深度的交互循环重构。 |
| **PicoClaw** | 40 | 106 | **v0.2.3-nightly** | **🔄 极速**：代码提交频繁，Nightly 版本迭代，但在配置继承和文档上技术债较重。 |
| **NanoClaw** | 15 | 32 | 无 | **🔧 深耕**：专注于容器安全性和开发者体验（Git Hooks），维护响应快。 |
| **NullClaw** | 10 | 16 | **v2026.3.18** | **🟢 平稳**：协议标准化 (A2A) 和 NixOS 适配进展顺利。 |
| **Moltis** | 1 | 7 (3 Open) | 无 | **🛡️ 严谨**：社区小而精，专注于防绕过安全机制和 Rust 底层稳定性。 |
| **TinyClaw** | 0 | 2 (Open) | 无 | **💤 低活**：核心架构重构中，暂无对外输出，进入开发静默期。 |
| **ZeptoClaw** | 1 | 3 (Open) | 无 | **🔨 基建**：专注底层协议 (ACP) 实现，功能开发暂时让位于工程化标准。 |
| **EasyClaw** | 1 | 3 (Merged) | **v1.7.2/v1.7.3** | **🎨 UI/UX**：连续发版，重点在于 UI 重构和 macOS 适配，代码层变动较少。 |

---

## 3. OpenClaw 在生态中的定位
*   **核心地位**：OpenClaw 以 **500+ Issues/PRs** 的绝对数据量稳居生态核心，是社区规模最大、吞吐量最高的“事实标准”参照物。其更新速度代表了行业的最高频次。
*   **技术路线差异**：
    *   **激进 vs 稳健**：相比 Zeroclaw 和 NullClaw 致力于协议标准化和清晰的版本发布，OpenClaw 采取了“激进的滚动更新”策略，导致近期频繁出现**版本回归**（如 WhatsApp 监听器失效）。
    *   **平台广度**：OpenClaw 在平台覆盖广度上略胜一筹，但 **Linux/Windows 桌面客户端** (#75) 的缺失是其相对于 EasyClaw 或其他跨平台工具的明显短板。
*   **社区规模**：其讨论热度（如钓鱼诈骗警示瞬间引发 32+ 讨论）显示出极强的社区凝聚力，但也因此吸引了大量非技术性噪音，维护者面临巨大的分类与治理压力。

---

## 4. 共同关注的技术方向
以下是多个项目在同一时间点（2026-03-20）涌现出的共性需求，预示着行业的技术演进方向：

1.  **多模态与语音交互**
    *   **涉及**：**PicoClaw** (#1648), **NanoClaw** (#1269), **CoPaw** (Console Multi-modal)
    *   **诉求**：不再满足于文本，强烈要求集成 TTS/ASR，支持语音消息的转录与发送。

2.  **多智能体编排**
    *   **涉及**：**OpenClaw** (#10010), **CoPaw** (v0.1.0 核心特性), **LobsterAI** (#541)
    *   **诉求**：从单一 Agent 演进到 Agent Teams，支持并行协调、任务分发和跨 Agent 通信。

3.  **安全性与防绕过**
    *   **涉及**：**NanoClaw** (Git Hooks 防绕过 #1271), **Moltis** (PreToolUse Hook #455)
    *   **诉求**：随着 Agent 获得更高权限（如 `exec`），用户极度关注 Agent 是否会跳过安全检查（如 Git pre-commit hooks）。

4.  **实时交互控制**
    *   **涉及**：**NanoBot** (Steering Loop #1224), **Zeroclaw** (`/stop` command #3891), **PicoClaw** (Interrupts)
    *   **诉求**：用户无法接受 Agent 在执行长任务时“失聪”，要求能够在任务执行中途插入消息、中断或引导 Agent。

---

## 5. 差异化定位分析
*   **全能型选手**：**OpenClaw**、**IronClaw**。功能覆盖最广，试图通过插件和集成覆盖所有场景，但也因此背负了最沉重的历史包袱和 Bug 负担。
*   **架构派**：**CoPaw** (Multi-Workspace), **NanoClaw** (Container Security)。侧重于底层的运行时隔离、多实例管理，面向开发者和高级极客用户。
*   **体验派**：**EasyClaw**, **LobsterAI**。侧重于 UI/UX 的打磨、Web 界面的现代化以及企业微信/飞书等办公场景的深度集成，面向终端办公用户。
*   **协议/底层派**：**ZeptoClaw** (ACP Protocol), **NullClaw** (A2A Protocol), **Moltis** (Rust Safety)。它们的核心价值不在于“好用”而在于“标准”和“安全”，是构建上层应用的地基。
*   **边缘/轻量派**：**PicoClaw**, **TinyClaw**, **NanoBot**。强调轻量化、边缘设备运行（如 Android/Termux）或特定垂直场景（如 `/office` 工作区）。

---

## 6. 社区热度与成熟度
*   **第一梯队 (成熟期/维护期)**：**Zeroclaw**, **NullClaw**。Issues 关闭率高，Release 规律，文档和工程化规范（如 Justfile, Taplo）完善，适合生产环境谨慎使用。
*   **第二梯队 (快速迭代期)**：**OpenClaw**, **PicoClaw**, **NanoBot**。代码提交极快，功能日新月异，但稳定性波动大，适合追求新功能的尝鲜者。
*   **第三梯队 (架构重构期)**：**CoPaw**, **IronClaw**, **LobsterAI**。刚刚发布或正在经历重大的架构升级（如多智能体、缓存系统），处于旧 Bug 修复与新 Feature 引入的阵痛期，短期稳定性较低。
*   **第四梯队 (冷启动/重塑期)**：**TinyClaw**, **EasyClaw**。项目在重构底层或重塑 UI，社区声音较小，处于技术打磨阶段。

---

## 7. 值得关注的趋势信号 (给 AI 开发者的建议)

1.  **"交互可控性" 成为新刚需**：
    用户不再满足于发个指令然后等结果。**NanoBot** 和 **Zeroclaw** 的动态表明，**Steering Loop（实时引导）** 和 **Task Interrupt（任务中断）** 是提升用户体验的关键。如果你的 Agent 还是“发令枪”模式，用户会感到焦虑。

2.  **多 Agent 协作的落地元年**：
    **OpenClaw**、**CoPaw** 和 **LobsterAI** 的讨论显示出市场正在从“单点工具”向“团队协作”过渡。Agent 间通信协议（如 **MCP**、**A2A**）的标准化将成为接下来的竞争高地。

3.  **本地化与隐私优先**：
    **Zeroclaw** 和 **PicoClaw** 的用户对 **Ollama** 和 **Venice.ai** 等本地模型的高度关注，以及对 **Moltis** 安全机制的推崇，表明开发者社区对数据隐私的敏感度正在提升。

4.  **警惕"版本疲劳"与"回归灾难"**：
    **OpenClaw** 和 **IronClaw** 今天的报告（WhatsApp 失效、缓存回退）给所有开发者敲响警钟：**高频迭代不等于高质量迭代**。在引入重大变更（如缓存系统、网关逻辑）时，缺乏回归测试会导致严重的社区信任危机。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目日报 (2026-03-20)

## 1. 今日速览
NanoBot 项目今日呈现出极高的活跃度，社区参与度显著提升。过去 24 小时内产生了 76 条代码与讨论更新（Issues: 24, PRs: 52），表明项目正处于快速迭代与功能扩张期。核心讨论集中在**实时交互能力**（如任务中断、会话管理）和**多通道适配**（如 QQ、飞书、Telegram）的优化上。虽然今日无新版本发布，但大量针对安全性、配置向导 和日志追踪的 PR 正在密集合并，预示着下一个版本将重点聚焦于稳定性与企业级特性。

## 2. 版本发布
*今日无新版本发布。*

## 3. 项目进展
今日虽无官方 Release，但合并或接近合并的 PR 推动了以下关键进展：

*   **交互体验重构**：
    *   **PR #2276**: 提议使用共享会话 来处理 Cron 和 Heartbeat 任务。这将解决定时任务无法与用户进行多轮交互的痛点，标志着 NanoBot 从“单向通知”向“双向交互代理”的重要跨越。[链接](https://github.com/HKUDS/nanobot/pull/2276)
    *   **PR #1224**: 引入可选的双层架构，实现 `Steering Loop`。允许用户在 Agent 执行工具链期间插入新消息，动态中断并引导任务执行，极大提升了复杂任务的可控性。[链接](https://github.com/HKUDS/nanobot/pull/1224)
*   **安全性与可观测性增强**：
    *   **PR #2218 & #2265**: 完善了环境变量引用语法 `{env:VAR}` 并固化了保存/恢复语义，防止敏感密钥泄露，增强了容器化部署的安全性。[链接](https://github.com/HKUDS/nanobot/pull/2218)
    *   **PR #2268**: 增加了 LiteLLM 的 Tracing 回调功能，实现了对 Token 使用、延迟和成本的非侵入式追踪。[链接](https://github.com/HKUDS/nanobot/pull/2268)
*   **通道修复**：
    *   **PR #2270**: 修复了飞书 机器人无法正确检测“提及”的问题，保障群聊互动准确性。[链接](https://github.com/HKUDS/nanobot/pull/2270)

## 4. 社区热点
*   **#2133 [enhancement] 关于在任务执行期间用户消息入列的一些想法**
    *   **状态**: [OPEN] | **评论**: 18 | **链接**: [HKUDS/nanobot#2133](https://github.com/HKUDS/nanobot/issues/2133)
    *   **分析**: 这是当前最热门的架构讨论。用户痛点在于 Agent 在执行长任务时“失聪”，必须等待 Loop 结束。社区正在探讨是修改底层 Agent 循环逻辑，还是通过简单的 `agent.md` 提示词工程来解决。这反映了用户对“实时响应式 Agent”的强烈需求。

*   **#1873 [enhancement] Nanobot currently cannot be secured from accessing it's own config.json**
    *   **状态**: [OPEN] | **评论**: 9 | **链接**: [HKUDS/nanobot#1873](https://github.com/HKUDS/nanobot/issues/1873)
    *   **分析**: 安全性备受关注。用户指出 Agent 若拥有 `exec()` 权限且能读取配置文件，存在泄露密钥的风险。虽然 PR #2218 部分缓解了此问题，但关于“多用户权限隔离”的根本性重构仍在讨论中。

*   **#2018 [Feedback] Try the new interactive configuration wizard [nanobot onboard]**
    *   **状态**: [OPEN] | **评论**: 9 | **链接**: [HKUDS/nanobot#2018](https://github.com/HKUDS/nanobot/issues/2018)
    *   **分析**: 新的交互式配置向导 收到了大量反馈，既有赞扬也有关于配置保存逻辑 的 Bug 报告。

## 5. Bug 与稳定性
*   **[严重] PR #2266**: `nanobot onboard` 在特定更新选项（选择 N）后会导致 Crash，并破坏配置文件的可用性。
    *   **状态**: 已提交修复 PR。用户需谨慎使用 nightly 版本的配置向导。
*   **[中等] Issue #2235**: Telegram 机器人回复显示两次（Faux streaming 问题）。
    *   **状态**: [OPEN] 待修复。[链接](https://github.com/HKUDS/nanobot/issues/2235)
*   **[中等] Issue #2242**: 飞书通道无法处理用户发送的图片。
    *   **状态**: [OPEN] 待修复。[链接](https://github.com/HKUDS/nanobot/issues/2242)
*   **[中等] Issue #2256**: 飞书话题群中，Bot 回复位置不正确（未在话题内回复）。
    *   **状态**: [OPEN] 待修复。[链接](https://github.com/HKUDS/nanobot/issues/2256)
*   **[轻微] Issue #2241**: 贡献指南中的 Ruff 检查报错，干扰新贡献者 workflow。
    *   **状态**: [CLOSED] 已关闭，可能是代码库已清理或指南已更新。[链接](https://github.com/HKUDS/nanobot/issues/2245)

## 6. 功能请求与路线图信号
*   **插件系统**: **Issue #2231** 请求引入类似 Copilot/Claude Code 的插件系统，以扩展 Agent 能力。这是一个潜在的路线图大方向。[链接](https://github.com/HKUDS/nanobot/issues/2231)
*   **模型动态切换**: **Issue #2257** 提出通过命令（如 Telegram 指令）动态切换 LLM 模型，无需重启服务。[链接](https://github.com/HKUDS/nanobot/issues/2257)
*   **QQ 通道文件支持**: **PR #1667** 正在为 QQ 适配图片和文件收发功能，弥补了 QQ 通道只能纯文本聊天的短板。[链接](https://github.com/HKUDS/nanobot/pull/1667)
*   **会话管理优化**: **Issue #2062** 用户请求增加“清空/重启会话”的功能，以解决上下文撑爆的问题。[链接](https://github.com/HKUDS/nanobot/issues/2062)

## 7. 用户反馈摘要
*   **痛点**: 上下文管理依然是难题。用户在飞书等长时间聊天的场景下，面临 Session 文件过大导致上下文溢出的问题，不得不手动删除文件重启服务。
*   **体验**: 交互式配置 被认为是“巨大的进步”，降低了上手门槛，但仍有用户反馈其在非正常退出时的数据持久化逻辑不够直观。
*   **通道质量**: QQ 和 Telegram 用户对多媒体支持（图片、文件）的呼声最高；Telegram 用户抱怨网络波动造成的日志刷屏，已有 PR 尝试优化。

## 8. 待处理积压
*   **Issue #1300 [Matrix Channel]**: Matrix 通道无法正常工作，Error 较多，且自 2 月底以来未完全解决。
*   **Issue #1864 [DingTalk]**: 钉钉用户侧不支持上传文件，收到 "file" 类型时报错。
*   **Issue #2273 [MCP Compatibility]**: Browser-use MCP 工具与 OpenRouter/OpenAI GPT-5.4 的 Schema 不兼容问题，涉及复杂的 Schema 验证逻辑，可能需要较长时间协调。

---
**总结**: NanoBot 今日在“实时性”和“工程化”方面迈出了大步。虽然多通道适配仍存在细节 Bug，但社区对 Steerin Loop 和安全增强的积极响应表明项目正在向生产级 Agent 系统演进。建议关注 PR #2276 和 #1224 的合并情况，这将是下一版本的核心卖点。

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报 2026-03-20

> **核心摘要**：项目处于**极高活跃度**状态，24小时内合并了 **40 个 PR** 并关闭了 **32 个 Issue**，正式发布了 **v0.5.1** 版本。今日重点在于**安全策略的透明化**、**多平台交互体验的统一**（Telegram/Discord/Mattermost/Slack）以及**容器化部署的易用性修复**。虽然社区反馈强烈，但涌现出大量关于本地大模型（Ollama）工具调用失败的新 Bug，需重点关注。

---

### 1. 今日速览
Zeroclaw 项目今日迎来 v0.5.1 正式版发布，标志着项目进入新的稳定阶段。社区贡献度极高，共有 10 个新版本打包生成，核心功能更新集中在**运行时模型切换**、**代理超时配置化**以及**技能/脚本的审计与加载机制**。Issues 处理效率惊人，关闭数量是新增/活跃数量的 3 倍，显示出维护团队正在积极清理技术债务。然而，随着 `autonomy.level = "full"` 和本地模型（Ollama/Venice.ai）的使用增多，涌现出 S1 级别的工具调用握手失败和幻觉 Bug。

---

### 2. 版本发布
**正式版本：v0.5.1**
- **下载/更新建议**：所有用户建议立即更新，特别是使用 Docker 和子代理功能的用户。
- **核心亮点**：
    - **Agent**：新增 `model_switch` 工具，支持运行时无缝切换模型。
    - **Delegate**：子代理的超时时间可通过 `config.toml` 配置，解决死锁问题。
    - **Heartbeat**：默认心跳间隔从 30 分钟优化至 5 分钟，减少资源占用。
    - **Security**：**关键更新**，将安全策略摘要注入 LLM 系统提示词，解决 Agent 不知道自己被限制而反复试错的问题 ([#2404](https://github.com/zeroclaw-labs/zeroclaw/issues/2404))。
- **Beta 版本动态**：
    - **v0.5.1-beta.414**：Telegram 通道新增 TTS 语音回复支持；Discord 和 Mattermost 新增消息中断 (`interrupt_on_new_message`) 支持。
    - **v0.5.1-beta.378 - .400**：持续完善技能机制，新增 `read_skill` 工具以支持紧凑模式下的按需加载，新增 Slack 线程回复选项。

---

### 3. 项目进展
今日合并的 PR 显著提升了系统的**可控性**与**平台兼容性**：

- **交互控制增强**：
    - **feat(channel)**: 为 Discord ([#3918](https://github.com/zeroclaw-labs/zeroclaw/pull/3918)) 和 Mattermost ([#3917](https://github.com/zeroclaw-labs/zeroclaw/pull/3917)) 增加了 `interrupt_on_new_message` 支持，追平了 Telegram 的体验。
    - **feat(channel)**: 新增 `/stop` 命令 ([#3891](https://github.com/zeroclaw-labs/zeroclaw/pull/3891))，允许用户取消正在进行的飞行任务，修复了之前处理器取消自身的竞态条件。
- **Docker 易用性修复**：
    - **fix(docker)**: 将默认 CMD 从 `gateway` 更改为 `daemon` ([#3897](https://github.com/zeroclaw-labs/zeroclaw/pull/3897))。之前的默认启动方式不会加载通道监听器（如 Telegram/Discord），导致大量新手用户以为 Docker 镜像无法连接，此修复显著降低上手门槛。
- **开发者体验**：
    - 引入 `Justfile` ([#3874](https://github.com/zeroclaw-labs/zeroclaw/pull/3874)) 统一开发命令，添加 `taplo.toml` ([#3873](https://github.com/zeroclaw-labs/zeroclaw/pull/3873)) 规范 TOML 格式。
- **配置与安全**：
    - **feat(skills)**: 恢复并新增 `allow_scripts` 审计选项 ([#4001](https://github.com/zeroclaw-labs/zeroclaw/pull/4001))，允许用户配置是否允许技能包含脚本文件，平衡了安全与灵活性。

---

### 4. 社区热点
今日讨论热度最高的帖子反映了用户对**权限控制**和**基础功能稳定性**的强烈关注：

- **[#1478 [Feature]: 除了安全,什么功能也没有](https://github.com/zeroclaw-labs/zeroclaw/issues/1478)** (🔥 42 评论)
  - **核心痛点**：用户吐槽 ZeroClaw 的安全限制过于严格，即使放开配置仍拒绝安装 `ffmpeg` 等基础工具，导致只能当“聊天机器人”。
  - **现状**：已关闭。PR #4001 (允许配置 `allow_scripts`) 和 v0.5.1 的安全策略透明化更新是对此的直接回应。
- **[#3882 Feature Request: Support 阿里云百炼 Coding Plan](https://github.com/zeroclaw-labs/zeroclaw/issues/3882)** (🔥 8 评论)
  - **诉求**：希望增加对阿里云百炼 Coding Plan 模型的支持。
  - **进展**：已有对应 PR [#3889](https://github.com/zeroclaw-labs/zeroclaw/pull/3889) 正在开发中。

---

### 5. Bug 与稳定性
今日报告了多个 S1 级别的严重 Bug，主要集中在**本地/私有模型部署**场景：

- **[#3999 Bug: Ollama Tool-Calling Handshake Failure](https://github.com/zeroclaw-labs/zeroclaw/issues/3999)** (S1 - 阻断)
  - **现象**：使用本地 Ollama 时，Zeroclaw 无法执行工具命令，也无法弹出安全确认提示，处于静默失败状态。
- **[#4007 Bug: Tool use with Venice.ai doesn't work](https://github.com/zeroclaw-labs/zeroclaw/issues/4007)** (S1 - 阻断)
  - **现象**：Venice.ai 模型声称没有可用工具或返回 JSON 而非函数调用。
- **[#3982 Bug: severe hallucination](https://github.com/zeroclaw-labs/zeroclaw/issues/3982)** (S1 - 阻断)
  - **现象**：在 Raspberry Pi 环境下，Agent 对系统状态产生严重幻觉（如错误的 `lsb_release` 信息）。
- **[#3764 Bug: Web UI endpoint returns 405... with custom provider headers](https://github.com/zeroclaw-labs/zeroclaw/issues/3764)** (S1 - 阻断)
  - **现象**：CLI 可以正常工作，但 Web UI 对自定义 Header 的支持有问题，导致请求失败。
- **[#3974 Bug: Native tool-call assistant text is dropped](https://github.com/zeroclaw-labs/zeroclaw/issues/3974)** (S2 - 降级)
  - **现象**：使用 Native Tool Call 时，LLM 的解释性文本在 Draft 更新中丢失，用户看不到 Agent 的思考过程。

---

### 6. 功能请求与路线图信号
从 Issues 和 PRs 中可以看出未来的开发方向：

- **本地模型支持强化**：针对 Ollama 和 Venice.ai 的问题，预示下一个版本将重点修复非 OpenAI/Anthropic 协议的工具调用兼容性。
- **Web UI 现代化**：PR [#3986](https://github.com/zeroclaw-labs/zeroclaw/pull/3986) 提出引入完整的主题系统和设置模态框，Web 界面功能将更加丰富。
- **企业级工具集成**：
    - **Google Workspace**：PR [#4010](https://github.com/zeroclaw-labs/zeroclaw/pull/4010) 正在增加操作级别的白名单，以细化 Gmail/Calendar 等服务的权限控制。
    - **Jira**：PR [#3997](https://github.com/zeroclaw-labs/zeroclaw/pull/3997) 新增 Jira 集成工具。
- **计算能力增强**：PR [#4012](https://github.com/zeroclaw-labs/zeroclaw/pull/4012) 新增计算器工具，以减少 LLM 在数学计算上的幻觉。

---

### 7. 用户反馈摘要
- **满意度正向**：
  - Docker 默认启动行为的修复 ([#3897](https://github.com/zeroclaw-labs/zeroclaw/pull/3897)) 获得了大量好评，解决了困扰新手的一大痛点。
  - Slack 线程回复功能 ([#3888](https://github.com/zeroclaw-labs/zeroclaw/issues/3888)) 的补齐受到移动端用户欢迎。
- **痛点与抱怨**：
  - **Homebrew 安包缺失前端**：用户反馈通过 Brew 安装的版本没有前端界面，导致 `zeroclaw gateway` 无效 ([#3991](https://github.com/zeroclaw-labs/zeroclaw/issues/3991))。
  - **Full Autonomy 不生效**：设置了 `autonomy.level = "full"` 后，Agent 在非 CLI 通道（如 Telegram）依然模拟权限请求而非直接执行 ([#3952](https://github.com/zeroclaw-labs/zeroclaw/issues/3952))。
  - **Sandbox 配置无效**：用户发现 `[security.sandbox]` 配置存在但实际上并未应用到 Shell 命令中 ([#3983](https://github.com/zeroclaw-labs/zeroclaw/issues/3983))。

---

### 8. 待处理积压
- **[#2401 Feature: /reasoning and /stop command](https://github.com/zeroclaw-labs/zeroclaw/issues/2401)**：虽然 `/stop` 已实现，但 `/reasoning` 命令（显示 Agent 思考过程）仍有待开发。
- **[#3642 Feature: Provide a "full" docker image](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)**：社区强烈要求提供一个包含所有功能（如 WhatsApp）的 Docker 镜像，而不仅仅是默认的精简版，以降低非技术用户的部署难度。
- **[#3782 Bug: MCP tools... unavailable in daemon /api/chat](https://github.com/zeroclaw-labs/zeroclaw/issues/3782)**：MCP 工具在 `channel start` 时可用但在 `daemon` 模式的 API 调用中不可用，这是一个严重的架构一致性问题，目前尚未有明确的修复时间表。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

你好！我是 PicoClaw (sipeed/picoclaw) 的项目分析师。以下是根据 **2026-03-20** 的 GitHub 数据生成的项目动态日报。

---

## 📊 PicoClaw 项目日报 (2026-03-20)

### 1. 今日速览
PicoClaw 项目今日处于**高度活跃**状态。过去 24 小时内共有 **106 个 PR** 和 **40 个 Issues** 发生变动，代码提交与讨论热度均处于高位。项目已发布最新的 **v0.2.3-nightly (20260320)** 版本，修复了 Anthropic API 兼容性及 OpenAI 格式序列化等关键问题。社区讨论主要集中在**语音交互**、**多模型故障转移**以及**渠道稳定性**（如飞书）方面。

### 2. 版本发布
*   **版本号**: `v0.2.3-nightly.20260320.71ce2196`
*   **状态**: 已发布
*   **注意事项**: 这是一个自动构建的 Nightly 版本，可能包含不稳定性，请谨慎使用。
*   **主要变更**: 涵盖了从 v0.2.3 至当前 main 分支的所有最新提交。
    *   **Full Changelog**: https://github.com/sipeed/picoclaw/compare/v0.2.3...main

### 3. 项目进展
今日代码仓库整合迅速，以下 PR 的合并标志着项目功能的完善与稳定性的提升：

*   **[Agent] 工具注册传递修复** ([#1711](https://github.com/sipeed/picoclaw/pull/1711))
    *   **状态**: 已合并
    *   **影响**: 修复了多代理重构后子代理无法调用工具的严重 Bug。此前因 `ToolRegistry` 为空，所有子代理的工具调用均返回 "tool not found"。
*   **[Documentation] 配置文档更新** ([#1740](https://github.com/sipeed/picoclaw/pull/1740), [#1788](https://github.com/sipeed/picoclaw/pull/1788))
    *   **状态**: 已合并
    *   **影响**: 明确了修改 `AGENTS.md` 等工作区文件无需重启网关；补充了 Agent Binding 路由配置的详细说明，降低了配置复杂度。
*   **[Channel] Telegram 修复** ([#1390](https://github.com/sipeed/picoclaw/pull/1390))
    *   **状态**: 已合并
    *   **影响**: 修复了当 LLM 调用失败或挂起时，Telegram "正在输入..." 状态无法自动结束的问题。
*   **[Security] Exec 工具禁用选项** ([#1621](https://github.com/sipeed/picoclaw/issues/1621))
    *   **状态**: Feature 已关闭/实现
    *   **影响**: 响应安全关切，现在允许用户通过配置完全禁用 `exec` (Shell 执行) 工具，以减少攻击面。

### 4. 社区热点
今日社区讨论主要集中在以下高热度 Issue：

*   **🔥 [Feature] 添加 TTS 和 ASR 语音支持** ([#1648](https://github.com/sipeed/picoclaw/issues/1648))
    *   **热度**: 14 条评论
    *   **摘要**: 社区强烈需求增加语音交互能力。讨论涉及如何集成现有的相关 PR 以及网关层面的音频架构设计。这表明 PicoClaw 正向多模态 AI 助手演进。
*   **🔥 [Bug] OpenRouter/Free 模型配置问题** ([#901](https://github.com/sipeed/picoclaw/issues/901))
    *   **热度**: 12 条评论
    *   **摘要**: 用户反馈在添加 OpenRouter 或免费模型时遇到困难，涉及配置继承和 API 前缀处理的复杂性。
*   **[Agent Refactor] 上下文管理与压缩** ([#1439](https://github.com/sipeed/picoclaw/issues/1439))
    *   **热度**: 6 条评论
    *   **摘要**: 深度探讨了 Agent 的上下文边界、Token 预算及压缩策略，这是长对话场景下的核心痛点。

### 5. Bug 与稳定性
今日报告的关键 Bug 及修复进展：

*   **🚨 [Critical] Anthropic API 400 错误** ([#1792](https://github.com/sipeed/picoclaw/issues/1792))
    *   **现象**: 使用 Claude 模型时返回 400 错误，提示 `tool_result` 重复。
    *   **修复**: 已提交 PR ([#1793](https://github.com/sipeed/picoclaw/pull/1793)) 进行去重和合并逻辑修复。
*   **🚨 [Major] OpenRouter 前缀移除问题** ([#1247](https://github.com/sipeed/picoclaw/issues/1247))
    *   **现象**: OpenRouter Provider 在发送请求时错误移除了 `openrouter/` 前缀。
    *   **状态**: 待解决，影响特定 Provider 的正常使用。
*   **[Channel] 飞书 机器人频繁断连/不回复** ([#1767](https://github.com/sipeed/picoclaw/issues/1767))
    *   **现象**: 飞书连接在后台断开后无自动重连机制。
    *   **状态**: 开放中，用户急需网络层的健壮性增强。
*   **[Launcher] Web UI 输入框禁用** ([#1704](https://github.com/sipeed/picoclaw/issues/1704))
    *   **现象**: 在特定环境下 TUI 启动后，Gateway 无法正常工作，导致 Web UI 不可用。

### 6. 功能请求与路线图信号
*   **Event-driven Hooks System** ([#1795](https://github.com/sipeed/picoclaw/issues/1795), [#1796](https://github.com/sipeed/picoclaw/issues/1796)): 用户希望引入类似 OpenClaw 的 Hooks 系统，以支持事件驱动的自动化（目前仅支持主动调用和定时任务）。这对开发者生态至关重要。
*   **OpenAI API 格式 Channel** ([#1738](https://github.com/sipeed/picoclaw/issues/1738)): 用户希望将 PicoClaw 作为一个 OpenAI 兼容的 API 服务嵌入到现有系统中，这是集成场景的强需求。
*   **Web Dashboard 增强** ([#1797](https://github.com/sipeed/picoclaw/issues/1797)): 请求在 Web 面板中增加 Cron 任务管理和成本统计。
*   **OTel GenAI 支持** ([#1731](https://github.com/sipeed/picoclaw/issues/1731)): 企业级用户提出增加 Open Telemetry 支持，以满足可观测性标准。

### 7. 用户反馈摘要
*   **满意度**: 用户对 **Context Management (上下文管理)** 的重构方向表示关注，认为这是提升长对话体验的关键。
*   **痛点**:
    *   **配置复杂性**: 多个 Issue 反映 Provider（如 OpenRouter, LiteLLM）的配置继承逻辑不直观，导致 API Key 和 Base URL 配置错误。
    *   **移动端/边缘端支持**: Android Termux 和 ARMv7 设备用户反馈启动器（Launcher）无法正常工作或架构不支持。
    *   **调试困难**: 当 Agent 执行工具时缺乏过程反馈，用户面对“黑盒”体验 ([#571](https://github.com/sipeed/picoclaw/issues/571))。

### 8. 待处理积压
*   **Issue #629**: LLM 调用失败后缺少重试机制。这是一个影响稳定性的老问题，至今未完全解决。
*   **Issue #1641**: PicoClaw 运行几天后因 `max_tool_iterations` 错误停止工作，疑似内存或状态累积问题，需长期测试排查。
*   **PR #1460**: OpenAI 兼容性工具调用的序列化修复，已开放较长时间，正在等待合并，涉及严格的 Provider 兼容性。

---
*数据来源: GitHub API (sipeed/picoclaw) | 生成时间: 2026-03-20*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 (2026-03-20)

> 基于 GitHub 数据的 AI 智能体项目每日分析报告

## 1. 今日速览
今日 NanoClaw 项目呈现**极高活跃度**，处于快速迭代期。过去 24 小时内共产生了 32 条 PR 更新和 15 条 Issue 讨论活跃，显示出强劲的开发动力。核心功能演进集中在**多模态交互能力**（如 Telegram 语音转录、Discord 群体协作）、**安全性与合规性加固**（如修复日志泄露、Git Hook 防护）以及**基础设施适配**（如 Linux 无头环境支持）。同时也暴露出 CI 流程中的维护债务，出现多个技能分支合并冲突的自动化报错。

## 2. 版本发布
*今日无新版本发布。*

## 3. 项目进展
今日合并/关闭的关键 PR 及其影响：

*   **[SECURITY] 修复容器错误日志泄露用户 Prompt (#1191)](https://github.com/qwibitai/nanoclaw/pull/1191)**
    *   **状态**: 已关闭
    *   **影响**: 这是一个关键的安全修复。此前 `container-runner.ts` 在容器报错时会将完整的用户输入写入磁盘日志。PR 调整了日志策略，仅在 verbose 模式下记录完整输入，防止敏感数据意外落地。
*   **[OPTIMIZATION] 加速 Docker 容器重启速度 (#651)](https://github.com/qwibitai/nanoclaw/pull/651)**
    *   **状态**: 已关闭
    *   **影响**: 通过将 `docker stop` 的默认超时从 10s 降至 1s，使得 NanoClaw 的服务重启速度提升了约 10 倍（从 ~20s 降至 ~2s），显著改善了开发和部署体验。
*   **[FEATURE] Telegram 语音消息转录支持 (#1269)](https://github.com/qwibitai/nanoclaw/pull/1269)**
    *   **状态**: 已关闭
    *   **影响**: 扩展了 Telegram 通道的能力，允许通过本地 Whisper 服务转录语音消息并发送给 Agent，增强了多模态交互体验。

## 4. 社区热点
今日讨论热度最高、最具风向标的内容：

*   **[RFC] Replace Agent SDK with Claude Code CLI (#1266)](https://github.com/qwibitai/nanoclaw/pull/1266)**
    *   **热度**: 新增 PR，引发架构层面关注
    *   **核心**: 针对近期关于 TOS 合规性的讨论 (#1224)，开发者提出直接在容器中使用 `claude` CLI 二进制文件替代现有的 SDK。这可能会成为 NanoClaw 底层架构的重大转折点，直接影响未来的运行稳定性与官方兼容性。
*   **[Feature] 支持 Git Hook 防绕过 (#1270 / #1271)](https://github.com/qwibitai/nanoclaw/issues/1270)
    *   **热度**: 新开 Issue + 对应 PR
    *   **核心**: 社区敏锐地发现了容器隔离的一个盲点——Agent 可以通过参数跳过 Git Hooks。用户建议引入 PreToolUse Hook 来阻止这种行为，反映了用户将 NanoClaw 用于严肃开发流程（需强代码规范）的强烈需求。

## 5. Bug 与稳定性
今日报告的关键问题：

*   **[CRITICAL] 安全: 容器错误日志包含完整用户 Prompt (#1150)](https://github.com/qwibitai/nanoclaw/issues/1150)**
    *   **状态**: Issue 已关闭 (有 Fix PR #1191)
    *   **描述**: 容器非零退出时，敏感的 User Prompt 会随错误日志写入磁盘。
    *   **进展**: 已有修复方案合并，风险解除。
*   **[HIGH] Linux systemd 用户会话回退机制失效 (#413)](https://github.com/qwibitai/nanoclaw/issues/413)**
    *   **状态**: 开放中
    *   **描述**: 在非 root SSH 登录的 Linux 服务器上，服务设置错误地直接回退到 `nohup`，而不是尝试修复 D-Bus 会话问题。
    *   **影响**: 降低了在 VPS 上部署 NanoClaw 的稳定性体验。
*   **[MEDIUM] Setup 验证未支持 `ANTHROPIC_AUTH_TOKEN` (#853)](https://github.com/qwibitai/nanoclaw/issues/853)**
    *   **状态**: 开放中
    *   **描述**: 官方 Claude Code CLI 使用 `ANTHROPIC_AUTH_TOKEN`，但 NanoClaw 的验证逻辑不识别此 Token，导致验证流程失败。

## 6. 功能请求与路线图信号
用户需求与开发方向分析：

*   **平台兼容性扩展**:
    *   **Podman 支持** ([#957](https://github.com/qwibitai/nanoclaw/issues/957)): 用户希望在文档中增加 Podman 替代 Docker 的说明，这是由于安全和许可原因在 Linux 社区的常见需求。
    *   **无头 Linux 支持** ([#1281](https://github.com/qwibitai/nanoclaw/pull/1281)): PR 已提交，旨在修复 VPS/服务器环境下浏览器打开失败的问题，并优化安装文档。
*   **高级 Agent 能力**:
    *   **Agent Swarm / 多群组协作** ([#1263](https://github.com/qwibitai/nanoclaw/issues/1263), [#1265](https://github.com/qwibitai/nanoclaw/pull/1265)): 社区正在探索让 Agent 参与多个 Telegram 群组或 Discord 频道，以实现跨仓库 Agent 的协同工作。
    *   **混合检索记忆** ([#1283](https://github.com/qwibitai/nanoclaw/pull/1283)): 正在进行中的 PR 试图用 LanceDB 替换现有纯向量搜索，引入 BM25 关键词检索，以解决"查全率"问题。
*   **新通道接入**:
    *   **Email 通道** ([#1251](https://github.com/qwibitai/nanoclaw/pull/1251)): 通过 OpenMail 接入邮件系统。
    *   **Signal 通道** ([#1121](https://github.com/qwibitai/nanoclaw/pull/1121)): 社区贡献了 Signal 协议的支持。

## 7. 用户反馈摘要
从 Issues 中提炼的用户心声：

*   **痛点 - 部署体验**: 用户在 MacOS 和 Linux (VPS) 环境下的部署遇到阻力，特别是 systemd 配置和缺少浏览器 GUI 的情况 (Issues #413, #1281)。
*   **痛点 - 多会话管理**: 有用户表示"只支持即时通讯软件驱动的 Agent 系统对我没用"，并自行开发了 Web 多会话通道 ([#1273](https://github.com/qwibitai/nanoclaw/issues/1273))。这暗示了 NanoClaw 可能需要考虑更通用的 Web UI 接口。
*   **建议 - 安全性**: 用户非常关注隔离容器的安全性，提出了防止 Git Hook 绕过 ([#1271](https://github.com/qwibitai/nanoclaw/pull/1271)) 和 禁用远程控制功能 ([#1126](https://github.com/qwibitai/nanoclaw/pull/1126)) 的请求。

## 8. 待处理积压
需维护者关注的技术债务：

*   **技能分支合并冲突**: 出现了一连串由 `github-actions[bot]` 创建的 Issue (#1261, #1276 - #1279)，主分支的最近几次提交导致 `skill/apple-container` 和 `skill/compact` 两个分支持续合并失败或测试失败。这需要维护者手动解决冲突，防止分支过时废弃。
*   **数据库迁移 Bug**: [#1272](https://github.com/qwibitai/nanoclaw/issues/1272) 指出 Telegram 的回填迁移错误地将所有聊天标记为群组 (`is_group=1`)，这会影响私聊场景的逻辑处理。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 (2026-03-20)

**分析师：** AI 智能体与个人助手领域观察员
**数据来源：** [github.com/nullclaw/nullclaw](https://github.com/nullclaw/nullclaw)
**报告日期：** 2026-03-20

---

## 1. 今日速览
NullClaw 项目在 2026-03-20 展现了极高的活跃度与稳健的迭代速度。过去 24 小时内，项目不仅发布了 **v2026.3.18** 版本，还处理了 26 个代码和问题更新（16 PR + 10 Issue），显示社区与维护团队处于高度协作状态。核心开发重点集中在**多模态适配**（增加 GLM/ZhipuAI、Novita AI 支持）、**协议标准化**（A2A 协议升级至 v0.3.0）以及**运维稳定性**（Docker/Nix 修复）。虽然出现了几个影响体验的 Bug（如内存系统失效、交互式命令卡死），但响应迅速，部分修复已随新版本发布。

---

## 2. 版本发布：v2026.3.18
项目发布了最新的 **v2026.3.18** 版本。本次更新侧重于兼容性修复与生态扩充。

*   **核心变更与修复：**
    *   **[Provider 扩充]** 新增 **Novita AI** 作为 OpenAI 兼容的提供商 ([#621](https://github.com/nullclaw/nullclaw/pull/621))，为用户提供更多低成本模型选择。
    *   **[Docker 修复]** 修正了容器启动配置，将废弃的 `default_provider` 字段迁移至新的 `agents.defaults.model.primary` 结构 ([#636](https://github.com/nullclaw/nullclaw/pull/636))。这解决了用户在拉取最新镜像时遇到的配置报错问题。
    *   **[Nix 环境修复]** 将 Flakes 开发环境固定为 **Zig 0.15.2**，解决了 NixOS 25.11 上的构建失败问题 ([#637](https://github.com/nullclaw/nullclaw/pull/637))。
*   **迁移注意事项：**
    *   Docker 用户需检查配置文件，确保不再使用旧版顶层字段 `default_provider`，参考 [#629](https://github.com/nullclaw/nullclaw/issues/629)。

---

## 3. 项目进展
今日合并了 8 个 PR，项目在协议互操作性、系统调度和配置逻辑方面取得实质性进展。

*   **[A2A 协议升级]** 合并了 **A2A v0.3.0** 协议更新 ([#630](https://github.com/nullclaw/nullclaw/pull/630))。
    *   *进展意义：* 增加了 `rejected`, `auth-required` 等任务状态，移除了旧版别名，并增强了历史记录支持。这表明 NullClaw 正在积极向 Agent 间通信标准化靠拢，为多 Agent 协作打下基础。
*   **[调度系统增强]** 通过 HTTP API 暴露了实时调度器 ([#648](https://github.com/nullclaw/nullclaw/pull/648)) 并允许 Cron 任务省略 command 字段 ([#643](https://github.com/nullclaw/nullclaw/pull/643))。
    *   *进展意义：* 解决了 CLI 与守护进程之间的竞态条件，使得定时任务（Agent Jobs）的管理更加动态和安全，不再依赖手动编辑 JSON 文件。
*   **[配置与身份逻辑修复]** 修复了 AIEOS Identity 无法注入系统提示词的 Bug ([#633](https://github.com/nullclaw/nullclaw/pull/633))。
    *   *进展意义：* 恢复了用户自定义 Agent 人格的功能，增强了 Agent 的个性化能力。
*   **[Channel 修复]** 修复了 Telegram 私聊房间判断错误 ([#634](https://github.com/nullclaw/nullclaw/pull/634)) 和草稿消息重试逻辑 ([#635](https://github.com/nullclaw/nullclaw/pull/635))，提升了即时通讯软件集成的稳定性。

---

## 4. 社区热点
*   **最活跃讨论：[Issue #619](https://github.com/nullclaw/nullclaw/issues/619) - "Improve error message"**
    *   *摘要：* 用户反馈日志中的 `error.ApiError` 信息过于模糊，难以调试。
    *   *分析：* 反映了用户对**可观测性** 的强烈需求。对于复杂的 Agent 流程， vague 的错误信息是提升用户体验的主要障碍。
*   **关注度最高 (👍1): [Issue #612](https://github.com/nullclaw/nullclaw/issues/612) - "NixOS build failed"**
    *   *摘要：* 虽然 PR #637 已修复此问题，但该 Issue 受到了社区点赞，表明 Nix 用户群体在 NullClaw 社区中占有一定比例，且对发行版兼容性非常敏感。

---

## 5. Bug 与稳定性
今日报告了 6 个 Bug，其中 3 个为严重等级，需引起注意。

*   **[High] 内存系统失效 [#646](https://github.com/nullclaw/nullclaw/issues/646)**
    *   *现象：* Agent 无法持久化或召回记忆。
    *   *状态：* OPEN。这直接影响了 Agent 的核心价值（上下文记忆），需优先排查。
*   **[High] 交互式命令导致网关挂起 [#644](https://github.com/nullclaw/nullclaw/issues/644)**
    *   *现象：* 在 Telegram 上运行 `htop`/`btop` 会导致 Gateway 挂死，需强制杀进程。
    *   *状态：* OPEN。涉及进程管理和信号处理，属于运行时稳定性问题。
*   **[Medium] Telegram Draft API 错误 [#626](https://github.com/nullclaw/nullclaw/issues/626)**
    *   *现象：* 大量 `TEXTDRAFT_PEER_INVALID` 错误。
    *   *状态：* CLOSED。Fix 已在 v2026.3.18 中发布 ([#635](https://github.com/nullclaw/nullclaw/pull/635))。
*   **[Medium] OTEL 诊断无法连接 [#638](https://github.com/nullclaw/nullclaw/issues/638)**
    *   *现象：* OpenTelemetry 配置后在容器网络中无法通信。
    *   *状态：* OPEN。

---

## 6. 功能请求与路线图信号
*   **[MCP 兼容性] 允许 localhost HTTP URL [#642](https://github.com/nullclaw/nullclaw/pull/642)**
    *   *状态：* OPEN。
    *   *分析：* 此 PR 允许本地开发环境下使用 `http://` 连接 MCP 服务器，降低了开发调试的门槛。预计会被合并，因为它是开发者的刚需。
*   **[模型支持] Qwen Code Cli 支持 [#647](https://github.com/nullclaw/nullclaw/issues/647)**
    *   *动机：* 丰厚的免费额度。
    *   *分析：* 社区对国产模型和高性价比模型的支持呼声持续存在。
*   **[重磅特性] 自适应智能管道 [#527](https://github.com/nullclaw/nullclaw/pull/527)**
    *   *状态：* OPEN。
    *   *分析：* 这是一个巨大的 Feature，包含 "Turn Scorer" 和 "Skill Router"。如果合并，将赋予 NullClaw 根据历史交互质量自我进化的能力。目前仍在开发中，值得长期关注。

---

## 7. 用户反馈摘要
*   **痛点 - 调试困难：** "I am trying to understand what the problem is... it is frustrating." ([#619](https://github.com/nullclaw/nullclaw/issues/619))。用户在遇到 Agent 报错时，除了通用的 API 错误外，无法获取具体的上下文（如哪个 Provider，什么参数错误）。
*   **场景 - NixOS 用户：** 存在构建环境依赖问题 ([#612](https://github.com/nullclaw/nullclaw/issues/612))，用户对文档与开发环境的同步性有较高要求。
*   **场景 - 模型多样性：** 用户积极尝试接入 ZhipuAI ([#641](https://github.com/nullclaw/nullclaw/pull/641)) 和 Qwen，倾向于使用免费或低成本的模型来运行日常 Agent 任务。

---

## 8. 待处理积压
以下 Issue/PR 长期开放或较为关键，建议维护者关注：

1.  **[PR #527 Adaptive Intelligence Pipeline](https://github.com/nullclaw/nullclaw/pull/527)**: 已开放 6 天。这是一个高价值但高风险的大型 PR，可能需要代码审查资源。
2.  **[Issue #644 Gateway Hangs](https://github.com/nullclaw/nullclaw/issues/644)**: 交互式命令卡死问题属于运行时崩溃隐患，建议尽快定位原因（可能是阻塞式 I/O 未被正确处理）。
3.  **[Issue #646 Memory System](https://github.com/nullclaw/nullclaw/issues/646)**: 记忆功能失效如果属实，将严重影响产品的核心卖点，需优先于功能开发进行修复。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

你好！我是 IronClaw 开源项目分析师。以下是基于 2026-03-20 GitHub 数据整理的项目动态日报。

---

## 📊 IronClaw 项目日报 (2026-03-20)

### 1. 今日速览
IronClaw 项目今日处于**极高活跃度**状态，代码库正在进行大规模的性能优化与架构升级。过去 24 小时内，Issues 和 PR 的更新量均达到 **50 条**，且 Issue 关闭率达到 72%（36/50），表明项目维护团队正积极处理技术债。
*   **核心动态**：项目发布了 **v0.20.0** 版本，重点引入了自修复机制的参数配置及测试故障注入框架。
*   **开发重心**：社区讨论主要集中在新引入的**嵌入式缓存系统的性能问题**（克隆开销、惊群效应）以及由 CI Review 生成的大量代码质量改进建议。
*   **潜在风险**：虽然 v0.20.0 已发布，但仍有用户报告了从旧版本升级时的数据库迁移校验和不匹配问题，需关注后续补丁。

---

### 2. 版本发布
**版本号：v0.20.0**
**发布日期：2026-03-19**

#### 主要更新内容
*   **自愈机制增强**：为 `self-repair` 模块新增了 `stuck_threshold`（卡住阈值）、`store`（存储）及 `builder` 构建器的配置支持 ([#712](https://github.com/nearai/ironclaw/pull/712))，提高了 Agent 长时间运行的稳定性。
*   **测试框架**：新增 `FaultInjector` 故障注入框架，专门用于测试 `StubLlm` 的异常处理能力 ([#1233](https://github.com/nearai/ironclaw/pull/1233))。
*   **网关体验**：统一了设置页面，新增子标签页支持，改善了用户配置体验。

---

### 3. 项目进展
今日有 22 个 PR 被合并或关闭，主要进展集中在核心能力的优化和基础设施的健壮性提升：

*   **性能优化**：引入并改进了 **LRU 嵌入式缓存** ([#1423](https://github.com/nearai/ironclaw/pull/1423), [#235](https://github.com/nearai/ironclaw/pull/235))。通过内存缓存避免重复的 HTTP 嵌入调用，显著提升了工作空间搜索的响应速度，并支持批量请求的部分命中逻辑。
*   **基础设施重构**：OAuth 和 MCP 认证流程实现了通用化 ([#1375](https://github.com/nearai/ironclaw/pull/1375))，统一了 WASM 工具和 MCP 服务器的托管认证流程，减少了代码重复。
*   **CI/CD 自动化**：多个 "staging-promotion" PR (如 [#1428](https://github.com/nearai/ironclaw/pull/1428), [#1439](https://github.com/nearai/ironclaw/pull/1439)) 显示项目已建立起高效的自动合并流水线，能够批量通过 CI 审查并将暂存区代码自动提升至主分支。
*   **架构演进**：提交了两个超大规模 (XL) 的 PR，涉及**自适应学习系统** ([#1187](https://github.com/nearai/ironclaw/pull/1187))（技能综合、用户画像、会话搜索）和基于所有者的全任务权限管理 ([#1440](https://github.com/nearai/ironclaw/pull/1440))，预示着 Agent 能力向更高阶的个性化和自动化迈进。

---

### 4. 社区热点
今日讨论热度最高的内容主要集中在**新引入缓存机制的性能缺陷**及**社区功能请求**：

*   **[CRITICAL] 缓存机制严重性能缺陷 ([#1429](https://github.com/nearai/ironclaw/issues/1429))**
    *   **摘要**：CI 审查指出，刚合并的嵌入式缓存在每次命中时都会克隆嵌入向量，导致严重的性能损耗。
    *   **反响**：此问题被标记为 CRITICAL (100)，热度极高。目前已有修复 PR [#1438](https://github.com/nearai/ironclaw/pull/1438) 提出使用 `Arc` 来解决克隆问题，体现了社区对高性能的极致追求。
*   **[FEATURE] Slack Socket Mode 支持 ([#1155](https://github.com/nearai/ironclaw/issues/1155))**
    *   **摘要**：用户请求支持 Slack 的 "Socket Mode"，以便在不开放入站流量的情况下接收消息。
    *   **关联**：虽然 Issue 仍处于 OPEN 状态，但相关 PR [#333](https://github.com/nearai/ironclaw/pull/333) (已关闭) 曾尝试解决此问题，社区仍在等待最终合并。

---

### 5. Bug 与稳定性
今日报告的 Bug 大多来自自动化 CI 审查，以下是按严重程度排列的关键问题：

*   **[CRITICAL] 版本不匹配**：Telegram 工件 URL 存在版本号不匹配问题 ([#1414](https://github.com/nearai/ironclaw/issues/1414))，可能导致资源加载失败。
*   **[HIGH] 数据库迁移失败**：用户反馈从 v0.18.0 升级至 v0.19.0 时，PostgreSQL 数据库出现 `V6__routines` 迁移校验和不匹配的错误 ([#1328](https://github.com/nearai/ironclaw/issues/1328))，目前已有 2 人点赞，急需修复。
*   **[HIGH] 缓存并发问题**：除了克隆开销，缓存机制还被发现存在 "Thundering herd"（惊群效应）问题 ([#1431](https://github.com/nearai/ironclaw/issues/1431))，即并发请求同一未缓存 key 时会触发重复计算。
*   **[HIGH] 逻辑漏洞**：
    *   N+1 查询反模式：在密钥凭证注入中发现性能瓶颈 ([#858](https://github.com/nearai/ironclaw/issues/858))。
    *   Token 预算未持久化：`max_tokens` 未写入数据库 ([#814](https://github.com/nearai/ironclaw/issues/814))。
    *   无界循环：部分循环缺少取消令牌 ([#870](https://github.com/nearai/ironclaw/issues/870))。

---

### 6. 功能请求与路线图信号
从活跃的 PR 中可以捕捉到项目未来的几个关键方向：

*   **智能化与自适应学习**：PR [#1187](https://github.com/nearai/ironclaw/pull/1187) 提出建立自适应学习系统，包括技能合成和用户画像。这表明 IronClaw 正试图从单纯的 "执行工具" 向 "学习用户习惯" 演进。
*   **更精细的路由与过滤**：
    *   **MCP 服务器过滤**：PR [#1378](https://github.com/nearai/ironclaw/pull/1378) 和 [#1243](https://github.com/nearai/ironclaw/pull/1243) 都在致力于实现基于频道的 MCP/Built-in 工具过滤。这意味着未来的 Agent 将能根据对话来源（如 Slack 或 研究频道）智能调用不同的工具集。
    *   **PDF 处理升级**：PR [#1435](https://github.com/nearai/ironclaw/pull/1435) 计划用 `pdf_oxide` 替换 `pdf-extract`，以获得更好的布局感知和更快的速度。
*   **失败处理结构化**：PR [#236](https://github.com/nearai/ironclaw/pull/236) 提议为失败/卡住的任务引入结构化的 `FallbackDeliverable`，这将大幅提升系统在处理错误时的透明度和用户体验。

---

### 7. 用户反馈摘要
*   **痛点**：升级体验不佳。Issue [#1328](https://github.com/nearai/ironclaw/issues/1328) 反映的数据库迁移报错表明，当前版本的数据库 schema 变更管理可能存在疏漏，影响了老用户的升级路径。
*   **场景**：多频道部署需求。用户 ([#1155](https://github.com/nearai/ironclaw/issues/1155), [#1378](https://github.com/nearai/ironclaw/pull/1378)) 强烈希望在不同的渠道（Slack, Telegram, Web）上对工具权限和能力进行隔离，反映出 IronClaw 正被用于复杂的企业级多渠道环境。

---

### 8. 待处理积压
以下为活跃但长时间未合并的重要 PR，建议维护者优先关注：
*   **[#1187](https://github.com/nearai/ironclaw/pull/1187) (feat: adaptive learning system)**：虽然规模巨大 (XL)，但这是提升 Agent 核心智能的关键特性，自 3 月 14 日提出以来尚未合并。
*   **[#1093](https://github.com/nearai/ironclaw/pull/1093) (fix: managed tunnels)**：修复了隧道管理功能完全失效的问题，对依赖 webhook 的用户至关重要，自 3 月 13 日待定。
*   **[#635](https://github.com/nearai/ironclaw/pull/635) (fix: orphaned tool_results)**：修复 Worker 执行工具时的严重 Bug，防止 API 返回空响应，自 3 月 6 日开放至今。

---
**分析师结语**：IronClaw 项目正处于快速迭代期，v0.20.0 的发布带来了令人期待的配置灵活性。然而，新引入的缓存机制带来的性能回退（而非提升）是一个警钟，提醒团队在合并大型性能优化 PR 时需进行更严格的基准测试。同时，数据库迁移问题需尽快修复以保障用户升级信心。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 (2026-03-20)

## 1. 今日速览
今日 LobsterAI 项目处于**极高活跃度**状态，社区响应热烈。
- **数据表现**：过去24小时内新增/活跃 Issues 达 19 条，待处理与已合并 PR 共 33 条，并发布了最新的 v2026.3.19 版本。
- **核心动向**：项目正经历大规模的 Bug 修复与体验优化阶段，特别是针对国际化 (I18N)、暗黑模式适配以及 OpenAI 新模型兼容性的集中攻关。
- **稳定性预警**：新版本发布后，关于 OpenClaw 引擎频繁重启和旧版本升级导致的兼容性问题（#540, #500）引发了较多用户关注，需引起重视。

---

## 2. 版本发布
**版本号**: `2026.3.19`
**发布时间**: 2026-03-19
**核心变更**:
- **依赖升级**: 升级了企业微信相关依赖 (PR #482)。
- **引擎优化**: 针对 OpenClaw Gateway 进行了重启逻辑修复 (PR #484)。
- **文档完善**: 更新了 AGENTS.md，新增 OpenClaw 和国际化指南 (PR by @nmgwddj)。
**注意事项**: 尽管该版本修复了网关重启逻辑，但部分用户反馈 (Issue #540) 仍遇到频繁重启问题，建议在升级前备份配置。

---

## 3. 项目进展
今日合并与推进的 PR 主要集中在代码质量提升与功能修复，项目在稳定性和扩展性上迈进一步。

- **性能优化 (PR #533)**: 修复了 CoWorkerStore 中的 N+1 查询问题，并实现了 `getConfig` 的批量查询，显著减少了数据库 RTT，提升了内存删除循环的效率。
- **关键修复 (PR #515)**: 统一了 OpenAI 官方 Provider 的参数，将已废弃的 `max_tokens` 替换为 `max_completion_tokens`，解决了新模型无法报错的问题。
- **国际化完善 (PR #536, #532, #529)**: 集中修复了多处界面语言覆盖不全和硬编码问题，优化了切换多语言时的体验，并对 MCP 设置进行了暗黑模式适配。
- **功能扩展 (PR #538, #537)**: 新增了 `qrcode` (二维码生成) 和 `github-profile` (GitHub 信息查询) 两个 Skill，丰富了 Agent 的工具能力。

---

## 4. 社区热点
今日讨论热度最高的议题集中在用户体验 (UX) 优化和核心功能请求。

- **[Feature Request] 支持多智能体协调 (Issue #541)**
  - **链接**: [#541](https://github.com/netease-youdao/LobsterAI/issues/541)
  - **讨论**: 用户强烈建议引入多智能体系统，支持 Agent 之间的相互调用与协调。这代表了从单 Agent 编排向多 Agent 协作系统演进的需求，可能是未来的重要路线图方向。

- **[UX] 启动界面文案优化 (Issue #519)**
  - **链接**: [#519](https://github.com/netease-youdao/LobsterAI/issues/519)
  - **讨论**: 用户详细分析了启动界面文案（如 "Starting OpenClaw gateway..."）和进度条展示带来的困惑，提出了具体的交互改进建议。

- **[Feature Request] 双内核切换 (Issue #497)**
  - **链接**: [#497](https://github.com/netease-youdao/LobsterAI/issues/497)
  - **讨论**: 社区呼吁官方支持 OpenClaw 和 CoWorker 两种内核的自由切换，以满足不同场景下的性能与功能需求。

---

## 5. Bug 与稳定性
今日报告的 Bug 数量较多，其中包含严重的阻碍性问题。

- **[严重] OpenClaw 频繁重启 (Issue #540)**
  - **描述**: 3.19 版本中，OpenClaw 网关每隔几十秒自动重启，导致服务无法使用。
  - **状态**: 新报 Issue，待修复。

- **[严重] 兼容性崩溃 (Issue #500)**
  - **描述**: Windows 11 环境下从 2.2 升级至 3.17 后无法运行，且出现配置丢失。
  - **状态**: 待处理。

- **[中等] 模型兼容性 (Issue #501)**
  - **描述**: 无法兼容 OpenAI 最新模型，报错 `max_tokens` 不支持。
  - **状态**: ✅ 已修复 (PR #515 已合并)。

- **[中等] 飞书机器人不回复 (Issue #511)**
  - **描述**: 3.17 版本配置后飞书机器人无响应，但企微正常。
  - **状态**: 待排查。

- **[中等] 流式输出缺失 (Issue #521)**
  - **描述**: 飞书集成无法像 ClawX 那样实时流式返回消息，体验不佳。
  - **状态**: 待优化。

---

## 6. 功能请求与路线图信号
根据 Issues 与 PR 的关联分析，以下功能可能被纳入近期版本：

- **双内核支持 (Issue #497)**: 代码中已有相关集成，用户强烈期望UI层支持切换。
- **多智能体协作 (Issue #541)**: 虽暂无对应 PR，但作为高级 Agent 编排能力，符合产品长期演进方向。
- **ARM64 & Docker 支持 (Issue #539)**: 服务器部署需求明确，涉及基础设施适配。
- **沙箱功能回归 (Issue #496)**: 用户反馈 3.17 版本移除了沙箱功能，PR #523 ("no sandbox") 显示这可能是已知的技术债务或架构调整。

---

## 7. 用户反馈摘要
- **痛点**: 新版本在 Windows 和部分 macOS 环境下存在稳定性隐患（重启、崩溃），升级体验不够平滑。
- **体验**: 国际化和暗黑模式的适配细节仍需打磨，多处硬编码影响非中文用户。
- **期待**: 用户对多智能体、双内核切换等“高阶”功能表现出浓厚兴趣，说明用户群体正在从“尝鲜”转向“深度使用/生产环境部署”。

---

## 8. 待处理积压
- **Issue #498**: 长对话后 AI 重复回复上一条内容 (疑似 Memory 压缩逻辑错误)。
- **Issue #531**: 多处硬编码导致 I18N 支持不完善 (虽有 PR #532 覆盖部分，但尚未完全合并/关闭)。
- **Issue #526**: 部分 Skill 缺少 version 字段 (✅ 已有 PR #534 修复，待合并)。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw 项目日报 (2026-03-20)

## 1. 今日速览
TinyClaw 项目今日处于**低活跃度维护**状态。过去 24 小时内无新 Issue 提出或关闭，代码库中增加了 2 个新的 Pull Requests（PR），暂无合并记录。开发重点集中在核心架构的重构与特定功能模块（Office 工作区）的交互体验优化上，显示出项目正致力于代码库的长期可维护性与用户体验的打磨。

## 2. 版本发布
暂无新版本发布。

## 3. 项目进展
今日无 PR 合并，但有两项重要的开发任务正在推进中，预示着未来的架构升级：

*   **核心架构重构 (PR #242)**: 开发者 `jlia0` 提交了对核心调用逻辑的重构方案。该方案旨在将 `invoke.ts` 中特定于提供商的 CLI 调用逻辑提取到独立的适配器模块中。
    *   **影响**: 此举将引入标准化的 `AgentAdapter` 接口，并实现提供商的自动注册。这显著降低了核心文件的复杂度（`invoke.ts` 代码量减少），为未来支持更多 AI 提供商（Claude, Codex, OpenCode 等）打下更灵活的基础。
    *   **链接**: [refactor(core): extract CLI logic into adapter pattern #242](https://github.com/TinyAGI/tinyagi/pull/242)

*   **交互体验优化 (PR #212)**: 贡献者 `mczabca-boop` 持续推进对 `/office` 实时工作区的重新设计。
    *   **影响**: 该 PR 于 3 月 13 日创建，昨日更新，旨在重新设计 `/office` 的体验。虽然具体改动细节待审阅，但表明项目团队正在优化办公场景下的交互效率。

## 4. 社区热点
今日无新增 Issues，热点主要集中在待审核的 PR 上：

*   **架构解耦讨论 (PR #242)**: 这是今日最具技术影响力的动态。虽然暂无评论，但该 PR 试图解决单体文件过于臃肿的问题。这是典型的“技术债偿还”工作，对于吸引新贡献者降低入门门槛至关重要。
*   **办公场景优化 (PR #212)**: 该 PR 虽然提出时间较早，但昨日有更新动作，说明维护者正在积极迭代此功能。对于关注 TinyClaw 办公能力的用户来说，这是值得关注的动态。

## 5. Bug 与稳定性
今日无新增 Bug 报告。
PR #242（核心重构）属于高风险变更，建议项目维护者在合并前进行充分的单元测试和集成测试，以防止适配器模式引入新的调用错误。

## 6. 功能请求与路线图信号
从 PR 动态分析，项目路线图主要聚焦于两个方向：
1.  **内部架构升级**: 向“适配器模式”转变，这意味着 TinyClaw 未来可能更轻松地接入新的 LLM 提供商或工具。
2.  **垂直场景深化**: `/office` 模块的重设计表明“Office/办公辅助”是项目的核心高频场景之一，未来可能会看到更多针对该场景的补丁。

## 7. 用户反馈摘要
由于今日无新 Issue 和评论，暂无直接的用户反馈数据。
*注：PR #212 提及“redesign”，暗示旧版 `/office` 体验可能存在操作不便或布局问题，此次更新可能是对潜在用户反馈的响应。*

## 8. 待处理积压
建议关注以下待合并项，以免阻塞开发流：
*   **[PR #242](https://github.com/TinyAGI/tinyagi/pull/242)**: 核心重构请求。此类涉及底层的改动若长时间处于 Open 状态，可能会导致后续开发产生代码冲突，建议优先审阅。
*   **[PR #212](https://github.com/TinyAGI/tinyagi/pull/212)**: 办公工作区重设计。该 PR 已存在一周左右，需确认是否在等待设计定稿或具体反馈。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

以下是基于 **2026-03-20** 数据的 Moltis 项目动态日报：

---

### 1. 今日速览
过去 24 小时内，Moltis 项目保持了较高的开发活跃度，社区共提交了 **7 个** 代码与讨论更新。虽然暂无新版本发布，但项目在 **安全性增强**、**跨平台兼容性修复** 以及 **模型生态扩展** 三个维度上均有实质性进展。社区讨论主要集中在防止 AI 智能体绕过 Git 钩子的安全机制上，同时出现了针对 Windows 平台的文件锁修复以及新增 Novita AI 提供商的代码提交。目前待合并的 PR（3 个）多于新报告的 Bug（1 个），显示项目维护者对代码响应积极，整体健康度良好。

---

### 2. 版本发布
**暂无新版本发布**。
*截至当前数据快照，过去 24 小时内未检测到新的 Release 标签或版本公告。*

---

### 3. 项目进展
今日有 **3 个新 PR 提交**，旨在推动功能改进与缺陷修复，目前均处于待合并状态：

*   **安全机制增强**：提交了 `feat: add block-no-verify PreToolUse hook` ([#455](https://github.com/moltis-org/moltis/pull/455))。该 PR 引入了一个关键的 PreToolUse 钩子，旨在防止 AI 智能体（Agent）在执行 `git commit` 或 `git push` 时使用 `--no-verify` 标志绕过本地的质量检查门禁（如 pre-commit 钩子）。这对确保 AI 生成代码的安全性具有重要意义。
*   **跨平台稳定性修复**：提交了 `fix(sessions): replace append(true) ...` ([#436](https://github.com/moltis-org/moltis/pull/436))。该 PR 解决了 [#434](https://github.com/moltis-org/moltis/issues/434) 中报告的 Windows 文件锁死问题。由于 Rust 标准库在 Windows 下对追加模式的特定限制，该修复通过改用 `write(true)+seek` 模式避免了 `LockFileEx os error 5` 错误，显著改善了 Windows 用户的使用体验。
*   **模型生态扩展**：提交了 `feat(providers): add Novita AI` ([#451](https://github.com/moltis-org/moltis/pull/451))。该代码为 Moltis 增加了 Novita AI 作为 OpenAI 兼容的 LLM 提供商，并注册了包括 `deepseek-v3.2` 在内的三个新模型，进一步丰富了用户的模型选择。

---

### 4. 社区热点
今日讨论的热点集中在 **AI Agent 的行为管控** 与 **工具搜索体验**：

*   **🔥 最热讨论**：[#313 Tool search](https://github.com/moltis-org/moltis/issues/313)
    *   **状态**：Open（Enhancement）
    *   **热度**：6 条评论，2 👍
    *   **分析**：这是一个长期活跃的功能请求，用户强烈希望在 Moltis 中增加“工具搜索”功能。尽管该 Issue 创建于 3 月初，但昨日（03-19）仍有更新和讨论，说明该需求是当前用户痛点之一。
*   **新晋关注**：[#454 Add block-no-verify hook](https://github.com/moltis-org/moltis/issues/454)
    *   **状态**：Open
    *   **分析**：该 Issue 由 [#455](https://github.com/moltis-org/moltis/pull/455) PR 配合提出，直接针对 AI Agent 绕过 Git 规范的行为。这反映出用户不仅关注“能不能用”，更开始深度关注 AI 编码过程中的“合规性与安全性”。

---

### 5. Bug 与稳定性
今日报告了 **1 个** 新 Bug，涉及插件系统的逻辑完整性：

*   **[Bug] #452: Skills with invalid name silently omitted from manifest**
    *   **严重程度**：中等
    *   **问题描述**：当一个技能包名称无效但 Slug 有效时，它会被解压到 `installed-skills` 目录，但在生成 `skills-manifest.json` 时会被静默忽略。
    *   **影响**：导致用户安装技能后无法在 Moltis 中看到或使用它，且没有任何错误提示，排查困难。
    *   **修复状态**：暂无关联 Fix PR。

---

### 6. 功能请求与路线图信号
从今日的 Issues 和 PRs 中，可以观测到以下可能纳入未来版本的信号：

*   **Git 安全工作流**：[#455](https://github.com/moltis-org/moltis/pull/455) 的提交表明，官方正在考虑将 Agent 的 Git 操作纳入更严格的管理，未来可能会默认集成更多“防呆”机制。
*   **企业级/多 Agent 管理需求**：[#453 Possible over load of one managerial agent](https://github.com/moltis-org/moltis/issues/453) 提出了关于“单个管理 Agent 过载”以及“为企业用途创建更多 Agent”的讨论。这暗示用户正尝试将 Moltis 应用于更复杂的商业场景，可能催生对多 Agent 编排或负载均衡功能的需求。

---

### 7. 用户反馈摘要
*   **痛点**：Windows 用户在会话管理中遭受文件锁错误（[#434](https://github.com/moltis-org/moltis/issues/434)），目前已有待合并的修复方案。
*   **安全焦虑**：用户意识到 AI Agent 可能无意中破坏代码规范（绕过 Git Hooks），并主动提议解决方案（[#454](https://github.com/moltis-org/moltis/issues/454)），显示出专业开发者对工具可控性的高要求。
*   **新模型接入**：社区积极贡献适配器接入 Novita AI ([#451](https://github.com/moltis-org/moltis/pull/451))，表明用户希望在一个客户端中整合更多样化的模型资源。

---

### 8. 待处理积压
*   **功能请求**：[#313 Tool search](https://github.com/moltis-org/moltis/issues/313) 虽然活跃度高，但已开启多日尚未关闭/解决，建议维护者评估纳入下一里程碑。
*   **新 Bug**：[#452 Invalid name skills unpacking issue](https://github.com/moltis-org/moltis/issues/452) 需关注，静默失败机制会对用户体验造成负面影响，建议尽快确认并安排修复。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 (2026-03-20)

## 1. 今日速览
CoPaw 项目今日处于**极度活跃**的发布后维护期，过去 24 小时内处理了 50 条 Issues 和 50 条 PRs，显示出社区对首个正式版 `v0.1.0` 的极高关注度。随着 v0.1.0 正式版的发布，项目实现了架构上的重大升级（多智能体、多工作空间），但同时也面临着显著的稳定性挑战。目前社区反馈主要集中在版本升级后的兼容性问题（如配置导入失败、上下文溢出报错）以及部分通道（飞书、QQ、Telegram）的消息处理 Bug。维护团队反应迅速，已针对死锁、Swagger 文档丢失、音频处理等关键问题提交了修复 PR。

## 2. 版本发布
今日发布 **2 个新版本**，标志着 CoPaw 进入了一个新的成熟阶段：

*   **[v0.1.0](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0) (正式版)**
    *   **核心架构升级**：引入 **Multi-Agent / Multi-Workspace（多智能体/多工作空间）架构**。支持同时运行多个 Agent，每个 Agent 拥有独立的配置、记忆、技能和工具。
    *   **功能特性**：新增控制台 Agent 选择器，便于在不同工作空间间切换。
    *   **影响**：这是一个里程碑式的更新，极大地增强了 CoPaw 处理复杂多任务场景的能力。

*   **[v0.1.0-beta.4](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0-beta.4)**
    *   **控制台增强**：支持多模态消息，包括图片和文件上传 ([#1772](https://github.com/agentscope-ai/CoPaw/pull/1772))。
    *   **模型修复**：修复了 `create_local_chat_model` 的导入错误 ([#1784](https://github.com/agentscope-ai/CoPaw/pull/1784))。

## 3. 项目进展
今日有 **28 条 PRs 被合并或关闭**，项目在功能丰富度和稳定性方面均有推进：

*   **生态扩展**：
    *   合并了 **Agents Square (Agent 广场)** 源浏览和导入流程的前后端实现 ([#1883](https://github.com/agentscope-ai/CoPaw/pull/1883))，这将极大地方便用户发现和共享 Agent 配置。
    *   新增 **通道路由** 功能 ([#1889](https://github.com/agentscope-ai/CoPaw/pull/1889))，允许根据规则将不同来源的消息分发至不同的 Agent，实现单一 Bot 服务多用户的精细化管理。
    *   为 **小易通道** 新增了文件和图片支持 ([#1885](https://github.com/agentscope-ai/CoPaw/pull/1885))。
*   **底层优化**：
    *   引入了 Token 认证系统 ([#181](https://github.com/agentscope-ai/CoPaw/pull/181))，提升了 API 的安全性。
    *   更新了工具结果压缩 配置 ([#1867](https://github.com/agentscope-ai/CoPaw/pull/1867))，优化了长对话中的内存管理。
*   **视觉与文档**：
    *   将 CoPaw Logo 添加至官网 ([#1878](https://github.com/agentscope-ai/CoPaw/pull/1878))，提升品牌识别度。

## 4. 社区热点
今日讨论最热烈的话题集中在 v0.1.0 版本的升级体验和通道兼容性上：

*   **[#1895 创空间升级失败](https://github.com/agentscope-ai/CoPaw/issues/1895)** (5 comments): 用户反映从 beta3 升级到 v0.1.0 正式版后出现失败，这可能是数据库迁移或配置文件格式变更导致的，是当前最紧急的阻碍性问题。
*   **[#1873 升级后 Context Window 报错](https://github.com/agentscope-ai/CoPaw/issues/1873)** (5 comments): 更新到 v0.1.0b3 后报错 `context window exceeds limit (2013)`。这可能意味着新版本在上下文处理逻辑或 Token 计算上存在回归，导致即使是很短的对话也触发限制。
*   **[#1827 任务卡死](https://github.com/agentscope-ai/CoPaw/issues/1827)** (5 comments): v0.1.0b3 执行任务时出现卡死现象，用户提供了详细的 UI 截图，疑似异步任务处理或阻塞 I/O 的问题。
*   **[#1846 “是不是凉了？”](https://github.com/agentscope-ai/CoPaw/issues/1846)** (3 comments): 虽然该 Issue 已关闭（带有讽刺意味），但它反映了社区对高频率更新节奏的期待。项目随后发布的 v0.1.0 也有力地回应了这一关切。

## 5. Bug 与稳定性
今日报告的 Bug 数量较多，部分为新版本引入的回归问题：

*   **【严重】死锁与性能问题**
    *   **[#1774 CPU 占用异常/死循环](https://github.com/agentscope-ai/CoPaw/issues/1774)**: 报告在 0.0.7 版本中，内存压缩钩子 (`ToolResultCompactor`) 陷入无限循环。**已有 Fix PR**: [#1893](https://github.com/agentscope-ai/CoPaw/pull/1893) 提议将 `threading.Lock` 替换为 `asyncio.Lock` 以解决事件循环阻塞问题。
*   **【高危】通道消息处理失败**
    *   **[#1516 Telegram 语音消息不支持](https://github.com/agentscope-ai/CoPaw/issues/1516)**: `AudioContent` 未能正确转换，导致无法处理语音。**已有 Fix PR**: [#1896](https://github.com/agentscope-ai/CoPaw/pull/1896)。
    *   **[#1770 飞书通道不回消息](https://github.com/agentscope-ai/CoPaw/issues/1770)**: 从 0.0.7 升级到 0.1.0b2 后出现错误，日志显示与 tokenizer 路径或认证有关。
    *   **[#1815 发送消息报错 400](https://github.com/agentscope-ai/CoPaw/issues/1815)**: 使用 Aliyun Coding Plan/Kimi 模型时出现参数错误。
*   **【中等】功能异常**
    *   **[#1829 Cron 任务状态错误](https://github.com/agentscope-ai/CoPaw/issues/1829)**: 任务被取消后状态显示为 "success" 而非 "cancelled"。**已有 Fix PR**: [#1894](https://github.com/agentscope-ai/CoPaw/pull/1894)。
    *   **[#1847 Swagger 文档无法访问](https://github.com/agentscope-ai/CoPaw/pull/1847)**: SPA 路由覆盖了 API 文档路由。**已有 Fix PR**: [#1847](https://github.com/agentscope-ai/CoPaw/pull/1847)。

## 6. 功能请求与路线图信号
社区不仅限于报错，也提出了一些增强功能的请求：

*   **多模态与长文本**: **[#1789](https://github.com/agentscope-ai/CoPaw/pull/1789)** 提出增加本地嵌入模型支持（如 Qwen3-VL, BGE），以实现隐私友好的本地化长期记忆检索。
*   **QQ 频道支持**: **[#1641](https://github.com/agentscope-ai/CoPaw/issues/1641)** 请求支持 QQ 频道的机器人私信处理，这反映了 QQ 平台政策变化后用户的新需求。
*   **调试体验**: **[#1859](https://github.com/agentscope-ai/CoPaw/issues/1859)** 用户希望能直接使用 Python/VSCode 调试 CoPaw 的内部逻辑，以便干预模型输出。

## 7. 用户反馈摘要
*   **痛点**: **版本升级的阵痛**。从 0.0.7 系列升级到 0.1.0 系列时，大量用户遇到了配置不兼容、连接失败、甚至服务崩溃的问题。特别是 `pip` 安装版本与 Web 提示版本不一致的问题 ([#1866](https://github.com/agentscope-ai/CoPaw/issues/1866))，增加了用户的困惑。
*   **满意度**: 用户对于 **v0.1.0 正式版**带来的“多智能体”架构表示了极大的兴趣和期待 ([#153](https://github.com/agentscope-ai/CoPaw/issues/153))，认为这是 CoPaw 区别于其他 Agent 框架的关键。
*   **场景**: 许多用户正在尝试将 CoPaw 集成到 **钉钉、飞书、Discord、Telegram** 等办公或社交软件中，且倾向于使用 **本地模型 (Ollama/Llama.cpp)** 以降低成本或保护隐私。

## 8. 待处理积压
*   **[#902 Discord 语音消息发送失败](https://github.com/agentscope-ai/CoPaw/issues/902)**: 自 3 月 7 日提出至今仍未合并修复，涉及 `.ogg` 格式支持问题。
*   **[#676 MCP HTTP 形式支持](https://github.com/agentscope-ai/CoPaw/issues/676)**: 用户尝试通过 HTTP 配置 MCP 服务时遇到 "Unprocessable Entity" 错误，目前仅有部分修复（环境变量占位符），协议支持尚待完善。
*   **[#1258 心流 iFlow 大模型无响应](https://github.com/agentscope-ai/CoPaw/issues/1258)**: 测试连接正常但聊天无响应，涉及第三方平台的兼容性排查，自 3 月 11 日以来进展缓慢。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

**ZeptoClaw 项目日报**
**日期：** 2026-03-20
**分析师：** AI 智能体与开源助手观察员

---

### 1. 今日速览
ZeptoClaw 项目在过去 24 小时内保持了较高的**开发活跃度**，但**发布节奏**暂时放缓。虽然今日没有新版本发布，但核心功能的迭代正在紧密进行中。社区贡献者 Alex-wuhu 提交了新的 LLM 提供商适配代码，显示出生态扩张能力。与此同时，核心的 Agent Client Protocol (ACP) 实现进入了关键的 Bug 修复与完善阶段，涉及 HTTP 通道与 stdio 的底层语义修正。目前有 3 个 PR 处于待合并状态，预示着下一个版本可能包含重要的功能补齐和开发体验改进。

### 2. 版本发布
今日无新版本发布。

### 3. 项目进展
尽管过去 24 小时内没有 PR 被合并，但以下关键功能的推进显示了项目当前的研发重心：

*   **基础设施与生态扩展：** 社区贡献者发起了 **[#390 feat(providers): add Novita AI provider](https://github.com/qhkm/zeptoclaw/pull/390)**，旨在为 ZeptoClaw 接入 Novita AI 作为新的 OpenAI 兼容 LLM 提供商。该 PR 遵循了现有的接入模式（如 xAI, DeepSeek），支持标准的 API Key 环境变量配置。
*   **开发者体验：** **[#287 chore: Dev tools for consistent pre-PR state](https://github.com/qhkm/zeptoclaw/pull/287)** 在今日获得了更新。该 PR 致力于统一开发与测试环境，确保贡献者在提交代码前能通过一致的 `cargo test` 和 `cargo clippy` 检查，这将显著提升代码合并的效率和稳定性。
*   **核心协议：** **[#356 feat(channels): ACP stdio + HTTP implementation](https://github.com/qhkm/zeptoclaw/pull/356)** 继续活跃中。这是一个重量级的功能 PR，引入了 ACP (Agent Client Protocol) 的 stdio 和 HTTP 通道实现，目前正在完善细节。

### 4. 社区热点
今日社区讨论主要集中在 **Agent Client Protocol (ACP)** 的实现细节与稳定性上：

*   **Issue #388 - [bug, area:channels] bug(channels): fix ACP HTTP initialize and notification semantics**
    *   **链接：** [qhkm/zeptoclaw#388](https://github.com/qhkm/zeptoclaw/issues/388)
    *   **热度：** 过去 24 小时内唯一活跃的 Issue，含有 2 条评论。
    *   **分析：** 该 Issue 直接指出了正在开发中的 PR #356 存在的两个关键协议错误。主要涉及 ACP HTTP 初始化标志的并发安全性（全局 flag 导致后续客户端可能跳过握手）以及 HTTP 通知响应体的处理问题。这表明开发团队与社区正在紧密协作，在功能正式合并前力求协议层的严谨性。

### 5. Bug 与稳定性
*   **高危：** ACP HTTP 通道握手逻辑存在并发安全风险。
    *   **详情：** 如 **[#388](https://github.com/qhkm/zeptoclaw/issues/388)** 所述，当前的 HTTP 初始化实现使用了单一的全局 flag。这意味着在多客户端场景下，一旦第一个客户端完成初始化，后续的客户端可以直接绕过 `session/new` 等握手步骤调用接口，破坏了协议的安全性与完整性。
    *   **状态：** 已有明确的 Issue 定位，预计将在 PR #356 合并前修复。
*   **中危：** HTTP 通知响应体语义错误。
    *   **详情：** HTTP 通知当前接收响应体，这可能不符合通知的语义或导致客户端处理异常。
    *   **状态：** 同样记录于 Issue #388。

### 6. 功能请求与路线图信号
*   **LLM 提供商多元化：** PR #390 (Novita AI) 的出现表明项目路线图将继续致力于兼容主流及新兴的 LLM 提供商，保持对 AI 生态的广泛接入能力。
*   **ACP 协议支持：** PR #356 和 Issue #388 的互动清晰地表明，“Agent Client Protocol”是当前版本最高优先级的功能，项目正致力于让 ZeptoClaw 成为符合 ACP 标准的 Agent。

### 7. 用户反馈摘要
从 Issue #388 的评论可以看出，核心开发者对协议的正确性有极高要求。虽然这不是普通用户的反馈，但从技术角度反映出用户（或协议对接方）对于 **ACP HTTP 通道稳定性** 的关注，特别是在并发调用和握手流程上的严谨性是目前的痛点所在。

### 8. 待处理积压
以下 PR 长期开放且今日有更新，建议维护者优先关注：
*   **[#356 ACP stdio + HTTP implementation](https://github.com/qhkm/zeptoclaw/pull/356)** (创建于 3月13日)：这是通往 ACP 标准化的关键路径，建议尽快解决关联的 Bug (Issue #388) 后推进合并。
*   **[#287 Dev tools](https://github.com/qhkm/zeptoclaw/pull/287)** (创建于 3月09日)：改善工程基础设施的 PR，建议尽快合并以优化后续开发流程。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw 项目日报 - 2026-03-20

## 1. 今日速览
EasyClaw (RivonClaw) 项目今日呈现出**高活跃度与快速迭代**状态。过去24小时内成功合并了3个重要的功能性 PR，并连续发布了 v1.7.2 和 v1.7.3 两个版本，标志着项目 UI 层面重构的完成及体验细节的优化。同时，社区关于“多浏览器功能”定义的讨论引发了新 Issues 的提出，显示出用户对核心功能逻辑的关注度正在上升。整体来看，项目正从“功能铺设”向“体验打磨”阶段平稳过渡。

## 2. 版本发布
今日连续发布了两个版本，主要聚焦于 UI 系统性重构与平台适配问题。

*   **[v1.7.3: RivonClaw v1.7.3](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.7.3)**
    *   **发布说明**：本版本主要解决了 macOS 平台的安装与启动问题。针对 macOS Gatekeeper 拦截未签名应用导致的“'RivonClaw' is damaged and can't be opened”报错，提供了官方解决方案。
    *   **注意事项**：macOS 用户需通过终端命令绕过安全限制才能运行，建议开发团队后续考虑代码签名以提升开箱即用体验。

*   **[v1.7.2: RivonClaw v1.7.2](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.7.2)**
    *   **重大更新**：进行了全面的 UI 重构，包括组件化改造、主题分离及技能页面的重新设计。
    *   **新功能**：增加了基于验证码的认证机制和集中的默认设置；引入了基于 SQLite 的账号配置及“频道组允许来源”编辑器。
    *   **底层变更**：插件 SDK 重构，并进行了国际化的品牌调整。

## 3. 项目进展
今日合并的 3 个 PR 全部由贡献者 **chinayin** 提交，共同构成了 v1.7.2 版本的 UI 体系升级，极大完善了用户认证与账户管理体验。

*   **[#20 UI Migration: Component Refactor](https://github.com/gaoyangz77/easyclaw/pull/20) [CLOSED]**
    *   **进展**：完成了 UI 底层架构的迁移。将 SVG 图标整合至 `icons.tsx`，提取了侧边栏底部组件 `<BottomActions>`，并重构了技能页面。这为后续的 UI 一致性打下基础。
*   **[#23 Redesign auth modal & account page](https://github.com/gaoyangz77/easyclaw/pull/23) [CLOSED]**
    *   **进展**：重塑了登录/注册模态框及账户页面。新增了 Pill 形状的切换器、密码显隐开关、密码强度指示条以及隐私/条款链接，并实现了对未知邮箱的自动注册逻辑。
*   **[#24 Account UI redesign popover](https://github.com/gaoyangz77/easyclaw/pull/24) [CLOSED]**
    *   **进展**：优化了账户交互逻辑。将 `/account` 导航改为点击头像弹出的下拉菜单，区分了登录与未登录状态的展示视图（如会员计划卡片、欢迎语等），并新增了 `UserPopover` 组件。

## 4. 社区热点
*   **[#22 提问：“多浏览器”功能是指多用户还是多平台一致呢？](https://github.com/gaoyangz77/easyclaw/issues/22)**
    *   **热度**：今日最新开启的 Issue，配有大尺寸截图，显示出用户对功能定义的困惑。
    *   **分析**：用户在实测了 UI 后，对“多浏览器”这一核心概念的具体含义（是支持多用户配置，还是跨平台数据同步）提出了疑问，并询问登录状态的差异性影响。这表明项目的核心价值主张可能需要更清晰的文档说明。

## 5. Bug 与稳定性
*   **[macOS 应用无法打开](https://github.com/gaoyangz77/easyclaw/releases/tag/v1.7.3)**（非 Issue，但在 Release 中修复）
    *   **等级**：中（影响 macOS 新用户）
    *   **状态**：已在 v1.7.3 Release Notes 中提供手动修复指引。
    *   **描述**：由于未签名，macOS Gatekeeper 默认拦截应用。目前尚无自动修复的代码 PR，需用户手动执行终端命令。

## 6. 功能请求与路线图信号
*   **功能澄清请求**：Issue #22 虽然是提问，但实际上是对产品 Roadmap 的“方向性质询”。用户希望通过“多浏览器”功能实现特定的管理目标。如果该功能目前仅处于 UI 阶段，可能需要后续 PR 补充具体逻辑实现。

## 7. 用户反馈摘要
*   **正面反馈**：来自已关闭 Issue #12 的用户 **Geekbruce** 称赞 EasyClaw 的“项目架构非常符合我预期的架构”，并主动寻求建立技术交流群。这表明技术受众对项目底层设计（特别是 v1.7.2 提到的组件重构和插件 SDK）持高度认可态度。

## 8. 待处理积压
*   **[#22 功能定义澄清](https://github.com/gaoyangz77/easyclaw/issues/22)**：当前仅有提问无回复。建议维护者尽快回应，明确产品定位，以免产生用户误解。
*   **社群建设**：虽然 Issue #12 已关闭，但用户提出的“建立交流群”需求尚未落地（关闭可能仅表示问题已读），建议项目方考虑建立 Discord 或微信群以满足技术交流需求。

</details>

---
*本日报由 [agents-radar](https://github.com/yinwm/agents-radar) 自动生成。*