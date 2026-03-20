# AI CLI 工具社区动态日报 2026-03-20

> 生成时间: 2026-03-20 01:18 UTC | 覆盖工具: 7 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI 开发工具生态横向对比分析报告
**报告日期**：2026-03-20
**分析师**：AI 开发工具生态观察

---

## 1. 生态全景

当前 AI CLI 工具生态正处于**从“单一模型调用”向“智能体工作流平台”转型的深水区**。各大厂商均在积极构建 **MCP (Model Context Protocol)** 和 **Plugin/Skill 生态**，试图解决模型“最后一公里”的落地问题。然而，**稳定性与安全性**成为今日最大的痛点，多个头部工具出现了严重的 Regression（功能回退）和数据安全隐患，这标志着行业正进入“精细化打磨”与“架构重构”并重的关键阶段。

---

## 2. 各工具活跃度对比 (2026-03-20)

| 工具名称 | 今日 Release | 活跃 Issues (Top 10) | 活跃 PRs (Top 10) | 关键动态关键词 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **v2.1.80** (主要) | 🔥🔥🔥 极高 (含严重级 Bug) | 🔥 高 | **MCP 故障**, Git 数据丢失, v2.1.79 回归 |
| **OpenAI Codex** | Rust v0.116.0 | 🔥🔥🔥 极高 (计费危机) | 🔥 高 (架构重构) | **Token 泄露**, V8 引擎迁移, 远程开发 |
| **Kimi Code** | 无 (Patch 繁忙) | 🔥🔥 中 (集成适配) | 🔥🔥 高 (修复密集) | **插件系统**, Windows 兼容, VSCode 终端 |
| **Qwen Code** | v0.13.0-preview | 🔥🔥 中 (编辑失效) | 🔥 中 | **Edit 失败**, Skills 规范, 权限系统 |
| **OpenCode** | 无 (重构中) | 🔥🔥 中 (认证故障) | 🔥 极高 | **Effect 架构**, 去 Bun 化, OAuth 故障 |
| **GitHub Copilot** | **v1.0.9** (补丁) | 🔥🔥 高 (UX 退步) | 无 | **终端冲突**, TUI 接管, SSH 兼容 |
| **Gemini CLI** | v0.35.0-preview.2 | 🔥 低 (死循环) | 🔥 低 | **Agent Loop**, Git Worktree, AST 感知 |

---

## 3. 共同关注的功能方向

尽管各工具定位不同，但社区需求显示出明显的趋同性：

*   **插件/技能 生态化**
    *   **关注工具**：Kimi Code (PR #1503 新增插件系统), Claude Code (v2.1.80 插件市场), Qwen Code (支持 `.agents/skills`), OpenCode (Effect 化 Skill 系统)。
    *   **诉求**：用户不再满足于 CLI 内置功能，强烈需求通过插件机制扩展 AI 能力（如自定义 Agent、集成企业内部 API），且希望配置标准化（如 `skills.md` 规范）。

*   **IDE 深度集成与终端体验**
    *   **关注工具**：Kimi Code (VSCode 终端回车键修复), GitHub Copilot (TMUX/SSH 适配问题), OpenAI Codex (远程开发需求)。
    *   **诉求**：CLI 必须在 IDE 终端（特别是 VSCode）中表现完美，且不能破坏 TMUX、SSH 等原生终端体验。用户反感 CLI 过度接管系统快捷键和滚动条。

*   **MCP (Model Context Protocol) 支持**
    *   **关注工具**：Claude Code (Headless 模式 MCP 加载失败), OpenAI Codex (MCP 连接池重构), GitHub Copilot (OAuth MCP 需求)。
    *   **诉求**：MCP 已成为连接 AI 与外部工具（如 Gmail, Figma）的事实标准，用户要求其在无头模式和自动化脚本中稳定运行。

---

## 4. 差异化定位分析

*   **Claude Code & OpenAI Codex (官方旗舰)**
    *   **侧重**：深度绑定自家大模型能力，提供最新的 Context Window (1M) 和联网能力。
    *   **现状**：面临“成长的烦恼”。Claude Code 陷入 MCP 集成回归和 Git 安全性危机；OpenAI Codex 则深陷计费漏洞泥潭。两者均在重构底层架构。

*   **OpenCode & Qwen Code (开源生态挑战者)**
    *   **侧重**：**OpenCode** 追求极致的架构现代化 和 Provider 灵活性（去 Bun 化）；**Qwen Code** 侧重于细粒度的文件操作和成本控制。
    *   **现状**：OpenCode 正经历痛苦的底层重构，导致部分边缘功能不稳定；Qwen Code 在文件编辑稳定性上遭遇挑战，但其 Skills 生态跟进迅速。

*   **GitHub Copilot CLI (IDE 附庸)**
    *   **侧重**：作为 VS Code Copilot 的延伸，强调自然语言生成 Shell 命令。
    *   **现状**：试图强化 TUI 体验，但用力过猛导致与终端原生功能（如复制粘贴、滚动）冲突，引发老用户不满。

*   **Kimi Code (后起之秀)**
    *   **侧重**：长文本处理与特定工作流优化（如 Web UI）。
    *   **现状**：社区活跃度高，开发者响应快，正在快速补齐插件系统和 Windows 兼容性短板。

---

## 5. 社区热度与成熟度

*   **成熟度高，问题集中**：
    *   **Claude Code / OpenAI Codex**：拥有庞大的用户基数，Issue 讨论往往集中在特定的核心功能（如计费、安全）上，且容易引发千人规模的讨论，显示出其作为生产工具的高渗透率。

*   **快速迭代，架构动荡**：
    *   **OpenCode**：虽然 Issue 数量中等，但 PR 数量极高且涉及底层架构重写，说明项目处于剧烈的“成长期”，技术风险较大，但潜力高。

*   **体验攻坚期**：
    *   **GitHub Copilot / Kimi Code**：热点问题多集中在 UX 细节（如快捷键、显示）和平台兼容性，说明核心功能已定型，正处于打磨体验的阶段。

---

## 6. 值得关注的趋势信号

1.  **Agent 安全性迫在眉睫**：
    *   **信号**：Claude Code (`git reset --hard` 自动执行), Qwen Code (Agent 覆盖文件), OpenAI Codex (Junction 删除系统目录)。
    *   **参考**：开发者对 AI 拥有文件读写权限的容忍度已降至冰点。未来的工具必须引入**沙盒**、**细粒度权限控制** (如 Qwen Code 的规则系统) 和**危险操作确认机制**。

2.  **架构重构以适应复杂生态**：
    *   **信号**：OpenAI Codex 迁移至 V8，OpenCode 全面拥抱 Effect。
    *   **参考**：简单的脚本式 AI CLI 已无法承载 MCP、插件和长上下文的需求，架构升级是下一阶段的必经之路。

3.  **“类 Unix”哲学的回归**：
    *   **信号**：GitHub Copilot 因接管终端滚动和快捷键遭到强烈抵制。
    *   **参考**：开发者希望 AI CLI 是“好用的命令行工具”，而不是“阻断性的图形界面”。工具设计应遵循“组合优于覆盖”的原则。

4.  **跨模型兼容性焦虑**：
    *   **信号**：OpenCode 的自定义 Provider 问题，OpenAI Codex 的计费漏洞。
    *   **参考**：单一模型依赖（如仅用 GPT-5 或 Claude）带来的成本和锁定风险过高，企业和个人开发者都在寻求能够**无缝切换模型** 或使用**本地/开源模型**的解决方案。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

根据您提供的 GitHub 数据（截止 2026-03-20），以下是 Claude Code Skills 社区的热点分析报告。

### 1. 热门 Skills 排行

以下 PR 在社区中引发了广泛的关注与讨论，主要集中在**文档生成质量**、**开发体验优化**及**AI 代理的高级能力**上：

*   **#514 [document-typography](https://github.com/anthropics/skills/pull/514)**
    *   **功能**：文档排版质量控制。解决 AI 生成文档中的常见排版问题，如“孤行”控制、章节孤立及编号对齐。
    *   **热点**：这是当前排名第一的热门 PR。社区强烈关注 Claude 生成文档的专业性和可读性，该 Skill 直击“AI 生成内容往往排版混乱”的痛点。
    *   **状态**：OPEN

*   **#210 [frontend-design 改进](https://github.com/anthropics/skills/pull/210)**
    *   **功能**：提升前端设计 Skill 的清晰度和可执行性。
    *   **热点**：旨在确保 Claude 能在单次对话中准确遵循指令，强调了指令的“可行动性”，是对现有 Skill 的重要迭代。
    *   **状态**：OPEN

*   **#83 [skill-quality-analyzer](https://github.com/anthropics/skills/pull/83)**
    *   **功能**：提供一套 Skill 质量分析和安全审查的元工具。
    *   **热点**：展示了社区对“生态自检”的需求。随着 Skill 数量激增，如何评估和保证单个 Skill 的质量成为核心议题。
    *   **状态**：OPEN

*   **#509 [CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509)**
    *   **功能**：添加社区贡献指南。
    *   **热点**：回应了社区关于仓库健康度仅为 25% 的批评。社区渴望明确的贡献规范，以降低参与门槛。
    *   **状态**：OPEN

*   **#444 [AURELION skill suite](https://github.com/anthropics/skills/pull/444)**
    *   **功能**：引入 AURELION 认知与记忆框架，包含 Kernel、Advisor、Agent 和 Memory 四个组件。
    *   **热点**：代表了对“结构化思维”和“持久化知识管理”的高级探索，试图为 AI Agent 提供更复杂的认知架构。
    *   **状态**：OPEN

*   **#629 [session-memory](https://github.com/anthropics/skills/pull/629)**
    *   **功能**：在上下文压缩和会话重启后，保留关键技术事实。
    *   **热点**：解决了长期对话中上下文丢失的痛点，对于长周期开发任务至关重要。
    *   **状态**：OPEN

*   **#154 [shodh-memory](https://github.com/anthropics/skills/pull/154)**
    *   **功能**：为 AI 代理提供持久化跨会话记忆系统。
    *   **热点**：与 #629 类似，强调了“记忆”是当前 Agent 能力进化的关键方向。
    *   **状态**：OPEN

### 2. 社区需求趋势

从 Issues 的讨论中，可以提炼出以下核心需求方向：

*   **生态安全与标准化**：Issue **#492** 指出社区 Skill 冒用官方命名空间的安全隐患，Issue **#202** 批评 `skill-creator` 过于冗长且不符合最佳实践。社区迫切需要**更严格的命名规范、安全审查机制及高效的开发标准**。
*   **企业级集成与稳定性**：大量 Issues（如 #406, #403, #389, #61）报告了 API 500 错误、SSO 登录问题及与 AWS Bedrock 的集成困难。这表明社区正在尝试将 Skills **深度集成到企业工作流中**，对稳定性和兼容性要求极高。
*   **质量保证与自动化测试**：Issue **#556** 揭示了评估脚本触发率为 0% 的问题，反映了社区对**自动化验证和测试工具**的渴望，以确保 Skill 能够按预期工作。
*   **跨平台互操作性**：Issue **#16** 提出将 Skills 暴露为 MCPs（Model Context Protocol），显示了社区希望打破平台壁垒，实现技能在不同系统间的复用。

### 3. 高潜力待合并 Skills

这些 PR 虽尚未合并，但讨论度高或功能关键，极有可能在近期落地：

*   **#362 [Fix UTF-8 panic](https://github.com/anthropics/skills/pull/362)**：修复了多字节字符处理导致的 Rust 崩溃。对于国际化社区（尤其是非英语用户）这是必须的基础设施修复。
*   **#374 [x402 BSV auth + micropayment](https://github.com/anthropics/skills/pull/374)**：引入基于 BSV 的微支付认证系统。如果落地，将开启“AI 服务付费”的全新商业模式。
*   **#486 [ODT skill](https://github.com/anthropics/skills/pull/486)**：支持 OpenDocument 文本格式。鉴于 LibreOffice 等软件的用户基础，这是对办公自动化场景的重要补充。

### 4. Skills 生态洞察

> **当前社区在 Skills 层面最集中的诉求是：从“尝鲜”转向“生产级落地”，迫切需要提升生成内容的排版质量、解决企业集成的稳定性问题，并建立标准化的记忆与安全机制。**

---

# Claude Code 社区动态日报 (2026-03-20)

> **本期摘要**：v2.1.80 发布，重点增强了状态栏 API 和插件市场管理；社区爆发针对 v2.1.79 的严重 Regression 问题，涉及 MCP 集成和模式权限，建议生产环境用户暂缓升级。

---

## 📌 今日速览
今日 **v2.1.80** 版本发布，主要新增了速率限制 API 和基于 `settings.json` 的插件定义能力。与此同时，社区反馈显示昨日的 **v2.1.79** 版本存在严重的 **Regression 问题**，导致 MCP 服务器在无头模式下无法加载以及 Context Window 显示异常，引发热议。此外，关于使用限制和 Git 数据安全的 Bug 依然高热不下。

---

## 🚀 版本发布：v2.1.80
- **状态栏增强**：新增 `rate_limits` 字段，支持脚本化展示 Claude.ai 的 5小时/7天使用配额（包含 `used_percentage` 和 `resets_at`）。
- **插件管理**：新增 `source: 'settings'` 插件市场来源，现在可以直接在 `settings.json` 中内联声明插件条目。
- **CLI 工具**：新增部分 CLI 工具支持（原文截断，待后续更新确认）。

---

## 🔥 社区热点 Issues (Top 10)

### 🚨 严重关注

1. **[#16157] [BUG] Max 订阅用户瞬间触碰使用限制**
   - **重要性**：⭐⭐⭐⭐⭐
   - **动态**：1251 条评论，持续发酵。多位 Max 订阅用户反馈在使用过程中莫名其妙触发速率限制，严重影响高阶付费体验。
   - **链接**：[anthropics/claude-code#16157](https://github.com/anthropics/claude-code/issues/16157)

2. **[#36309] [BUG] v2.1.79 导致 HTTP OAuth MCP 服务器在 Headless 模式无法加载**
   - **重要性**：⭐⭐⭐⭐⭐
   - **动态**：严重的 Regression 问题。更新至 v2.1.79 后，`-p` 模式下无法加载 MCP 集成，影响自动化工作流。
   - **链接**：[anthropics/claude-code#36309](https://github.com/anthropics/claude-code/issues/36309)

3. **[#34143] [BUG] Opus 4.6 在 Max 计划下仍显示 200K Context 而非 1M**
   - **重要性**：⭐⭐⭐⭐
   - **动态**：尽管 v2.1.75 声称默认开启 1M Context，但用户反馈 `/context` 仍显示 200k。可能是配置覆盖或前端显示 Bug。
   - **链接**：[anthropics/claude-code#34143](https://github.com/anthropics/claude-code/issues/34143)

4. **[#34327] [BUG] Claude Code 启动时自动执行 `git reset --hard` 导致代码丢失**
   - **重要性**：⭐⭐⭐⭐⭐
   - **动态**：数据灾难级风险。工具在会话启动首秒内自动运行硬重置，两次导致未提交工作丢失。需立即修复。
   - **链接**：[anthropics/claude-code#34327](https://github.com/anthropics/claude-code/issues/34327)

5. **[#36339] [BUG] Windows 下 `rm -rf` 命令通过 NTFS junction 删除了整个 C:\Users**
   - **重要性**：⭐⭐⭐⭐⭐
   - **动态**：老 Issue 持续受关注。在 Windows 上使用 pnpm 时，由于 junction 链接处理问题，删除操作穿透至系统目录。
   - **链接**：[anthropics/claude-code#36339](https://github.com/anthropics/claude-code/issues/36339)

### 🔧 功能与体验

6. **[#20469] [Feature Request] 为 Max 个人用户开放 Microsoft 365 连接器**
   - **重要性**：⭐⭐⭐⭐
   - **动态**：用户质疑为何支付最高费用的 Max 计划无法使用仅限 Team/Enterprise 的 M365 连接器。
   - **链接**：[anthropics/claude-code#20469](https://github.com/anthropics/claude-code/issues/20469)

7. **[#24964] [BUG] Cowork 文件夹选择器拒绝主目录外的文件夹及 Symlinks**
   - **重要性**：⭐⭐⭐
   - **动态**：协同开发体验受限，限制了复杂项目结构的灵活性。
   - **链接**：[anthropics/claude-code#24964](https://github.com/anthropics/claude-code/issues/24964)

8. **[#28951] [BUG] VS Code 扩展不支持远程控制**
   - **重要性**：⭐⭐⭐
   - **动态**：IDE 集成体验割裂，CLI 支持的功能在 VS Code 插件中不可用。
   - **链接**：[anthropics/claude-code#28951](https://github.com/anthropics/claude-code/issues/28951)

9. **[#36168] [BUG] VS Code 更新后 "Bypass/Skip permissions" 功能失效**
   - **重要性**：⭐⭐⭐
   - **动态**：效率杀手，更新后无法再跳过权限确认，工作流被打断。
   - **链接**：[anthropics/claude-code#36168](https://github.com/anthropics/claude-code/issues/36168)

10. **[#36060] [BUG] claude.ai MCP 集成在 -p 模式下不可用**
    - **重要性**：⭐⭐⭐⭐
    - **动态**：与 #36309 类似，Gmail/Calendar 等官方集成在 Headless 模式下失效。
    - **链接**：[anthropics/claude-code#36060](https://github.com/anthropics/claude-code/issues/36060)

---

## 🛠️ 重要 PR 进展 (Top 10)

1. **[#36333] 修复 hookify 脚本中的 Python 导入错误**
   - **内容**：修复了 `hookify` 核心配置加载器的模块导入路径问题，解决了所有 Hook 事件触发的 `No module named 'hookify'` 错误。
   - **链接**：[anthropics/claude-code#36333](https://github.com/anthropics/claude-code/pull/36333)

2. **[#36300] 修复 ralph-wiggum Stop Hook 的 JSON Schema 匹配**
   - **内容**：Stop Hook 响应从 `{decision: block}` 修正为符合 Schema 的 `{ok: boolean}`，防止 Claude Code 拒绝 Hook 响应。
   - **链接**：[anthropics/claude-code#36300](https://github.com/anthropics/claude-code/pull/36300)

3. **[#36279] 为 Hook 输入添加 Agent 上下文字段**
   - **内容**：新增 4 个 Agent 上下文字段，允许 Hook 区分主 Agent 和子 Agent，实现更精准的安全策略。
   - **链接**：[anthropics/claude-code#36279](https://github.com/anthropics/claude-code/pull/36279)

4. **[#36260] 为 devcontainer 初始化脚本添加 IPv6 防火墙规则**
   - **内容**：补充了缺失的 IPv6 防火墙策略，不仅限制 IPv4，现在也对 IPv6 进行了白名单管理。
   - **链接**：[anthropics/claude-code#36260](https://github.com/anthropics/claude-code/pull/36260)

5. **[#36253] 新增 Hook 示例**
   - **内容**：提供了文件守卫、会话预加载和通知功能的 Hook 示例代码，方便开发者上手。
   - **链接**：[anthropics/claude-code#36253](https://github.com/anthropics/claude-code/pull/36253)

6. **[#35683] 新增 scroll-fix 插件修复终端滚动回归问题**
   - **内容**：引入插件修复所有平台下的终端滚动回顶 Bug，支持 Ctrl+6 冻结切换。
   - **链接**：[anthropics/claude-code#35683](https://github.com/anthropics/claude-code/pull/35683)

7. **[#36252] 补充 security-guidance 插件的 README**
   - **内容**：完善了安全插件文档，涵盖了 9 种安全模式及配置方法。
   - **链接**：[anthropics/claude-code#36252](https://github.com/anthropics/claude-code/pull/36252)

8. **[#23971] 修正文档中 agents 字段类型定义**
   - **内容**：文档修正 agents 字段应为 "String Array" 而非 "String"，修复了安装失败的隐患。
   - **链接**：[anthropics/claude-code#23971](https://github.com/anthropics/claude-code/pull/23971)

9. **[#31529] 新增 `/remote-control-diagnose` 诊断命令**
   - **内容**：新增命令帮助用户调试 RC 环境不可用的广泛错误。
   - **链接**：[anthropics/claude-code#31529](https://github.com/anthropics/claude-code/pull/31529)

10. **[#36145] 更新 npm 安装方式的弃用通知**
    - **内容**：进一步更新关于 npm 安装方式的弃用说明。
    - **链接**：[anthropics/claude-code#36145](https://github.com/anthropics/claude-code/pull/36145)

---

## 📊 功能需求趋势

根据过去 24 小时的 Issues 讨论，社区关注点主要集中在以下方向：

1. **安全与权限控制**
   - **趋势**：用户极度关注 Git 操作的安全性和数据丢失风险（#34327, #36339）。
   - **需求**：希望能有更明确的“危险操作”确认机制，以及对 Symlink/Junction 的安全处理。

2. **MCP (Model Context Protocol) 集成稳定性**
   - **趋势**：MCP 是当前的核心生产力工具，但最近的几个版本（v2.1.79, v2.1.80）出现了严重的兼容性回退（#36309, #36060）。
   - **需求**：用户迫切要求修复 Headless 模式下的 OAuth 加载问题。

3. **VS Code 扩展功能对齐**
   - **趋势**：VS Code 用户感到功能被“阉割”，如缺少远程控制 (#28951) 和权限跳过失效 (#36168)。
   - **需求**：实现 CLI 与 IDE 扩展的功能平权。

4. **Plan 权限与公平性**
   - **趋势**：Max 用户抱怨虽然支付了最高费用，但无法获得 Team/Enterprise 的某些功能（如 M365 连接器）。
   - **需求**：调整权限策略，给予个人高阶用户完整的工具访问权限。

---

## 👨‍💻 开发者关注点

- **生产环境慎用 v2.1.79**：多个 Issue 报告该版本导致 Headless MCP 服务器加载失败，且可能存在 Context Window 显示错误，建议暂时回退或等待 v2.1.80 验证。
- **Plugin 开发者注意**：Hookify 的导入路径已发生变化（PR #36333），Plugin Manifest 中的 `agents` 字段类型必须为数组（PR #23971）。
- **Windows 用户风险**：关于 `rm -rf` 穿透 Junction 删除系统文件的问题依然存在，在使用清理类指令时需格外小心。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 (2026-03-20)

## 📌 今日速览
Codex 社区目前面临严重的**稳定性与信任危机**。过去 24 小时内，关于 **Token 消耗过快（Rate Limits/Billing）** 的投诉激增，多个高赞 Issues 指控最新版本存在严重计费漏洞，导致配额非正常瞬间耗尽。与此同时，开发团队正忙于推进 V8 引擎集成和代码架构重构，试图解决 Windows 原生支持和远程开发等长期痛点。

---

## 🚀 版本发布
**Rust v0.116.0 (稳定版)**
*   **主要更新**：
    *   **App-server TUI 增强**：初始设置期间现已支持设备码登录 ChatGPT，并支持刷新现有的 ChatGPT Token。
    *   **插件体验优化**：Codex 现可提示安装缺失的插件或连接器，支持配置建议允许名单，并同步安装/卸载状态。
*   **预览版发布**：`rust-v0.117.0-alpha.2` 及多个 v0.116.0 alpha 版本也已发布，主要包含内部依赖项更新。

---

## 🔥 社区热点 Issues (Top 10)

1.  **[#14593] VS Code 扩展更新后 Token 消耗异常快** 🔥🔥🔥
    *   **重要性**：⚠️ **极高**。涉及用户直接经济利益。
    *   **详情**：大量 Business 订阅用户反馈更新到 v26.311.21342 后，Token 配额瞬间耗尽。
    *   **社区反应**：137 评论，64 👍。用户情绪激动，怀疑存在计费 Bug。
    *   [链接](https://github.com/openai/codex/issues/14593)

2.  **[#14762] 付费额度非正常极速下降** 🔥🔥🔥
    *   **重要性**：⚠️ **极高**。证实了计费异常并非个例。
    *   **详情**：用户报告刚充值的 $40 额度在极短时间内（甚至过夜仅运行两个 prompt）就消耗了 80%。
    *   **社区反应**：15 评论，20 👍。用户称“令人恐惧”，不敢使用 CLI。
    *   [链接](https://github.com/openai/codex/issues/14762)

3.  **[#10450] [Feature Request] Codex 桌面端支持远程开发** 🔥🔥
    *   **重要性**：⭐⭐⭐ 核心功能需求。
    *   **详情**：目前 Codex Desktop App 缺乏 VS Code 的 Remote SSH/Container 开发支持，限制了其在专业工作流中的替代能力。
    *   **社区反应**：396 👍。这是社区历史最高赞的需求之一。
    *   [链接](https://github.com/openai/codex/issues/10450)

4.  **[#15105] API 错误率激增，所有 CLI 调用失败** 🔥🔥
    *   **重要性**：🚨 **服务中断**。
    *   **详情**：过去 2 小时内，远程压缩任务导致高 API 错误率，所有 Codex CLI 请求均报错“high demand”。
    *   **社区反应**：用户无法进行任何开发工作。
    *   [链接](https://github.com/openai/codex/issues/15105)

5.  **[#13864] GPT-5.4 响应错误消息（忽略最新输入）**
    *   **重要性**：🐛 模型行为/逻辑错误。
    *   **详情**：模型倾向于回答早期的消息而不是最后一条用户指令。
    *   **社区反应**：严重影响对话连贯性，Pro 用户受困扰。
    *   [链接](https://github.com/openai/codex/issues/13864)

6.  **[#14675] Windows 桌面端 `apply_patch` 失败**
    *   **重要性**：🐛 平台特定 Bug。
    *   **详情**：在 Windows 上对 `src/**` 嵌套文件应用补丁时，沙盒刷新报错退出。
    *   **社区反应**：阻碍了 Windows 用户进行代码重构。
    *   [链接](https://github.com/openai/codex/issues/14675)

7.  **[#14461] Windows 上启用 WSL 模式导致无法启动**
    *   **重要性**：🐛 启动阻断 Bug。
    *   **详情**：配置 `terminalShell=wsl` 后，Codex App 无法启动。
    *   **社区反应**：Windows + WSL 开发环境的常见痛点。
    *   [链接](https://github.com/openai/codex/issues/14461)

8.  **[#12888] Agent 编辑导致 "command failed; retry without sandbox?"**
    *   **重要性**：🐛 沙盒机制问题。
    *   **详情**：Agent 编辑操作在沙盒内莫名失败，且缺乏有用的错误日志。
    *   **社区反应**：频繁打断心流，用户被迫手动干预。
    *   [链接](https://github.com/openai/codex/issues/12888)

9.  **[#8259] [Feature Request] Markdown 表格格式化**
    *   **重要性**：⭐ 体验优化。
    *   **详情**：生成的 Markdown 表格空格错乱，不可读。
    *   **社区反应**：32 👍。这是长期存在的输出质量问题。
    *   [链接](https://github.com/openai/codex/issues/8259)

10. **[#14399] [Feature Request] 细粒度权限控制**
    *   **重要性**：⭐ 安全与便利的平衡。
    *   **详情**：目前的“默认权限”太严（每步都要点），“完全访问”太松。用户希望有中间选项。
    *   **社区反应**：反映了高级用户对自动化流程控制的需求。
    *   [链接](https://github.com/openai/codex/issues/14399)

---

## 🛠️ 重要 PR 进展 (Top 10)

1.  **[#15247] Code Mode 迁移至 V8** (cconger)
    *   **内容**：将 Code Mode 移至独立 crate，切断对旧 codex 的依赖，准备集成 V8 引擎。
    *   **影响**：这是 Codex 执行底层架构的重大升级，旨在提升性能和跨平台兼容性。
    *   [链接](https://github.com/openai/codex/pull/15247)

2.  **[#15258/15257/15256] MCP 连接池化与重构** (jgershen-oai)
    *   **内容**：一系列 PR 旨在重构 MCP (Model Context Protocol) 连接，将其拆分为后端和轻量级客户端，并在 ThreadManager 中实现连接池化。
    *   **影响**：将大幅降低 MCP 工具调用的开销，提升多线程和 App-server 中的工具响应速度。
    *   [链接](https://github.com/openai/codex/pull/15258)

3.  **[#15236] 修复压缩任务的中断处理** (charley-oai)
    *   **内容**：使 `CompactTask` 尊重取消信号，允许用户按 `Esc` 键中断漫长的上下文压缩过程。
    *   **影响**：解决用户反馈的 UI 卡死问题，提升交互体验。
    *   [链接](https://github.com/openai/codex/pull/15236)

4.  **[#14525] 增加内置工具的细粒度开关** (ashwinnathan-openai)
    *   **内容**：新增 `config.tools` 配置层，允许用户分组控制内置工具的可用性。
    *   **影响**：回应了社区对“细粒度权限”的需求，让 Agent 行为更可控。
    *   [链接](https://github.com/openai/codex/pull/14525)

5.  **[#15226/15144] Guardian 审批会话预热与优化** (charley-oai)
    *   **内容**：在第一次审批请求前预热 Guardian trunk 会话，构建可复用的缓存前缀。
    *   **影响**：加速 Agent 执行危险操作前的审批流程，减少等待延迟。
    *   [链接](https://github.com/openai/codex/pull/15226)

6.  **[#15215] 初始版插件 TUI 菜单** (canvrno-oai)
    *   **内容**：在 TUI 和 App-server 中添加 `/plugins` 菜单，支持列表浏览和读取状态。
    *   **影响**：为在终端内管理插件铺平道路，增强 CLI 的易用性。
    *   [链接](https://github.com/openai/codex/pull/15215)

7.  **[#14869] 添加远程环境 CI 矩阵** (pakrym-oai)
    *   **内容**：通过 `CODEX_TEST_REMOTE_ENV` 标志，让集成测试能在 Docker 容器内的“远程”环境中运行。
    *   **影响**：提升 Codex 在远程容器和 SSH 场景下的稳定性。
    *   [链接](https://github.com/openai/codex/pull/14869)

8.  **[#15114] 修复受限文件系统配置** (celia-oai)
    *   **内容**：允许受限权限配置文件读取运行时辅助的可执行文件（如 zsh helper）。
    *   **影响**：修复了在严格安全模式下 Shell 工具可能无法运行的问题。
    *   [链接](https://github.com/openai/codex/pull/15114)

9.  **[#15253] 拆分 Features 为独立 Crate** (aibrahim-oai)
    *   **内容**：将功能系统拆分为 `codex-features` crate。
    *   **影响**：模块化架构改进，便于未来维护和扩展新功能。
    *   [链接](https://github.com/openai/codex/pull/15253)

10. **[#15237] 使用 SIWC 客户端密钥进行实时认证** (aibrahim-oai)
    *   **内容**：支持从 ChatGPT 认证中获取实时客户端密钥。
    *   **影响**：改进实时语音/会话功能的认证流程。
    *   [链接](https://github.com/openai/codex/pull/15237)

---

## 📈 功能需求趋势
根据过去 24 小时的 Issues 和 PR 分析：
1.  **稳定性重于新功能**：由于计费和 API 错误问题，社区关注度从“想要什么新功能”转移到了“系统可用性”。
2.  **Windows 原生支持**：Windows 相关 Bug (WSL, Sandbox, Process) 占比依然很高，原生体验尚未达到 macOS/Linux 水平。
3.  **远程开发**：尽管已有相关 PR，但缺乏对 `remote-dev` 的官方支持仍是最大痛点之一。
4.  **MCP 生态集成**：大量 PR 投入在 MCP 优化上，表明 OpenAI 正在大力整合第三方工具生态。

---

## 👨‍💻 开发者关注点
1.  **计费透明度**：开发者对 Token 计数机制表示极度担忧，急需官方解释或回滚有问题的版本。
2.  **上下文管理**：上下文窗口满导致任务失败的问题依然高频，压缩机制的可靠性有待加强。
3.  **沙盒性能**：Sandbox 带来的延迟和权限配置复杂性是影响开发效率的主要瓶颈。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 (2026-03-20)

## 📰 今日速览
Gemini CLI 今天发布了一个补丁版本 `v0.35.0-preview.2`，主要修复了版本分支问题。社区讨论集中在 **Agent 行为异常（死循环）**、**终端 UI 启动时的重复警告**以及**Git Worktree 支持的开发进度**上。尽管项目正处于活跃开发阶段，但部分核心功能（如 `/plan` 命令、截图输入）仍存在较多用户痛点。

---

## 📦 版本发布
**v0.35.0-preview.2**
*   **类型**: Patch Release
*   **内容**: 这是一个紧急补丁，从 `release/v0.35.0-preview.1-pr-23074` 分支 cherry-pick 了提交 (4e5dfd0)，旨在修复 preview.1 版本中的特定问题并创建 preview.2。
*   **链接**: [Release v0.35.0-preview.2](https://github.com/google-gemini/gemini-cli/pull/23134)

---

## 🔥 社区热点 Issues

1.  **[#23182 Agent 陷入死循环并消耗大量 Token](https://github.com/google-gemini/gemini-cli/issues/23182)**
    *   **重要性**: ⚠️ 高
    *   **摘要**: 用户报告 Agent 在尝试读取文件时失败，随后陷入无限循环并持续消耗 Token，无法选择正确的工具。
    *   **反应**: 新提交的 Bug，目前尚无评论，但涉及核心稳定性，关注度极高。

2.  **[#23172 终端 UI 启动时出现重复的扩展警告](https://github.com/google-gemini/gemini-cli/issues/23172)**
    *   **重要性**: 🔧 中
    *   **摘要**: 启动 CLI 时，关于扩展配置缺失或 `conductor` 被替换的警告会显示两次。
    *   **反应**: 引起了 2 次评论，已有相应的 PR (#23181, #23178) 尝试修复此问题。

3.  **[#22933 Agent 会话死循环问题](https://github.com/google-gemini/gemini-cli/issues/22933)**
    *   **重要性**: ⚠️ 高
    *   **摘要**: 描述了 Agent 在处理 Session ID 和路径写入时的逻辑死循环，表现出明显的决策混乱。
    *   **反应**: 收到 1 个点赞，社区对 Agent 的稳定性表示担忧。

4.  **[#16803 [功能请求] 支持粘贴截图](https://github.com/google-gemini/gemini-cli/issues/16803)**
    *   **重要性**: 🚀 需求
    *   **摘要**: 用户强烈希望在 CLI 交互模式中直接粘贴截图，以便更直观地与 AI 沟通。
    *   **反应**: 该 Issue 在今天被关闭（可能是作为 "Won't fix" 或转移到了其他跟踪系统），但显示了用户对多媒体输入的渴望。

5.  **[#23013 Omission 占位符检测器不支持 `#` 和 `/*` 注释风格](https://github.com/google-gemini/gemini-cli/issues/23013)**
    *   **重要性**: 🐛 Bug
    *   **摘要**: 当前代码生成工具仅支持 `//` 注释的占位符检测，导致 Python/Ruby 等语言中未完成的代码（如 `# rest of code...`）被写入磁盘。
    *   **反应**: 这是一个明显的质量改进点，影响多语言开发体验。

6.  **[#22855 [功能请求] `/plan` 命令应接受 Prompt 参数](https://github.com/google-gemini/gemini-cli/issues/22855)**
    *   **重要性**: 🚀 需求
    *   **摘要**: 用户希望 `/plan` 能接受文本参数，以便在一个命令中启动计划，而不是先进入输入框再输入。
    *   **反应**: 获得了 2 个点赞，符合高效操作的工作流需求。

7.  **[#22745 评估 AST (抽象语法树) 感知的文件读取与搜索](https://github.com/google-gemini/gemini-cli/issues/22745)**
    *   **重要性**: 🔮 长期规划
    *   **摘要**: 这是一个 EPIC Issue，旨在调查是否引入 AST 感知工具来更精确地读取代码边界（如方法范围），减少 Token 噪音和读取轮次。
    *   **反应**: 讨论活跃，涉及提升 Agent 代码理解能力的底层架构。

8.  **[#22819 实现全局与项目的内存路由](https://github.com/google-gemini/gemini-cli/issues/22819)**
    *   **重要性**: 🧠 Agent 智能
    *   **摘要**: 探讨 Agent 如何将记忆保存到正确位置（全局用户偏好 vs 项目特定约定）。
    *   **反应**: 1 个点赞，是提升 Agent 个性化能力的关键。

9.  **[#22816 二级依赖应使用多重缩进显示](https://github.com/google-gemini/gemini-cli/issues/22816)**
    *   **重要性**: 🎨 UI/UX
    *   **摘要**: 建议在依赖树视图中使用多级树形结构，而不是当前的两级结构。
    *   **反应**: 附带了视觉截图建议。

10. **[#22809 调整主 Agent Prompt 以鼓励主动写入内存](https://github.com/google-gemini/gemini-cli/issues/22809)**
    *   **重要性**: 🧠 Agent 智能
    *   **摘要**: 建议 Agent 应在用户陈述偏好或反复纠正行为时，主动调用内存工具。
    *   **反应**: 涉及系统 Prompt 的优化。

---

## 🚀 重要 PR 进展

1.  **[#23181 fix(core): 跳过早期 loadCliConfig 调用中的扩展加载以防止重复警告](https://github.com/google-gemini/gemini-cli/pull/23181)**
    *   **状态**: Closed (Merged?)
    *   **内容**: 修复了 Issue #23172，通过优化启动流程中的 `loadCliConfig` 调用逻辑，解决了扩展警告重复显示的问题。

2.  **[#23178 fix(cli): 在终端 UI 中去重启动时的扩展警告](https://github.com/google-gemini/gemini-cli/pull/23178)**
    *   **状态**: Open
    *   **内容**: 另一个针对重复警告的修复方案，引入了模块级变量 `emittedWarnings` 来追踪已发出的警告。显示团队正在从不同角度解决此 UI 问题。

3.  **[#23177 fix(cli): 防止子命令遮蔽并跳过命令的认证](https://github.com/google-gemini/gemini-cli/pull/23177)**
    *   **状态**: Open
    *   **内容**: 修复了贪婪匹配默认命令导致的管理子命令（如 `mcp`, `extensions`）被误判为对话查询的问题，并优化了非必要认证流程。

4.  **[#23161 fix(core): 确保子代理工具更新立即应用配置覆盖](https://github.com/google-gemini/gemini-cli/pull/23161)**
    *   **状态**: Open
    *   **内容**: 修复了运行时更改代理配置（如切换模型、温度）不生效或代理未正确注销的 Bug。

5.  **[#22973 feat(worktree): 添加 Git Worktree 支持以实现隔离的并行会话](https://github.com/google-gemini/gemini-cli/pull/22973)**
    *   **状态**: Open
    *   **内容**: 引入了中央 Git Worktree 管理系统，允许在同一仓库的不同分支上并行运行多个 Gemini 会话，避免文件冲突。这是一个重大的工作流增强功能。

6.  **[#23179 fix: ACP: 分离对话文本与执行工具命令标题](https://github.com/google-gemini/gemini-cli/pull/23179)**
    *   **状态**: Open
    *   **内容**: 重构了 ACP 工具执行管道，确保 IDE 仅渲染干净的原始命令，而将 Agent 的上下文解释分离显示，改善了工具调用的可读性。

7.  **[#23180 fix: 保存时保留外部添加的设置](https://github.com/google-gemini/gemini-cli/pull/23180)**
    *   **状态**: Closed
    *   **内容**: 修复了 CLI 保存设置（如主题更改）时会覆盖掉用户手动在 `settings.json` 中添加的顶层键的问题。

8.  **[#22856 feat(cli): 添加 /context 命令以显示上下文窗口细分](https://github.com/google-gemini/gemini-cli/pull/22856)**
    *   **状态**: Open
    *   **内容**: 新增 `/context` 命令，可视化展示模型上下文窗口的占用情况（系统提示词、工具架构、内存文件等），对调试 Token 使用非常有帮助。

9.  **[#23159 feat(core): 引入 AgentSession 并重命名流事件](https://github.com/google-gemini/gemini-cli/pull/23159)**
    *   **状态**: Open
    *   **内容**: 对 `AgentProtocol` 接口进行更新，引入基于订阅的模型和 `AgentSession` 包装器，改进了 Agent 事件的消费方式（从 `stream_` 重命名为 `agent_`）。

10. **[#23045 feat(cli): 在 ACP 模式下有条件地排除 ask_user 工具](https://github.com/google-gemini/gemini-cli/pull/23045)**
    *   **状态**: Open
    *   **内容**: 防止 IDE 拦截 `ask_user` 工具调用并显示令人困惑的权限对话框，强制模型回退到纯文本对话查询，改善 ACP (Agent Control Protocol) 模式下的体验。

---

## 📈 功能需求趋势

1.  **Agent 稳定性与调试工具**: 社区高度关注 Agent 的 "Loop" 问题和对代码库的无效操作。用户需要更可靠的停止机制和更好的上下文理解（如 AST 支持）。
2.  **工作流增强**: Git Worktree 支持和 `/plan` 命令改进显示出用户希望 CLI 能更好地处理复杂的并行开发任务。
3.  **UI/UX 细节优化**: 启动警告的去重、依赖树的视觉层级改进、以及 `/context` 命令的添加，反映了用户对 CLI 反馈信息清晰度的严格要求。

---

## 👨‍💻 开发者关注点

*   **配置管理**: 开发者反馈 `loadCliConfig` 的多次调用导致了副作用（重复警告），且外部修改的配置文件容易被覆盖。
*   **多语言支持**: 占位符检测器对非 `//` 风格注释的缺失支持，影响了 Python/Go 开发者的代码补全体验。
*   **启动性能与冗余**: CLI 启动流程中存在冗余操作（如重复加载扩展），这增加了延迟并困扰用户。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 (2026-03-20)

## 📰 今日速览
GitHub Copilot CLI 于昨日发布了 **v1.0.9** 版本，重点修复了此前版本中争议较大的**终端交互兼容性问题**（包括复制粘贴和 SSH 断开时的错误提示）。然而，新版发布引发了社区关于**终端原生体验退化**的激烈讨论，特别是由于 CLI 占用了 TUI 滚动和右键菜单控制权，导致在 `tmux` 和 `putty` 等环境下的常规操作受阻，同时部分用户反馈了模型可用性和 API 稳定性的问题。

---

## 🚀 版本发布
**[v1.0.9] (2026-03-19)**
**主要更新：**
*   **跨平台兼容性修复：** 修复了在 WSL 环境下复制文本时 CJK 及其他非 ASCII 字符出现乱码的问题。
*   **SSH 稳定性提升：** 解决了在 SSH 断开或终端关闭时，时间线中虚假出现的 I/O 错误（ENOTCONN, EIO）。
*   **配置增强：** 新增 `include_gitignored` 配置选项，允许在 `@` 文件搜索中包含被 git 忽略的文件。
*   **发布链接：** [github.com/github/copilot-cli/releases](https://github.com/github/copilot-cli)

---

## 🔥 社区热点 Issues

以下是过去 24 小时内最值得关注的 Issues，主要集中在终端交互回归和用户体验上：

1.  **[#239 屏幕闪烁与滚动跳跃 (热词: TUI/UX)]**
    *   **状态：** OPEN | **👍 66**
    *   **内容：** 当对话历史增长时，屏幕出现剧烈闪烁和输出重复。发送新请求时屏幕会自动跳回顶部，破坏工作流。
    *   **原因：** 这是长期存在的体验问题，随着使用时长增加影响显著。

2.  **[#1284 方向键失效输出乱码 (热词: Regression)]**
    *   **状态：** OPEN | **更新：** 2026-03-19
    *   **内容：** 交互会话中方向键停止工作，直接输出字面字符（如 A、B、C、D），说明终端的转义序列未被正确解析。
    *   **原因：** 这是一个严重的功能性 Bug，直接影响了 CLI 的基本可用性。

3.  **[#1481 快捷键逻辑冲突 (热词: UX)]**
    *   **状态：** OPEN | **👍 9**
    *   **内容：** 社区强烈抗议 `SHIFT + ENTER` 被用于执行命令，这违背了大多数聊天工具（光标、Claude Code）中使用该组合键换行的通用习惯。
    *   **原因：** 用户肌肉记忆冲突，严重影响输入效率。

4.  **[#2148 TMUX 滚动与按键失效 (热词: Compatibility)]**
    *   **状态：** CLOSED | **更新：** 2026-03-19
    *   **内容：** 升级到 v1.0.8 后，CLI 内部接管了滚动，导致无法使用 `tmux` 的原生翻页、搜索和键盘选择功能。
    *   **原因：** 新版 TUI 实现与终端复用器/模拟器深层冲突，导致高级用户工作流受阻。

5.  **[#2159 Windows Putty/SSH 复制粘贴失效 (热词: Bug)]**
    *   **状态：** CLOSED | **更新：** 2026-03-19
    *   **内容：** 用户报告无法通过鼠标选择复制文本，也无法通过右键粘贴，导致通过 SSH 使用 CLI 的核心工作流断裂。
    *   **原因：** 涉及远程开发场景下的高频操作。

6.  **[#2082 Linux 下 Ctrl+Shift+C 复制失效 (热词: Regression)]**
    *   **状态：** OPEN | **更新：** 2026-03-19
    *   **内容：** Ubuntu 24.04 下标准的 `Ctrl+Shift+C` 快捷键不再工作，新版强制使用 Ctrl+C 或右键（但右键也有问题，见 #2158）。
    *   **原因：** 改变 Linux 用户习惯的标准快捷键引发的不满。

7.  **[#2158 Linux 右键菜单被拦截 (热词: UX Bug)]**
    *   **状态：** OPEN | **更新：** 2026-03-19
    *   **内容：** Copilot 捕获了右键事件，试图使用自定义复制粘贴，但复制失败并报错 `spawn xclip ENOENT`，导致无法使用系统控制台菜单。
    *   **原因：** 过度接管系统 UI 事件导致的功能倒退。

8.  **[#2143 文本选择仅复制首字符 (热词: Critical Bug)]**
    *   **状态：** OPEN | **更新：** 2026-03-19
    *   **内容：** 选择输出代码并使用 Ctrl+C 复制时，剪贴板仅获得第一个字符，导致无法复制代码片段。
    *   **原因：** 这是一个从 v1.0.3 开始持续存在的严重功能缺陷。

9.  **[#33 支持 OAuth HTTP MCP 服务器 (热词: Feature)]**
    *   **状态：** CLOSED | **评论：** 33
    *   **内容：** 社区呼吁支持 Figma 和 Atlassian 的 Remote MCP 服务器，这些服务依赖 OAuth 认证。
    *   **原因：** 拓展 Copilot CLI 在企业工具链生态中的连接能力。

10. **[#1157 全局 Hooks 配置支持 (热词: Feature)]**
    *   **状态：** OPEN | **👍 18**
    *   **内容：** 相比 Claude Code/Cursor，社区希望 Copilot 支持全局 Hooks 配置（如 `UserPromptSubmit`），而不是仅在仓库级别配置。
    *   **原因：** 减少重复配置，增强全局自动化工作流能力。

---

## 📌 重要 PR 进展
*(过去 24 小时内无新的 Pull Requests 更新)*

---

## 📈 功能需求趋势
基于过去 24 小时的 Issue 数据分析：

1.  **终端兼容性与原生体验倒退：**
    *   超过 60% 的活跃讨论集中在 v1.0.8/v1.0.9 版本引入的 UI 变更。
    *   **核心冲突：** 社区不希望 CLI 接管终端的原生滚动（TMUX）、快捷键（Linux Copy）和鼠标事件（Right Click）。用户倾向于使用系统级工具（如 `tmux`、`putty`）的原生能力，而不是 CLI 内部重新实现的 TUI。

2.  **模型可用性与 API 稳定性：**
    *   用户反馈了关于 Claude Sonnet 4.5/4.6 模型不可用的问题（#2099）。
    *   频繁出现 "Transient API Error" 和 503 错误（#2166, #2160），表明在 Copilot CLI 中使用付费模型时的连接稳定性有待提升。

3.  **高级配置与企业级集成：**
    *   **MCP (Model Context Protocol) 扩展：** 对 OAuth 认证 MCP 服务器的支持需求强烈。
    *   **配置标准化：** 用户要求严格遵守 XDG Base Directory Specification（#1750），以及支持 LSP 的初始化选项（#1269），显示出用户对 CLI 集成到复杂开发环境中的高标准要求。

---

## 🛡️ 开发者关注点
*   **关键痛点：** 新版本的 TUI 更新破坏了 "一切皆文本" 的 Unix 哲学。开发者无法在 SSH 会话中正常复制粘贴，无法在 Tmux 中滚动查看历史，这使得工具在远程开发场景下几乎不可用。
*   **强烈建议：** 在没有提供完美替代方案之前，不要覆盖操作系统的标准快捷键（如 Linux 的复制粘贴）和终端复用器的原生绑定。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：** 2026-03-20
**分析师：** AI 开发工具技术观察

---

### 1. 今日速览
今日 Kimi CLI 社区异常活跃，虽然未发布新版本，但维护者针对近期用户反馈的多个痛点提交了 **7 项修复 PR**，涵盖 Windows 文件锁冲突、VS Code 终端兼容性、Web UI 交互及 JSON 解析稳定性等关键问题。同时，社区关于 **"插件系统" (Skills/Tools)** 的讨论热度持续走高，标志着项目正从单一 CLI 工具向平台化生态演进。

### 2. 版本发布
*   **过去 24 小时：无新版本发布。**

---

### 3. 社区热点 Issues
以下为今日最值得关注的 10 个 Issue，反映了当前用户的主要痛点：

1.  **[#1380 ACP terminal tool fails with 'module acp has no attribute TerminalHandle'](https://github.com/MoonshotAI/kimi-cli/issues/1380)**
    *   **类型：** Bug
    *   **关注点：** v1.17 & v1.18 版本中，由于依赖库 `agent-client-protocol` 升级至 0.8.0 导致的 API 变更，使得终端工具适配器失效，影响核心对话功能。
    *   **状态：** 已有修复 PR (#1524) 提交。

2.  **[#1429 Windows 平台并发写入导致 Permission denied](https://github.com/MoonshotAI/kimi-cli/issues/1429)**
    *   **类型：** Bug
    *   **关注点：** Windows 用户在高并发场景下频繁遇到文件锁报错，导致会话中断。
    *   **状态：** 修复 PR (#1520) 引入了 `asyncio.Lock` 机制。

3.  **[#1437 Enter key appends `[13u` instead of sending message in VS Code](https://github.com/MoonshotAI/kimi-cli/issues/1437)**
    *   **类型：** Bug
    *   **关注点：** VS Code 集成终端的高频痛点，由于 Kitty 键盘协议冲突，导致回车键无法正常发送消息。
    *   **状态：** 修复方案已确定并提交 PR (#1514, #1502)。

4.  **[#1428 klmi web 的附件按钮点击后会执行一次 submit](https://github.com/MoonshotAI/kimi-cli/issues/1428)**
    *   **类型：** Bug
    *   **关注点：** Web UI 交互逻辑错误，点击附件会意外触发表单提交，阻碍正常文件上传流程。
    *   **状态：** 修复 PR (#1521) 已提交。

5.  **[#1513 Windows 安装脚本在默认 PowerShell 执行策略下闪退](https://github.com/MoonshotAI/kimi-cli/issues/1513)**
    *   **类型：** Bug
    *   **关注点：** 严重影响新用户的首体验，安装脚本在干净的 Windows 环境下静默失败。
    *   **状态：** 修复 PR (#1516) 已提交。

6.  **[#751 Slash commands execute immediately upon selection](https://github.com/MoonshotAI/kimi-cli/issues/751)**
    *   **类型：** Enhancement
    *   **关注点：** UX 优化需求。当前斜杠命令选中后需按两次 Enter，用户希望简化为一次。
    *   **状态：** 功能 PR (#1509) 已实现。

7.  **[#1475 Option to display current directory in prompt (regression)](https://github.com/MoonshotAI/kimi-cli/issues/1475)**
    *   **类型：** Enhancement/Bug
    *   **关注点：** v1.15.0 之后移除了窗口标题中的当前路径显示，导致多终端切换时难以区分项目。
    *   **状态：** 修复 PR (#1519) 已提交。

8.  **[#1378 JSON parsing error when tool call arguments contain control characters](https://github.com/MoonshotAI/kimi-cli/issues/1378)**
    *   **类型：** Bug
    *   **关注点：** 模型生成的 JSON 若包含换行符等控制字符会导致解析崩溃，影响会话恢复和工具调用。
    *   **状态：** 修复 PR (#1460) 建议使用非严格模式。

9.  **[#107 Kimi CLI Skill.md (Feature Request)](https://github.com/MoonshotAI/kimi-cli/issues/107)**
    *   **类型：** Enhancement
    *   **关注点：** 社区高度关注的特性，建议引入类似 `.cursorrules` 或 Anthropic 的 "Skill" 机制，允许用户自定义 Agent 能力。
    *   **状态：** 今日已有相关的 Plugin System PR (#1503) 出现。

10. **[#1492 Make commands length configurable](https://github.com/MoonshotAI/kimi-cli/issues/1492)**
    *   **类型：** Enhancement
    *   **关注点：** 用户反馈命令行显示的 `Used Shell...` 截断过于严重，难以查看完整命令。
    *   **状态：** 修复 PR (#1523) 将宽度适配终端尺寸。

---

### 4. 重要 PR 进展
今日提交的 PR 质量极高，主要集中在 Bug 修复和体验优化：

*   **[#1524 fix: replace removed acp.TerminalHandle](https://github.com/MoonshotAI/kimi-cli/pull/1524)**
    *   **内容：** 适配最新的 `agent-client-protocol` SDK，移除已废弃的 `TerminalHandle`，解决核心功能报错。
*   **[#1520 fix: add asyncio.Lock to prevent concurrent file write conflicts](https://github.com/MoonshotAI/kimi-cli/pull/1520)**
    *   **内容：** 解决 Windows 平台并发写入 `context.jsonl` 导致的 `PermissionError`。
*   **[#1514 fix: disable Kitty keyboard protocol to fix Enter key](https://github.com/MoonshotAI/kimi-cli/pull/1514)**
    *   **内容：** 通过禁用 Kitty 键盘协议，修复了 VS Code 终端中回车键输出 `[13u` 乱码的问题。
*   **[#1521 fix(web): prevent toolbar buttons from triggering form submit](https://github.com/MoonshotAI/kimi-cli/pull/1521)**
    *   **内容：** 修正 Web UI 按钮 HTML 类型，防止附件按钮误触发表单提交。
*   **[#1503 feat: add plugin system (Skills + Tools)](https://github.com/MoonshotAI/kimi-cli/pull/1503)**
    *   **内容：** **重磅更新**。引入插件系统，支持通过本地目录、Zip 或 Git URL 安装插件，并允许插件作为独立子进程提供工具。
*   **[#1509 feat: auto-submit slash commands upon selection](https://github.com/MoonshotAI/kimi-cli/pull/1509)**
    *   **内容：** 实现斜杠命令选中即执行，减少一次按键交互。
*   **[#1519 feat: display current directory in terminal title](https://github.com/MoonshotAI/kimi-cli/pull/1519)**
    *   **内容：** 恢复并在终端标题栏显示当前工作目录，解决多项目管理困扰。
*   **[#1516 fix: handle PowerShell Restricted execution policy](https://github.com/MoonshotAI/kimi-cli/pull/1516)**
    *   **内容：** 改进 Windows 安装脚本，优雅处理受限的 PowerShell 执行策略。
*   **[#1460 fix: use strict=False for JSON parsing](https://github.com/MoonshotAI/kimi-cli/pull/1460)**
    *   **内容：** 放宽 JSON 解析严格度，允许包含控制字符，增强鲁棒性。
*   **[#1515 fix(web): enable inline math formula rendering](https://github.com/MoonshotAI/kimi-cli/pull/1515)**
    *   **内容：** 修复 Web UI 无法渲染行内数学公式 (`$...$`) 的 Bug。

---

### 5. 功能需求趋势
基于过去 24 小时的数据分析，社区关注点呈现以下趋势：

*   **插件化与生态构建 (高热度):**
    *   Issue #107 和 PR #1503 显示，用户强烈希望打破 CLI 固有能力限制，通过 "Skills/Plugins" 机制扩展功能，自定义 Agent 行为。
*   **IDE 集成体验优化:**
    *   VS Code 终端兼容性 (Issue #1437)、会话管理 (Issue #1376) 和 Windows 环境下的稳定性是开发者反馈的重点。
*   **交互细节 (UX) 完善:**
    *   社区非常关注操作流的简洁性，如 "一键执行命令" (Issue #751)、"显示当前路径" (Issue #1475) 和 "查看完整命令" (Issue #1492)。
*   **多任务与并发处理:**
    *   出现了关于并发写入 (Issue #1429) 和多任务执行 (Issue #1482) 的讨论，表明用户正尝试将 Kimi CLI 用于更复杂的并行工作流。

---

### 6. 开发者关注点
*   **Windows 平台兼容性:** 今日 Issues 中超过 30% 涉及 Windows 特有问题（文件锁、PowerShell 脚本、Gitbash 启动失败），Windows 用户体验仍需大幅打磨。
*   **依赖库版本管理:** `agent-client-protocol` 的快速迭代导致了旧版 CLI 突然失效 (Issue #1380)，开发者呼吁更稳健的依赖锁定或迁移提示。
*   **基础稳定性:** 相比于添加大模型新功能，社区呼声最高的是修复 JSON 解析错误、连接错误 (Connection error) 和 HTTP Header 验证等阻碍正常使用的 Bug。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 (2026-03-20)

## 📅 今日速览
OpenCode 社区今日正处于一个关键的“架构重构期”与“大模型适配阵痛期”。核心开发团队（由 `thdxr` 和 `kitlangton` 主导）正在大规模推进 **OpenCode 2.0** 的底层架构迁移，将核心服务从旧模式迁移到 **Effect** 服务模式，并移除对 Bun 运行时的强依赖，以支持 Node.js。与此同时，社区爆发了关于 **Anthropic OAuth 认证故障** 和 **Claude API 使用限制** 的激烈讨论，导致大量 Issue 涌入。

## 🔖 版本发布
**无新版本发布**
尽管无 Release，但在 PR #16918 中，`opencode 2-0` 分支仍在活跃更新，涉及核心 LSP 服务器改进和包管理器的重大替换（由 Bun 转向 Npm Arborist）。

## 🔥 社区热点 Issues

以下是今日最值得关注的 10 个 Issue，涵盖了故障、核心架构争议和新功能需求：

1.  **[#18267 Claude code 0auth broked!?](https://github.com/anomalyco/opencode/issues/18267)** 🔥🔥🔥
    *   **摘要**: 过去 24 小时内热度最高的 Issue。大量用户反馈 Claude Code 官方 OAuth 认证出现 429 错误甚至无法连接。
    *   **重要性**: 直接影响 Anthropic 官方登录用户的可用性，评论数已达 96。

2.  **[#7456 fix: Claude Code API credentials](https://github.com/anomalyco/opencode/issues/7456)** 🔥🔥
    *   **摘要**: OpenCode 报错称“此凭证仅限 Claude Code 使用”，导致用户无法复用官方 CLI 的凭证。
    *   **社区反应**: 这是一个长期存在的痛点，用户急需在 OpenCode 中无缝使用 Claude Code 的订阅服务。

3.  **[#10416 OpenCode is not private by default?](https://github.com/anomalyco/opencode/issues/10416)** 🔥🔥
    *   **摘要**: 用户发现即使在本地部署 LLM，OpenCode 仍会在外部网络计算会话标题。
    *   **重要性**: 涉及**数据隐私**核心底线，引发了对“私有化部署”真实性的严重质疑。

4.  **[#18315 Claude Pro/Max auth flow returns Invalid token](https://github.com/anomalyco/opencode/issues/18315)** 🔥🔥
    *   **摘要**: 报告了一种新的认证故障，Claude Pro/Max 刷新令牌失败并提示 Invalid token。
    *   **趋势**: 与 #18267 类似，显示 Anthropic 服务的认证层目前极不稳定。

5.  **[#18265 Repository anomalyco/opencode-anthropic-auth no longer exists](https://github.com/anomalyco/opencode/issues/18265)** 🔥🔥
    *   **摘要**: 用户发现 OpenCode 的 Anthropic 认证仓库被删除/404，引发了对该 Provider 支持是否终止的恐慌。
    *   **社区反应**: 官方尚未在 Issue 中明确回复，增加了不确定性。

6.  **[#18242 Extra usage is required... infinite retry loop](https://github.com/anomalyco/opencode/issues/18242)** 🔥🔥
    *   **摘要**: 即使 Anthropic 已在 3 月 13 日移除了长上下文额外收费，OpenCode 仍提示该错误并陷入死循环。
    *   **重要性**: 典型的业务逻辑过时 Bug，导致无法进行长对话。

7.  **[#13546 Custom provider errors with "Unknown parameter: 'reasoningSummary'"](https://github.com/anomalyco/opencode/issues/13546)** 🔥
    *   **摘要**: 自定义 OpenAI 兼容提供商（如调用 GPT-5）时，因 OpenCode 强制注入 `reasoningSummary` 参数导致报错。
    *   **技术影响**: 阻碍了用户通过代理或中转服务使用最新模型。

8.  **[#7957 Ctrl+C should not exit OpenCode](https://github.com/anomalyco/opencode/issues/7956)** 🔥
    *   **摘要**: 极具争议的 UX 问题。`Ctrl+C` 目前直接退出程序，与通用的“复制”快捷键冲突，误触率极高。
    *   **社区反应**: 获得了 17 个赞，用户强烈要求修改此行为。

9.  **[#3743 Loop in certain models](https://github.com/anomalyco/opencode/issues/3743)** 🔥
    *   **摘要**: 某些模型（如 KIMI K2, MiniMax, GLM）在工具调用时会陷入无限循环。
    *   **重要性**: 暴露了 OpenCode Agent 控制循环在非 OpenAI/Anthropic 模型上的不稳定性。

10. **[#14972 Agent stops after tool execution (OpenAI-compatible providers)](https://github.com/anomalyco/opencode/issues/14972)** 🔥
    *   **摘要**: 使用 Gemini 或 LiteLLM 等 OpenAI 兼容接口时，Agent 在执行完工具后异常停止（finish_reason: stop）。
    *   **趋势**: 社区正在积极寻求摆脱单一模型依赖，此类兼容性 Bug 关乎生态多样性。

## 🛠️ 重要 PR 进展

今日代码仓库非常活跃，主要集中在 **Effect 架构重构** 和 **去 Bun 化**：

1.  **[#18319 effectify Pty service](https://github.com/anomalyco/opencode/pull/18319)**
    *   **内容**: 将终端 Pty 服务迁移至 Effect 模式，使用 `Map<PtyID, ActiveSession>` 管理状态。
    *   **意义**: 提升终端会话管理的稳定性和资源清理能力。

2.  **[#18318 refactor: replace Bun shell execution with portable Process utilities](https://github.com/anomalyco/opencode/pull/18318)**
    *   **内容**: 移除 `Bun.spawn` 和 `Bun.$`，改用跨平台的 `Process` 工具类。
    *   **意义**: **关键去依赖 PR**，为 OpenCode 未来脱离 Bun 运行时铺路。

3.  **[#18313 effectify SessionStatus service](https://github.com/anomalyco/opencode/pull/18313)**
    *   **内容**: 重构 SessionStatus 服务，引入 `runSyncInstance` 辅助函数。

4.  **[#18282 Skill: use forkScoped + Fiber.join for lazy init](https://github.com/anomalyco/opencode/pull/18282)**
    *   **内容**: 改进 Skill 插件的懒加载机制，使用 Effect 的 Fiber 语义。
    *   **意义**: 优化启动性能和资源占用。

5.  **[#18271 effectify Command service](https://github.com/anomalyco/opencode/pull/18271)**
    *   **内容**: 命令服务全面 Effect 化，替换了旧的 `Instance.state()` 模式。

6.  **[#18269 Effectify ToolRegistry service](https://github.com/anomalyco/opencode/pull/18269)**
    *   **内容**: 工具注册中心迁移至新模式，强化了实例上下文管理。

7.  **[#18316 refactor: abstract SQLite behind runtime-conditional import](https://github.com/anomalyco/opencode/pull/18316)**
    *   **内容**: 抽象 SQLite 层，使其能在 Bun (`bun:sqlite`) 和 Node.js (`node:sqlite`) 之间动态切换。
    *   **意义**: 打通了跨运行时数据库访问的障碍。

8.  **[#18308 refactor: replace BunProc with Npm module using @npmcli/arborist](https://github.com/anomalyco/opencode/pull/18308)**
    *   **内容**: **重磅变动**。移除 `src/bun/` 目录，放弃使用 `bun add/install`，改用 npm 官方的 `@npmcli/arborist` 进行包管理。
    *   **影响**: 旨在解决安装过程中的不确定性，构建更稳健的依赖管理。

9.  **[#18317 feat: quiet mode for CLI runs](https://github.com/anomalyco/opencode/pull/18317)**
    *   **内容**: 新增 `-q | --quiet` 参数，提供更清爽的 CLI 输出。
    *   **意义**: 回应脚本用户的需求，减少日志噪音。

10. **[#18306 feat(opencode): add Open WebUI provider](https://github.com/anomalyco/opencode/pull/18306)**
    *   **内容**: 增加对 Open WebUI 的 Provider 支持。
    *   **意义**: 拓展了本地模型生态的接入渠道。

## 📊 功能需求趋势

从今日的 Issues 和 PRs 中，我们可以提炼出以下社区趋势：

1.  **OpenCode 2.0 架构跃迁**:
    *   开发者正全力将核心代码库迁移到 **Effect** 系统。
    *   **去 Bun 依赖** 成为技术重点，转向 Node.js 兼容性和标准 npm 工具链（Arborist）。

2.  **认证与 API 的多态兼容**:
    *   用户极度渴望打破厂商锁定。Issues 显示了大量关于“复用 Claude Code 官方客户端凭证”和“支持自定义/第三方 OpenAI 兼容接口”的呼声。
    *   社区对单一 Provider 的稳定性（如 Anthropic 的故障）感到焦虑，急需多账户轮换和多 Provider 并行。

3.  **对非 Anthropic/OpenAI 模型的优化**:
    *   社区反馈的 Bug 中，很大一部分涉及 Kimi、GLM、Grok、LiteLLM 等非主流模型。这表明用户正在积极探索低成本或特定领域的模型，但 OpenCode 的 Agent 控制逻辑对这些模型的支持尚不完善（如 Loop 问题、Stop 信号问题）。

4.  **UX 与交互细节**:
    *   终端 UX (Ctrl+C 冲突) 和 隐私透明度 是用户非功能性反馈的焦点。

## 👨‍💻 开发者关注点

*   **稳定性**: 核心开发者目前更关注大规模重构 (Effectify) 而非修细碎的 Bug。这可能导致未来一段时间内，Edge cases 的 Bug 修复响应变慢。
*   **兼容性地狱**: 随着 OpenAI 推出 GPT-5 并引入 `reasoningSummary` 等新参数，以及 Anthropic 的政策变更，维护一个兼容所有 Provider 的统一接口正变得越来越困难。
*   **包管理策略**: 放弃 Bun 的包管理器转而拥抱 Node 生态标准的 Arborist，显示出项目正在向更工业化、更标准化的方向迈进，尽管这可能会牺牲一部分 Bun 带来的极速体验。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 (2026-03-20)

> **数据来源**: github.com/QwenLM/qwen-code
> **分析师**: AI 开发工具技术观察

---

## 1. 今日速览
Qwen Code 今日发布了 `v0.13.0-preview.0` 预览版及对应的 Nightly 版本，主要包含版本号升级及针对 OpenRouter 的 Pipeline 修复。社区反馈显示，**文件编辑功能的稳定性**再次成为用户痛点，多个 Issue 报告了严重的 "Edit Failed" 问题及 Agent 覆盖文件导致数据丢失的风险；同时，关于 **Skills 生态扩展** (`.agents/skills` 支持) 和 **权限系统** 的代码合并正在加速推进。

---

## 2. 版本发布
*   **[v0.13.0-nightly.20260320](https://github.com/QwenLM/qwen-code/releases) & [v0.13.0-preview.0](https://github.com/QwenLM/qwen-code/releases)**
    *   **Bump Version**: 版本号升级至 0.13.0。
    *   **Pipeline Fix**: 修复了从 OpenRouter 接收重复 `finish_reason` 数据块导致的处理错误 [PR #2403](https://github.com/QwenLM/qwen-code/pull/2403)。
    *   **System Prompt**: 增加了系统提示词自定义选项。

---

## 3. 社区热点 Issues
以下是过去 24 小时内最值得关注的 10 个讨论：

1.  **[#2460 CLI & VSC 编辑功能失效](https://github.com/QwenLM/qwen-code/issues/2460)**
    *   **摘要**: 用户反馈 CLI 和 VSCode 插件出现频繁且严重的 "edit failed"，甚至导致 Node/PS 编辑器损坏代码，称项目被彻底摧毁。
    *   **关注点**: **核心功能稳定性危机**，影响用户对工具的基本信任。

2.  **[#2499 Agent 数据丢失风险](https://github.com/QwenLM/qwen-code/issues/2499)**
    *   **摘要**: Agent 使用 `write_file` 覆盖文件时未先读取现有内容，导致文件内容被截断或覆盖。
    *   **关注点**: **安全性问题**，Agent 行为缺乏安全检查机制。

3.  **[#2454 /model 命令清空配置](https://github.com/QwenLM/qwen-code/issues/2454)**
    *   **摘要**: 手动添加到 `settings.json` 的模型配置，在使用 `/model` 命令后被静默删除。
    *   **关注点**: **配置管理逻辑缺陷**，已由 PR #2482/#2504 修复。

4.  **[#1922 编辑工具回退](https://github.com/QwenLM/qwen-code/issues/1922)**
    *   **摘要**: Python 文件编辑失败，该问题曾在旧版本修复，但在 v0.10.5 再次出现。
    *   **关注点**: **回归 Bug**，基础功能的不稳定性持续存在。

5.  **[#2496 中英文混合文件名识别错误](https://github.com/QwenLM/qwen-code/issues/2496)**
    *   **摘要**: 文件名如 "测试and测试.md" 会被误读为 "测试 and 测试.md"（带空格）。
    *   **关注点**: **国际化与字符处理**的细节体验。

6.  **[#2086 / #2155 支持 .agents/skills 目录](https://github.com/QwenLM/qwen-code/issues/2155)**
    *   **摘要**: 社区呼吁支持 `.agents/skills` (带 s) 目录，以符合新兴的跨工具 Skills 规范。
    *   **关注点**: **生态标准化**，已有对应的 PR #2476 处理。

7.  **[#2491 Linux 中文输入法兼容性](https://github.com/QwenLM/qwen-code/issues/2491)**
    *   **摘要**: Ubuntu 20.04 搜狗输入法环境下，CLI 无法输入单个汉字。
    *   **关注点**: **特定平台下的输入法兼容性**。

8.  **[#2379 Skills 继承机制](https://github.com/QwenLM/qwen-code/issues/2379)**
    *   **摘要**: 用户希望在 SKILL.md 中通过 `extends: bundled` 扩展内置的 Review 能力，而非完全复制。
    *   **关注点**: **插件系统的可扩展性**。

9.  **[#2420 Ctrl+Y 跳过限流等待](https://github.com/QwenLM/qwen-code/pull/2420)**
    *   **摘要**: 这是一个由 Issue 转化为 PR 的功能，用户希望在遇到 TPM 限流倒计时时能手动跳过。
    *   **关注点**: **用户体验优化**。

10. **[#2227 Mac 快捷键适配错误](https://github.com/QwenLM/qwen-code/issues/2227)**
    *   **摘要**: Mac 系统下终端仍显示 "Ctrl + Y" 而非 Cmd 组合键。
    *   **关注点**: **平台适配细节**。

---

## 4. 重要 PR 进展
以下 PR 对修复近期问题和引入新功能至关重要：

1.  **[#2482 / #2504 修复 /model 命令配置覆盖问题](https://github.com/QwenLM/qwen-code/pull/2482)**
    *   **状态**: Closed (Merged)
    *   **内容**: 修复了 `/model` 命令会覆盖 `settings.json` 中用户手动添加模型的问题。现在仅写入变更的 Key。

2.  **[#2476 支持 .agents/skills 目录](https://github.com/QwenLM/qwen-code/pull/2476)**
    *   **状态**: Open
    *   **内容**: 添加 `.agents` (复数) 作为技能提供者目录，紧跟跨工具规范趋势。

3.  **[#2475 / #2503 修复表格竖线转义问题](https://github.com/QwenLM/qwen-code/pull/2475)**
    *   **状态**: Closed / Open
    *   **内容**: 修复 Markdown 表格中包含 `|` 字符 (如 `A|B`) 时显示错乱的问题。

4.  **[#2283 引入基于规则的权限系统](https://github.com/QwenLM/qwen-code/pull/2283)**
    *   **状态**: Closed (Merged)
    *   **内容**: 引入 `Bash(git *)`, `Read(./secrets/**)` 等细粒度规则控制 Agent 权限，替代简单的工具黑/白名单。

5.  **[#2501 修复 VSCode 代理配置](https://github.com/QwenLM/qwen-code/pull/2501)**
    *   **状态**: Open
    *   **内容**: 修复 VS Code 插件在企业代理环境下无法连接 CLI 的问题，支持传递代理设置。

6.  **[#1978 VSCode 支持粘贴图片](https://github.com/QwenLM/qwen-code/pull/1978)**
    *   **状态**: Open (0.13.0)
    *   **内容**: 为 VS Code IDE Companion 添加图片粘贴支持，完善多模态输入流程。

7.  **[#2371 新增 /btw 旁路问答命令](https://github.com/QwenLM/qwen-code/pull/2371)**
    *   **状态**: Open (0.13.0)
    *   **内容**: 新增 `/btw` 命令，允许用户在不影响主对话历史的情况下进行快速问答，不消耗工具调用。

8.  **[#2502 Skills 支持 extends: bundled](https://github.com/QwenLM/qwen-code/pull/2502)**
    *   **状态**: Open
    *   **内容**: 允许用户在 SKILL.md 中通过 `extends: bundled` 原生扩展内置技能（如 /review），无需复制整个文件。

9.  **[#2490 多语言 i18n 与认证支持](https://github.com/QwenLM/qwen-code/pull/2490)**
    *   **状态**: Open
    *   **内容**: 增强阿里巴巴云 Coding Plan 认证支持，并为 WebUI 引入了多语言国际化系统。

10. **[#2474 修复 CRLF 换行符编辑问题](https://github.com/QwenLM/qwen-code/pull/2474)**
    *   **状态**: Closed (Merged)
    *   **内容**: 修复了当 `old_string` 包含 CRLF (`\r\n`) 而文件已标准化为 LF 时，Edit 工具失败的问题。

---

## 5. 功能需求趋势
从 Issue 和 PR 数据中提炼出的社区关注焦点：

*   **稳定性与可靠性**: 对 "Edit failed" 和文件损坏的投诉极其强烈，表明当前的 Agent 文件操作逻辑存在严重缺陷，需优先保证不破坏用户代码。
*   **IDE 集成体验**: VSCode 和 JetBrains 集成中的代理配置、进程残留、快捷键适配是主要优化方向。
*   **Skills 生态建设**: 社区正在积极推动 `.agents` 目录标准化以及更灵活的 Skill 继承机制。
*   **安全与权限**: 细粒度的权限控制不仅被提出，且已进入 Merge 阶段，反映用户对 Agent 自主性的担忧。

---

## 6. 开发者关注点
*   **文件操作风险**: Agent 调用 `write_file` 覆盖而非增量修改文件导致数据丢失，是当前最大的使用风险（Issue #2499）。
*   **配置持久化**: `settings.json` 容易被 CLI 命令（如 `/model`）重置或覆盖，导致自定义配置丢失（Issue #2454）。
*   **跨平台细节**: Mac 快捷键显示、Linux 中文输入法支持、Windows 启动速度等问题虽小，但影响日常开发体验。

---
*日报生成时间: 2026-03-20*

</details>

---
*本日报由 [agents-radar](https://github.com/yinwm/agents-radar) 自动生成。*