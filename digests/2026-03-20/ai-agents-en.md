# OpenClaw Ecosystem Digest 2026-03-20

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-03-20 01:18 UTC

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

## OpenClaw Deep Dive

# OpenClaw Project Digest: 2026-03-20

## 1. Today's Overview
OpenClaw is experiencing an extremely high-velocity development cycle with significant friction in the latest releases. The project generated 500 issue updates and 500 pull request updates in the last 24 hours, indicating a massive surge in community engagement and maintenance activity. However, the data reveals a "stability crunch": the latest versions (2026.3.12 - 2026.3.13) appear to have introduced widespread regressions, particularly affecting WhatsApp connectivity, local gateway handshakes, and Docker environments. Despite high community traffic (500 updated issues), 0 new releases were published today, suggesting the maintainers are in the middle of managing a complex stabilization effort.

## 2. Releases
**No new releases published today.**
*Note: The current latest stable version appears to be **2026.3.13** (based on referenced commits 61d171a), but users are reporting severe regressions compared to 2026.3.8 and earlier.*

## 3. Project Progress
*Note: While 500 PRs were updated, the majority listed in the top data are OPEN, meaning work is in progress. Significant merged/closed items were not present in the top-affecting data provided.*

**Key Areas Under Active Development:**
*   **ACP (Agent Control Protocol) Dispatch:** PR #49420 (Size: XL) addresses "ghost turns" and "stuck sessions" by wiring abort signals and timeouts. This is critical for reliability but is still under review.
*   **Ollama & Local Provider Fixes:** PRs #50729 and #50728 target a breaking change where tool call arguments from Ollama models were not being correctly deserialized from JSON strings, causing tool execution failures.
*   **Memory & Search Improvements:** PR #43498 introduces a `memory_refresh` tool to prevent data loss during updates, and PR #49200 adds **Tavily** as a bundled web search provider (expanding options beyond Brave/Perplexity).
*   **Docker Hardening:** PR #32424 (Stale/Updated) attempts to fix setup crashes and runtime tooling reliability for Mac Docker environments.

## 4. Community Hot Topics
*   **[#75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** (46 comments, 👍 63)
    *   **Status:** The most requested feature in the project's history remains unaddressed.
    *   **Need:** Users demand desktop parity with macOS/iOS/Android. The community feels "left behind" on Linux and Windows platforms.

*   **[#49836: Phishing Scam Warning](https://github.com/openclaw/openclaw/issues/49836)** (32 comments, 👍 18)
    *   **Status:** Security Alert.
    *   **Need:** Immediate community awareness regarding a fake repository (`Scalarterlight/0penC...`) phishing for wallet keys. This is currently the most discussed security topic.

*   **[#10010: Agent Teams - Parallel Coordination](https://github.com/openclaw/openclaw/issues/10010)** (12 comments, 👍 2)
    *   **Status:** Feature Request.
    *   **Need:** Users want advanced multi-agent orchestration (Agent Teams), similar to experimental features in other AI tooling, moving beyond single-agent sessions.

*   **[#50090: Community Skill Development & ClawHub](https://github.com/openclaw/openclaw/issues/50090)** (5 comments, 👍 1)
    *   **Status:** Ecosystem Feedback.
    *   **Need:** Frustration that the "write a SKILL.md and publish" promise is not working in practice. The gap between the plugin promise and reality is widening.

## 5. Bugs & Stability
**Current Stability: RED.** There is a cluster of regressions in versions 2026.3.12 and 2026.3.13 that effectively break core functionality for specific workflows.

*   **[CRITICAL] WhatsApp "No active listener" Epidemic**
    *   **Affected Issues:** #34741, #45171, #46659, #48109, #48126, #45576 (All showing high activity/closure comments).
    *   **Symptoms:** "No active WhatsApp Web listener" errors occur during CLI sends (`openclaw message send`), agent message tools, or cron jobs, even when status shows "Connected".
    *   **Severity:** High. Breaks proactive messaging and automations while inbound auto-reply may still work.
    *   **Fix Status:** Multiple issues are CLOSED, but reports persist in #48126 and #46659, suggesting the fix in 2026.3.13 may be partial or regression-specific.

*   **[HIGH] Gateway CLI & Loopback Failures**
    *   **Affected Issues:** #45504, #45560, #45173, #49510, #49950.
    *   **Symptoms:** `openclaw devices list`, `openclaw gateway probe`, and local CLI commands fail with "gateway closed (1000)" or timeout. This suggests a breaking change in how the local CLI authenticates or handshakes with the local loopback gateway in Docker/macOS environments.
    *   **Fix PR:** PR #46892 addresses the aggressive 3s timeout.

*   **[HIGH] Docker & Matrix Extension Breakage**
    *   **Affected Issues:** #47717, #45232.
    *   **Symptoms:** Matrix plugin fails to load in Docker due to missing source tree imports (`src/` references in runtime). Control UI stuck on "pairing required" after upgrade to 2026.3.13.

*   **[MEDIUM] Authentication / API Key Issues**
    *   **Affected Issues:** #23538 (Anthropic 401), #41293 (Mistral 422), #44851 (Kimi 401).
    *   **Analysis:** A cluster of issues suggests changes in how API keys or headers are passed to LLM providers, specifically for Anthropic (setup-token) and Mistral.

## 6. Feature Requests & Roadmap Signals
*   **MCP (Model Context Protocol) Client:** Issue #29053 requests native support for external MCP servers. This is a strong roadmap signal as MCP is becoming an industry standard for tool connectivity.
*   **MiniMax M2.7 Support:** Issue #50234 requests support for newer MiniMax models (M2.7-highspeed).
*   **Zero-Downtime Context Compaction:** Issue #49233 proposes an External Memory Provider API to solve the "agent blackout" (30-60s freeze) during memory compaction, a major UX pain point for long-running sessions.
*   **Local Search Alternatives:** Issue #16629 notes Brave Search API is no longer free. PR #47279 attempts to add **DuckDuckGo** as a free alternative search provider to fill this gap.

## 7. User Feedback Summary
*   **Frustration with Regressions:** Users are reporting that upgrades (specifically to 2026.3.12/13) break previously working features (WhatsApp, CLI Gateway, Docker).
*   **Installation Fatigue:** Issue #39447 and #50294 highlight friction with `npm install` and `pnpm` setup on Linux/Docker, suggesting the "easy install" promise needs work.
*   **Platform Inequality:** The disproportionate attention to iOS/macOS vs Linux/Windows (Issue #75) remains a sore spot.
*   **Plugin/Extension Complexity:** Feedback in #50090 and #29053 indicates that while the plugin system is powerful, it is currently too hard for average users to customize or extend without deep knowledge of the codebase.

## 8. Backlog Watch
*   **[#10841: Time Awareness](https://github.com/openclaw/openclaw/issues/10841)** (14 👍): Agents cannot accurately set reminders because they guess the current time instead of knowing it. A fundamental logic gap in the scheduler.
*   **[#16137: Message Buffering](https://github.com/openclaw/openclaw/issues/16137)** (8 👍): Intermediate messages are buffered and delivered only after the agent turn completes, destroying the "real-time" feeling of AI responses.
*   **[#25359: Per-Agent Plugin Slots](https://github.com/openclaw/openclaw/issues/25359)** (4 👍): Global plugin slots prevent multi-agent setups (e.g., a "Work" agent vs. "Personal" agent) from having different memory or tool configurations.
*   **Stale/PR Stacks:**
    *   PR #27443 (Multi-user RBAC) and PR #26732 (Outbound Rate Limiting) are marked "stale" or large size, indicating they are roadmap items that haven't made it to merge priority yet.

---

## Cross-Ecosystem Comparison

# Ecosystem Cross-Project Comparison Report
**Date:** 2026-03-20
**Analyst:** Senior Open Source Ecosystem AI Agent

## 1. Ecosystem Overview
The open-source personal AI agent ecosystem is currently undergoing a **phase of aggressive standardization and infrastructure hardening**. While the initial hype around "autonomous agents" has settled, the community is now rigorously solving complex reliability issues, specifically around **context memory management, multi-agent orchestration, and sandbox security**. There is a visible bifurcation in the market: core framework projects (like OpenClaw and NanoClaw) are doubling down on stability and regression fixing, while derivative UI-focused projects (like EasyClaw) are prioritizing user experience and authentication flows. **Interoperability is the new competitive moat**, with the **Model Context Protocol (MCP)** becoming a must-have integration rather than a niche feature.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Primary Focus | Health/Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | **Stable (2026.3.13)** | Regression Fixes | **RED ALERT.** High activity but critical stability crisis (WhatsApp, Gateway). |
| **NanoBot** | 24 | 52 | Nightly | Enterprise Ready | **High.** Focus on observability and secure configuration. |
| **Zeroclaw** | 43 | 50 | **v0.5.1 Stable** | Security Parity | **High.** Just hit stable; heavy tension between safety and usability. |
| **PicoClaw** | 40 | 106 | Nightly (v0.2.3) | Refactor/Churn | **Med/High.** High merge velocity but provider instability issues. |
| **NanoClaw** | ~10 | ~10 | None | Polyglot Engines | **Healthy.** Rapid security fixes, expanding beyond Anthropic. |
| **NullClaw** | ~10 | ~10 | **v2026.3.18** | Protocol/A2A | **Stable.** Relatively quiet, focused on protocols and infrastructure. |
| **IronClaw** | 50 | 50 | **v0.20.0** | Self-Repair | **Recovering.** Major release features self-healing but has upgrade friction. |
| **LobsterAI** | 19 | 33 | **v2026.3.19** | Enterprise/i18n | **Fragile.** Release v3.19 introduced gateway regressions. |
| **CoPaw** | 50 | 50 | **v0.1.0** | Multi-Agent UI | **CRITICAL.** Major release causing "deadlocks" and upgrade failures. |
| **Moltis** | 4 | 3 | None | Governance | **Stable.** Low volume, focus on file locking and git safety. |
| **TinyClaw** | 0 | 2 | None | Refactoring | **Quiet.** Focus on internal adapter patterns; no community noise. |
| **ZeptoClaw** | ~3 | ~3 | None | ACP Protocol | **Niche.** Deep technical work on Agent Client Protocol. |
| **EasyClaw** | 2 | 3 (Merged) | **v1.7.2/1.7.3** | UI/Productization | **Productizing.** Heavy focus on UI/UX and authentication polish. |

---

## 3. OpenClaw's Position

**Advantages:**
*   **Community Dominance:** OpenClaw remains the undisputed leader in raw community mass (500+ updates/day), serving as the "reference implementation" for the ecosystem.
*   **Platform Breadth:** Despite user complaints, it maintains the widest array of platform integrations (WhatsApp, Matrix, Slack, Discord), which competitors are still racing to match.

**Technical Approach:**
*   OpenClaw is currently paying the "technical debt tax" of its monolithic architecture. While competitors like **NanoClaw** and **PicoClaw** are successfully decoupling logic or refactoring adapters, OpenClaw is struggling with "ghost turns" and global handshake failures (Issues #45504, #34741).

**Community Sentiment:**
*   **Negative:** The user base is currently the most frustrated among all top-tier projects due to the **Stability Crunch** in versions 2026.3.12/13.
*   **Recommendation:** OpenClaw needs to pause feature addition (currently focused on `tavily` search and obscure model support) to execute a "Stability Sprint" similar to what **IronClaw** just attempted with v0.20.0.

---

## 4. Shared Technical Focus Areas

*   **Model Context Protocol (MCP) & Extensibility**
    *   **Projects:** OpenClaw, NanoClaw, CoPaw, ZeptoClaw.
    *   **Signal:** There is a universal shift away from hardcoded tools toward dynamic, protocol-based tool discovery. OpenClaw is receiving requests for native MCP clients; ZeptoClaw is building ACP (Agent Client Protocol) to solve similar connectivity issues.

*   **Multi-Agent / Multi-Workspace Architecture**
    *   **Projects:** CoPaw (Leading), LobsterAI, OpenClaw, Moltis.
    *   **Signal:** Users are moving past single-agent chatbots. **CoPaw's v0.1.0** release is entirely dedicated to multi-agent workspace isolation, and **LobsterAI** users are explicitly requesting "Agent Teams" and "Managerial Agents" (OpenClaw #10010, Moltis #453).

*   **Sandboxing & Governance**
    *   **Projects:** Zeroclaw, Moltis, NanoClaw, NanoBot.
    *   **Signal:** A major philosophical debate is occurring.
        *   **Zeroclaw** is criticized for being "too safe" (blocking `ffmpeg`).
        *   **Moltis** and **NanoClaw** are actively implementing "No-Verify" blocks to stop agents from bypassing git hooks.
        *   **NanoBot** is rushing to implement `{env:VAR}` syntax to prevent leaking keys in config files.
    *   **Conclusion:** The ecosystem is prioritizing "Safety by Default" as enterprises adopt these tools.

*   **Provider Fragmentation & "LiteLLM"**
    *   **Projects:** PicoClaw, NullClaw, ZeptoClaw.
    *   **Signal:** Every project is chasing support for niche providers (Novita AI, Qwen, Alibaba Cloud). This highlights a lack of standardization in LLM APIs, forcing every agent framework to build its own adapter layer.

---

## 5. Differentiation Analysis

| Feature | PicoClaw | NanoClaw | Zeroclaw | CoPaw | EasyClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Core Architecture** | **High-Modularity** | **Polyglot** (Multi-Engine) | **Strict Sandbox** | **Multi-Agent OS** | **Client App** |
| **Target User** | Hackers / Tinkerers | DevOps / Backend Ops | Paranoid Security Teams | Collaboration Teams | End Consumers |
| **Differentiation** | Best support for **local/CLI** providers (Ollama, Codex). | Best **non-Anthropic** support (OpenAI, Codex). | Best **security constraints** (Configurable timeouts, tool blocking). | Best **Workspace Isolation** (Multiple agents, one UI). | Best **UI/UX** (Captcha, Auth, Themes). |

---

## 6. Community Momentum & Maturity

*   **Tier 1: High Velocity / High Pain (The "Growth Pains" Tier)**
    *   **OpenClaw:** Massive scale, massive bugs.
    *   **CoPaw:** Just launched a major architectural shift (v0.1.0) and is currently fighting fires (deadlocks, upgrade failures).
    *   **PicoClaw:** Extremely high PR churn (106 in 24h), indicating rapid iteration but potential instability.

*   **Tier 2: Stabilizing / Enterprise Ready**
    *   **IronClaw:** Successfully released v0.20.0 with self-repair mechanisms.
    *   **Zeroclaw:** Just reached "Stable" v0.5.1; focusing now on user complaints (usability).
    *   **NullClaw:** Quiet reliability; focusing on protocol implementation (A2A).

*   **Tier 3: Niche / UI Wrapper**
    *   **EasyClaw:** Focused entirely on the "Application Layer" (UI, Themes, Auth) rather than agent logic.
    *   **TinyClaw:** Refactoring in silence; likely preparing for a future push.

---

## 7. Trend Signals for AI Developers

1.  **The "LiteLLM" Pattern is Standardizing:** Developers should no longer assume "OpenAI-compatible" is sufficient. Projects are actively baking in `litellm` or building complex adapter chains to handle discrepancies in how different providers (Anthropic, OpenRouter, DeepSeek) handle tool calls and streaming.
2.  **"God Mode" vs. "Safe Mode":** There is a clear segmentation between projects designed for **Local Personal Use** (Users want "God Mode" to run bash scripts freely—e.g., Zerocraw Issue #1478) vs. **Enterprise Deployment** (Users want RBAC, Audit Logs, and Sandboxing—e.g., NanoBot PRs).
3.  **Voice & Audio is the Next Frontier:** **PicoClaw** and **NanoClaw** are seeing high demand for TTS/STT (Voice transcription, Voice reply). The text-only chat interface is considered insufficient for 2026.
4.  **The "Upgrade Anxiety" Problem:** As these projects mature, **database migration and configuration compatibility** are becoming the primary blockers for adoption (see IronClaw #1328, LobsterAI #500, CoPaw #1895). Successful projects will need to invest in robust migration tooling.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the project digest for **NanoBot** on **2026-03-20**.

### 1. Today's Overview
NanoBot is experiencing a period of high activity and rapid iteration, with **52 Pull Requests** and **24 Issues** updated in the last 24 hours. The project appears to be in a "heavy development" phase, focusing on expanding platform support (QQ, Discord, Web) and refining core runtime capabilities (session management, security, observability). While the sheer volume of open PRs (41) indicates robust contribution, it also suggests potential bottlenecks in code review and merging. Recent updates show a strong focus on enterprise readiness, with significant efforts being put into security hardening (environment variables), secret management, and interactive configuration tools.

### 2. Releases
**No new releases** published today. The project continues to rely on nightly builds (`uv tool install ... @nightly`) for users to access the latest features, particularly the new `onboard` configuration wizard.

### 3. Project Progress
Significant architectural improvements and feature additions are currently under review or have been recently merged:

*   **Security & Configuration:**
    *   **Secret Management:** PR [#2212](https://github.com/HKUDS/nanobot/pull/2212) and [#2218](https://github.com/HKUDS/nanobot/pull/2218) introduce the `{env:VAR}` syntax to allow API keys and sensitive configs to be injected from environment variables rather than stored in `config.json`. This addresses a critical security concern raised in Issue [#1873](https://github.com/HKUDS/nanobot/issues/1873).
    *   **Onboard Wizard:** PR [#2266](https://github.com/HKUDS/nanobot/pull/2266) fixes crashes in the new interactive configuration wizard, ensuring the feature is stable for wider adoption.

*   **Runtime & Channel Enhancements:**
    *   **Interactive Steering:** PR [#1224](https://github.com/HKUDS/nanobot/pull/1224) proposes a "Steering Loop" architecture. This allows the agent to dynamically interrupt its current tool execution flow to handle new user messages, addressing the "blocking" pain point where users currently have to wait for a loop to finish or use `/stop`.
    *   **Observability:** PR [#2268](https://github.com/HKUDS/nanobot/pull/2268) adds tracing for LiteLLM calls, and PR [#1490](https://github.com/HKUDS/nanobot/pull/1490) adds Langfuse support, providing developers with better debugging and cost-monitoring tools.
    *   **Cron & Session:** PR [#2276](https://github.com/HKUDS/nanobot/pull/2276) enables interactive conversations for cron jobs by allowing them to share the user's session context.

### 4. Community Hot Topics
The community is actively debating architectural limits and platform integrations:

*   **Real-time Interaction (Issue [#2133](https://github.com/HKUDS/nanobot/issues/2133))**
    *   **Discussion:** A highly active thread (18 comments) discussing how to handle user messages while an Agent loop is running.
    *   **Underlying Need:** Users want the bot to be "interruptible" for approvals or status updates without stopping the task, moving from a simple request-response model to a collaborative, stateful interaction model.

*   **Security Concerns (Issue [#1873](https://github.com/HKUDS/nanobot/issues/1873))**
    *   **Discussion:** Users are worried that the agent can trivially access its own `config.json` using `exec()`, potentially leaking API keys.
    *   **Underlying Need:** A demand for stricter sandboxing or permission isolation, especially for containerized deployments.

*   **QQ Channel Support (Issue [#2226](https://github.com/HKUDS/nanobot/issues/2226) & PR [#1667](https://github.com/HKUDS/nanobot/pull/1667))**
    *   **Discussion:** There is a strong push from the community to enable file and image sending/receiving in the QQ channel.
    *   **Underlying Need:** Feature parity across different messaging platforms (Slack/DingTalk vs. QQ), as QQ is currently text-only.

### 5. Bugs & Stability
Several stability issues have been identified, some with pending fixes:

*   **Anthropic Provider Failure ([Issue #2200](https://github.com/HKUDS/nanobot/issues/2200)):** Users report a `litellm.BadRequestError` when using Anthropic, rendering the provider broken.
*   **Telegram Response Duplication ([Issue #2235](https://github.com/HKUDS/nanobot/issues/2235)):** Responses are appearing twice in Telegram, suspected to be a "faux streaming" glitch. **Fix proposed in PR [#2272](https://github.com/HKUDS/nanobot/pull/2272)** for network error handling.
*   **Configuration Persistence Bug ([Issue #2241](https://github.com/HKUDS/nanobot/issues/2241)):** The `nanobot onboard` wizard saves partial edits even if the user cancels/exits, leading to corrupted configurations.
*   **OpenRouter Model Stripping ([Issue #2222](https://github.com/HKUDS/nanobot/issues/2222)):** The gateway incorrectly strips model prefixes (e.g., `openrouter/hunter-alpha` -> `hunter-alpha`), causing validation errors for unknown models.

### 6. Feature Requests & Roadmap Signals
Based on today's activity, future versions will likely include:

*   **Plugin System ([Issue #2231](https://github.com/HKUDS/nanobot/issues/2231)):** A request to implement a plugin architecture (similar to Copilot CLI) to extend agent functionality without modifying the core codebase.
*   **Cycle Detection ([PR #2271](https://github.com/HKUDS/nanobot/pull/2271)):** Introduction of a `CycleDetector` to prevent the agent from entering infinite tool-calling loops, a critical stability feature for autonomous agents.
*   **Model Switching ([Issue #2257](https://github.com/HKUDS/nanobot/issues/2257)):** Requests for runtime model/provider switching via commands (e.g., in Telegram), rather than requiring config restarts.

### 7. User Feedback Summary
*   **Pain Points:**
    *   **Session Management:** Users are frustrated that sessions (context memory) grow indefinitely and cannot be easily cleared or restarted without manually deleting files or restarting the service ([Issue #2062](https://github.com/HKUDS/nanobot/issues/2062)).
    *   **Configuration Complexity:** While the new `onboard` wizard is welcome, users are encountering bugs with partial saves and argument parsing (e.g., `-c` flag errors in [Issue #2250](https://github.com/HKUDS/nanobot/issues/2250)).
    *   **Platform Nuances:** Feishu users report that bots do not reply in the correct thread context ([Issue #2256](https://github.com/HKUDS/nanobot/issues/2256)) and cannot process images ([Issue #2242](https://github.com/HKUDS/nanobot/issues/2242)).

### 8. Backlog Watch
*   **Matrix Channel Instability ([Issue #1300](https://github.com/HKUDS/nanobot/issues/1300)):** Open since Feb 27, reports that the Matrix channel fails to start. Needs attention from channel maintainers.
*   **DingTalk File Uploads ([Issue #1864](https://github.com/HKUDS/nanobot/issues/1864)):** Open since March 11, highlighting that file support is missing despite being a standard feature in other channels.
*   **Steering Loop ([PR #1224](https://github.com/HKUDS/nanobot/pull/1224)):** A massive, high-impact PR introducing dynamic task interruption. It has been open for nearly a month and represents a major architectural shift; its progress is worth watching.

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw Project Digest: 2026-03-20

## 1. Today's Overview
Zeroclaw is experiencing a **high-velocity development cycle**, transitioning from beta build v0.5.1-beta.379 to the stable **v0.5.1** release today. With 43 issues and 50 pull requests updated in the last 24 hours, the project is rapidly iterating on feature stability, specifically focusing on channel parity, security constraints, and internationalization. The release cadence has been intense, with 10 distinct version tags pushed, moving quickly from beta refinements to a production-ready release. Community engagement remains robust, though user sentiment highlights a growing tension between the project's stringent default security posture and usability for local, non-hosted deployments.

## 2. Releases
**🎉 New Release: v0.5.1 (Stable)**
The project has moved to a stable release, incorporating features tested through the recent beta series.
*   **Agent Core:** Runtime model switching is now enabled via the `model_switch` tool.
*   **Security & Config:** Security policy summaries are now injected directly into the LLM system prompt (addressing previous "trial-and-error" behavior). Sub-agent timeouts are now configurable via `config.toml`.
*   **Skills & i18n:** Autonomous skill creation has been added. Tool descriptions have been externalized to support translations (i18n).
*   **System:** Default heartbeat interval adjusted from 30 minutes to 5 minutes.

**Recent Beta Updates (v0.5.1-beta.378 - v0.5.1-beta.414):**
The beta cycle focused heavily on **Channel Interaction** and **Safety**:
*   **New Commands:** Added `/stop` command to cancel in-flight tasks across channels.
*   **Interruptions:** Enabled `interrupt_on_new_message` support for Discord and Mattermost.
*   **Voice:** Added TTS (Text-to-Speech) voice reply support for the Telegram channel.
*   **Refinement:** Added `read_skill` for Compact mode and `thread_replies` option for Slack.

## 3. Project Progress
**Significant Merged/Closed Features:**
*   **Channel Parity:** Discord and Mattermost received feature parity with Telegram/Slack regarding message interruptions (PRs #3918, #3917) and cancellation commands (PR #3891).
*   **Delegate Configuration:** Addressed configuration rigidity by making sub-agent timeouts fully configurable in `config.toml` (PR #3992, #4004).
*   **Developer Experience:** Improved repository consistency by adding `Justfile` for commands, `taplo.toml` for TOML formatting, and `.gitattributes` for line endings (PRs #3874, #3873, #3875).
*   **Docker Defaults:** Changed the default Docker container CMD from `gateway` to `daemon` to ensure channel listeners spawn correctly out-of-the-box (PR #3897).
*   **Tooling:** Added a `CalculatorTool` for precise arithmetic operations (PR #4012) and a `Jira` integration tool (PR #3997).

## 4. Community Hot Topics
*   **[Feature] Security vs. Usability Debate** ([#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478) - 42 comments)
    *   **The Issue:** Users are frustrated that Zeroclaw blocks execution of tools (like `ffmpeg`) even when security configurations are set to permissive levels.
    *   **User Sentiment:** "You are very safe, safe to the point where this bot can only be a chat robot... Why should I install it if I have to do everything manually?"
    *   **Analysis:** There is a strong demand for a "God Mode" or "Local Only" security profile that bypasses strict sandboxing for personal, trusted environments.

*   **[Feature] Alibaba Cloud Coding Plan Support** ([#3882](https://github.com/zeroclaw-labs/zeroclaw/issues/3882) - 8 comments | PR [#3889](https://github.com/zeroclaw-labs/zeroclaw/pull/3889))
    *   **The Issue:** Users want support for Alibaba Cloud's specialized coding models.
    *   **Progress:** A PR is currently open to add this provider, indicating active development on this request.

*   **[Enhancement] HITL (Human-in-the-Loop) for Telegram** ([#1865](https://github.com/zeroclaw-labs/zeroclaw/issues/1865) - 6 comments)
    *   **The Issue:** Users want interactive approval buttons (Yes/No) in Telegram, rather than hardcoded auto-approval.

*   **[Feature] LiteLLM Integration** ([#2602](https://github.com/zeroclaw-labs/zeroclaw/issues/2602) - 4 comments)
    *   **The Issue:** Request to officially register LiteLLM as a provider alias to simplify gateway setups.

## 5. Bugs & Stability
**🔴 High Severity (S1 - Workflow Blocked):**
*   **[Bug] Context Overflow** ([#3987](https://github.com/zeroclaw-labs/zeroclaw/issues/3987)): Users report running out of context immediately, even with small sessions.
*   **[Bug] Ollama Tool-Calling Failure** ([#3999](https://github.com/zeroclaw-labs/zeroclaw/issues/3999)): Security prompts and tool usage fail completely when using local Ollama instances.
*   **[Bug] Web UI 405 Error** ([#3764](https://github.com/zeroclaw-labs/zeroclaw/issues/3764)): Custom provider headers work in CLI but fail in the Web UI.
*   **[Bug] Tool Hallucinations (Channels)** ([#4009](https://github.com/zeroclaw-labs/zeroclaw/issues/4009)): LLMs hallucinate tool usage text instead of emitting native tool calls on non-CLI channels (Feishu/Lark).
*   **[Bug] Severe Hallucinations** ([#3982](https://github.com/zeroclaw-labs/zeroclaw/issues/3982)): Agent reports false system states (e.g., claiming `lsb_release` is missing when it isn't).

**🟠 Medium Severity (S2 - Degraded):**
*   **[Bug] Autonomy Level Ignored** ([#3952](https://github.com/zeroclaw-labs/zeroclaw/issues/3952)): Configuration `autonomy.level = "full"` is ignored; agents still simulate permission requests.
*   **[Bug] Anthropic Cache 0%** ([#3977](https://github.com/zeroclaw-labs/zeroclaw/issues/3977)): Prompt caching on Haiku 4.5 shows 0% hit rate.
*   **[Bug] Native Tool Call Text Dropped** ([#3974](https://github.com/zeroclaw-labs/zeroclaw/issues/3974)): Assistant explanation text is dropped during draft updates in channels.

## 6. Feature Requests & Roadmap Signals
*   **Full Docker Image:** There is a request (#3642) for a "full" Docker image with all feature flags (like WhatsApp) enabled by default to lower the barrier to entry.
*   **Reasoning Visibility:** Users want a `/reasoning` command to understand what the agent is "thinking" (#2401).
*   **Script Execution in Skills:** Users are requesting a configuration option to explicitly allow `.sh` or `.bash` scripts within skills, which are currently blocked by security policy (#1889).
*   **Web UI Theming:** A new PR (#3986) suggests adding a theme system and settings modal to the web interface.

## 7. User Feedback Summary
*   **Pain Point - Security Paralysis:** A significant portion of feedback revolves around the default security policy being too restrictive for local/home use cases. Users feel they are fighting the agent to get work done.
*   **Configuration Complexity:** While improvements are being made (e.g., `LiteLLM` alias requests), users are still struggling with complex setups, particularly around provider headers and Web UI configuration.
*   **Channel Inconsistencies:** Users are actively requesting feature parity between channels (e.g., Slack thread replies, Telegram HITL buttons), indicating that the multi-platform support is a major use case.

## 8. Backlog Watch
*   **Security Sandbox Enforcement:** There is a claim that `[security.sandbox]` configuration exists but is never actually applied to shell commands (#3983), meaning commands run with full host access regardless of settings. This requires maintainer verification.
*   **Cron Agent Tool Permissions:** An issue (#3920) suggests that cron jobs have an `allowed_tools` code path, but it does not persist correctly, leading to broken automation workflows.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest: 2026-03-20

## 1. Today's Overview
PicoClaw is experiencing a **high-velocity development cycle** with significant momentum towards the v0.2.3 release. In the last 24 hours, the project processed 106 Pull Requests (roughly equal split between open and merged/closed) and 40 Issues, indicating a robust merge pipeline and active community engagement. However, stability remains a mixed bag; while high-impact bug fixes for providers (Anthropic, OpenAI-compatible, CLI tools) are landing, users are reporting regressions related to "Cooldown" logic and persistent Feishu (Lark) channel connectivity issues. The current codebase is rapidly evolving, particularly in provider interoperability and the agent refactor domain.

## 2. Releases
**New Release: Nightly Build v0.2.3-nightly.20260320**
*   **Status**: Automated unstable build.
*   **Key Changes**: Full changelog available [here](https://github.com/sipeed/picoclaw/compare/v0.2.3...main).
*   **Note**: This nightly likely includes the recent batch of provider fixes (Anthropic, CLI tool extraction) and documentation updates. Users are advised to exercise caution due to the unstable nature of nightly builds.

## 3. Project Progress
*   **Provider Reliability (Merged)**: Several critical fixes for provider compatibility were merged.
    *   **Anthropic API**: Fixed a 400 error caused by duplicate `tool_result` blocks and improper history sanitization ([PR #1793](https://github.com/sipeed/picoclaw/pull/1793)).
    *   **CLI Providers**: Improved robustness in extracting tool calls from JSON outputs for `claude-cli`, `gemini-cli`, and `codex-cli`, fixing failures when JSON was pretty-printed or mixed with text ([PR #1813](https://github.com/sipeed/picoclaw/pull/1813)).
    *   **OpenAI Compatibility**: Fixed serialization issues where empty content strings with tool calls caused errors with strict providers ([PR #1460](https://github.com/sipeed/picoclaw/pull/1460)).
*   **Launcher & Ops**: Improved the launcher to better detect externally managed gateways (e.g., via systemd) and recognize credential-free CLI providers like `gemini-cli` ([PR #1811](https://github.com/sipeed/picoclaw/pull/1811), [PR #1810](https://github.com/sipeed/picoclaw/pull/1810)).
*   **Subagent Refactor**: Fixed a bug where subagents failed to find tools because the `ToolRegistry` was not being propagated correctly after the multi-agent refactor ([PR #1711](https://github.com/sipeed/picoclaw/pull/1711)).

## 4. Community Hot Topics
*   **[Feature] Audio/TTS Support** ([#1648](https://github.com/sipeed/picoclaw/issues/1648))
    *   **Engagement**: 14 comments.
    *   **Analysis**: There is strong demand for voice interaction capabilities. Users are pushing for the integration of existing TTS/ASR PRs into the main gateway to enable voice-driven agents.
*   **[Bug] OpenRouter/Free Models** ([#901](https://github.com/sipeed/picoclaw/issues/901), [#1247](https://github.com/sipeed/picoclaw/issues/1247), [#1790](https://github.com/sipeed/picoclaw/issues/1790))
    *   **Engagement**: High volume of reports (12, 2, and 0 comments respectively).
    *   **Analysis**: Users are struggling to configure "free" or OpenRouter models. The issues range from configuration inheritance (API keys) to protocol prefix stripping (`openrouter/` being removed), suggesting the OpenRouter provider needs a usability audit.
*   **[Feature] Event-Driven Hooks** ([#1795](https://github.com/sipeed/picoclaw/issues/1795))
    *   **Engagement**: Active discussion.
    *   **Analysis**: Users want to move beyond simple cron jobs and active skills to an event-driven architecture (triggers on message send, command execution), similar to OpenClaw's system.

## 5. Bugs & Stability
*   **[High Severity] Anthropic 400 Errors**: Duplicate tool results were breaking the Anthropic API. **Status:** Fix merged in [PR #1793](https://github.com/sipeed/picoclaw/pull/1793).
*   **[High Severity] Feishu (Lark) Instability**: Multiple users report the bot frequently stops replying due to network disconnections and API card limits ([Issue #1767](https://github.com/sipeed/picoclaw/issues/1767), [#1727](https://github.com/sipeed/picoclaw/issues/1727)). **Status:** Open; requests for auto-reconnect mechanisms.
*   **[Medium Severity] OpenRouter Fallback Logic**: The fallback chain defaults to OpenRouter-only candidates, causing total failure when that provider hits a cooldown ([Issue #1581](https://github.com/sipeed/picoclaw/issues/1581)).
*   **[Medium Severity] Tool Result Sanitization**: Historical context handling was not merging consecutive tool results, leading to API rejections ([Issue #1792](https://github.com/sipeed/picoclaw/issues/1792)). **Status:** Fix merged in [PR #1793](https://github.com/sipeed/picoclaw/pull/1793).

## 6. Feature Requests & Roadmap Signals
*   **Observability**: Request for **OpenTelemetry (OTel) GenAI support** to meet enterprise observability standards ([Issue #1731](https://github.com/sipeed/picoclaw/issues/1731)).
*   **Agent Management**:
    *   **Context Management**: Continued discussion on boundaries, compression, and token budgeting ([Issue #1439](https://github.com/sipeed/picoclaw/issues/1439)).
    *   **Cron/Dashboard**: Requests to manage Cron jobs and view cost statistics (token usage) via the Web Dashboard ([Issue #1797](https://github.com/sipeed/picoclaw/issues/1797)).
*   **Channels**:
    *   **OpenAI API Channel**: A channel that acts *as* an OpenAI API server to embed PicoClaw into existing workflows ([Issue #1738](https://github.com/sipeed/picoclaw/issues/1738)).
    *   **Email Channel**: Proposal to use email as a transport mechanism ([Issue #1794](https://github.com/sipeed/picoclaw/issues/1794)).
    *   **OpenIM**: Inquiry into support for the OpenIM protocol ([Issue #1372](https://github.com/sipeed/picoclaw/issues/1372)).
*   **UI/UX**: Requests to hide "thought process" tags (``) in the chat interface for better readability ([Issue #1714](https://github.com/sipeed/picoclaw/issues/1714)) and add progress feedback during tool execution ([Issue #571](https://github.com/sipeed/picoclaw/issues/571)).

## 7. User Feedback Summary
*   **Configuration Fatigue**: Users are frustrated by DRY (Don't Repeat Yourself) violations in configuration, specifically regarding `api_key` and `api_base` inheritance in `model_list` ([Issue #1635](https://github.com/sipeed/picoclaw/issues/1635)).
*   **Platform Fragmentation**: There is notable friction running PicoClaw on 32-bit ARM (armhf) devices and Android Termux, with requests for pre-built launchers ([Issue #1778](https://github.com/sipeed/picoclaw/issues/1778), [#1675](https://github.com/sipeed/picoclaw/issues/1675)).
*   **Documentation Gaps**: Users are unsure about runtime behavior, such as whether the gateway needs a restart after editing workspace `.md` files ([Issue #1728](https://github.com/sipeed/picoclaw/issues/1728)). **Status:** Clarified in [PR #1740](https://github.com/sipeed/picoclaw/pull/1740).

## 8. Backlog Watch
*   **Context Management**: The Agent Refactor track 6 ([#1439](https://github.com/sipeed/picoclaw/issues/1439)) remains a critical, complex task that is still under discussion.
*   **Feedback Loops**: The request for "progress feedback during tool execution" ([#571](https://github.com/sipeed/picoclaw/issues/571)) was opened in February and remains open, indicating a gap in user experience for long-running tasks.
*   **Strict Model Support**: Issues regarding strict OpenAI-compatible providers and tool call serialization ([#1460](https://github.com/sipeed/picoclaw/pull/1460)) have been lingering but saw movement today.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-03-20

## 1. Today's Overview
NanoClaw is experiencing **high-velocity development** today, with significant activity focused on infrastructure, security, and new messaging channels. The project shows **healthy maintenance** with rapid responses to critical security vulnerabilities, though there is a growing backlog of CI merge conflicts in skill branches requiring manual intervention. Development is trending toward **polyglot agent support** (OpenAI, email, Discord) and enhanced system observability.

## 2. Releases
*No new releases published today.*

## 3. Project Progress
**Security & Hygiene:**
*   **Prompt Leakage Fixed:** A critical security issue where container error logs exposed full user prompts has been closed and fixed ([#1150](https://github.com/qwibitai/nanoclaw/issues/1150), [#1191](https://github.com/qwibitai/nanoclaw/pull/1191)).
*   **Git Hook Security:** A new mechanism to prevent agents from bypassing git pre-commit hooks via `--no-verify` was implemented ([#1271](https://github.com/qwibitai/nanoclaw/pull/1271)).

**Core Capabilities:**
*   **Conversation Search:** A major feature adding BM25/FTS5 conversation search and WhatsApp file attachment support was closed ([#1160](https://github.com/qwibitai/nanoclaw/pull/1160)).
*   **Voice Transcription:** Support for transcribing Telegram voice messages via local Whisper has been merged ([#1269](https://github.com/qwibitai/nanoclaw/pull/1269)).
*   **Performance:** Docker stop timeouts were reduced to make agent restarts significantly faster ([#651](https://github.com/qwibitai/nanoclaw/pull/651)).

## 4. Community Hot Topics
**Infrastructure & Authentication (High Engagement)**
*   **[Podman Support](https://github.com/qwibitai/nanoclaw/issues/957)**: Users are requesting official documentation and support for Podman as a Docker alternative (4 reactions).
*   **[Anthropic Auth Token](https://github.com/qwibitai/nanoclaw/issues/853)**: Users report friction with the official Claude Code CLI token (`ANTHROPIC_AUTH_TOKEN`) not being recognized during setup.

**Feature Requests**
*   **[Agent Swarming](https://github.com/qwibitai/nanoclaw/pull/1265)**: High interest in enabling multi-agent collaboration via Discord webhooks.
*   **[Web Channels](https://github.com/qwibitai/nanoclaw/issues/1273)**: Community members are building custom web channels to move beyond just messenger-based control.

## 5. Bugs & Stability
**Critical (Fixed)**
*   **[Security: Prompt Logging](https://github.com/qwibitai/nanoclaw/issues/1150)**: *Closed.* Full user prompts were being written to disk in container error logs. Fixed in PR #1191.

**Medium (Active)**
*   **[Linux systemd Fallback](https://github.com/qwibitai/nanoclaw/issues/413)**: The service setup on Linux (non-root SSH) falls back to `nohup` unnecessarily when systemd user sessions fail, instead of attempting to fix the session.
*   **[Setup Verification Token Gap](https://github.com/qwibitai/nanoclaw/issues/853)**: The setup script fails to validate `ANTHROPIC_AUTH_TOKEN`, breaking workflows for users of the standard Claude Code CLI.
*   **[DB Migration Bug](https://github.com/qwibitai/nanoclaw/issues/1272)**: A migration script incorrectly marks all Telegram chats as groups (`is_group=1`), breaking DM logic.

**Maintenance / Stability**
*   **[Merge Conflicts](https://github.com/qwibitai/nanoclaw/issues/1279)**: Multiple automated "merge-forward" workflows are failing for `skill/apple-container` and `skill/compact` branches due to conflicts with `main`.

## 6. Feature Requests & Roadmap Signals
*   **Observability:** PR [#1111](https://github.com/qwibitai/nanoclaw/pull/1111) proposes detailed API usage tracking (costs, tokens) and PR [#1280](https://github.com/qwibitai/nanoclaw/pull/1280) adds opt-in PostHog diagnostics. This signals a user desire for better cost management and debugging tools.
*   **Memory Enhancement:** There is a strong push to replace the basic vector memory with [LanceDB Pro](https://github.com/qwibitai/nanoclaw/pull/1283) for hybrid BM25+vector retrieval, addressing current limitations in keyword-heavy queries.
*   **Polyglot Engines:** PR [#963](https://github.com/qwibitai/nanoclaw/pull/963) proposes adding OpenAI Codex as an alternative agent engine, suggesting users want to run NanoClaw independent of Anthropic's infrastructure.

## 7. User Feedback Summary
**Pain Points:**
*   **Setup Friction:** Users are struggling with environment differences, specifically missing `ANTHROPIC_AUTH_TOKEN` support and silent failures in browser automation on headless Linux servers.
*   **Security Paranoia:** Users are actively looking for ways to lock down agent behavior (git hook bypasses, prompt leakage), indicating high stakes in deployment environments.

**Positive Sentiment:**
*   Users appreciate the "well designed" architecture and the speed of feature development (e.g., emojis, voice transcription).
*   There is active community contribution, with users building custom web channels and sharing them.

## 8. Backlog Watch
*   **[Skill Branch Maintenance](https://github.com/qwibitai/nanoclaw/issues/1279)**: Requires manual developer intervention to resolve merge conflicts in `skill/apple-container` and `skill/compact`.
*   **[Alternative Container Runtime](https://github.com/qwibitai/nanoclaw/issues/957)**: Documentation support for Podman is pending.
*   **[Headless UX](https://github.com/qwibitai/nanoclaw/pull/1281)**: Improvements for VPS/server setups are currently in draft PR form.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest: 2026-03-20

## 1. Today's Overview
NullClaw is demonstrating high development velocity with significant maintenance and feature expansion activity. The project released version `v2026.3.18`, addressing critical configuration bugs related to Docker, Telegram, and Matrix integrations. Developer focus appears split between stabilizing core infrastructure (scheduler, identity injection, atomic operations) and expanding protocol capabilities (A2A v0.3.0, new providers like Novita AI and Qwen). While the closure rate for issues is healthy (50%), a few emergent bugs regarding interactive commands and memory persistence require immediate attention to ensure production stability.

## 2. Releases
**v2026.3.18** (Released: 2026-03-19)
*   **Changes:**
    *   **Provider Expansion:** Added Novita AI as an OpenAI-compatible provider (#621).
    *   **Docker Configuration:** Fixed the container starter config to align with the current schema, removing deprecated `default_provider` fields (#636).
*   **Migration Notes:** Users pulling the latest Docker image (`ghcr.io/nullclaw/nullclaw:latest`) should verify their configuration maps to the new `agents.defaults.model.primary` schema, as top-level defaults are no longer supported.

## 3. Project Progress
*   **Core Stability & Fixes:**
    *   **Identity Injection:** Fixed a bug where configured AIEOS identities were parsed but never injected into system prompts (#633).
    *   **Matrix Integration:** Updated private room detection logic to use joined member counts, preventing misclassification of quiet rooms (#634).
    *   **Telegram:** Implemented suppression logic for draft retries to peers returning `TEXTDRAFT_PEER_INVALID`, reducing log spam (#635).
    *   **Nix Environment:** Pinned the development shell to Zig 0.15.2 to resolve build failures on NixOS (#637).
*   **Protocol & Workflow:**
    *   **A2A Protocol:** Upgraded implementation to v0.3.0, adding new task states (rejected, auth-required) and removing legacy method aliases (#630).
*   **Open Pull Requests:**
    *   **Scheduler API:** A move to expose the live cron scheduler via a REST API is in progress (#648), aiming to eliminate race conditions between the CLI and the daemon.
    *   **Portability:** Efforts are ongoing to simplify atomic access using `portable_atomic.zig` (#640).

## 4. Community Hot Topics
*   **[Bug] Telegram Draft Errors** (#626 - 🔥 2 comments)
    *   *Issue:* Users reported severe log spam caused by `TEXTDRAFT_PEER_INVALID` errors when using the Telegram bot.
    *   *Resolution:* This was addressed quickly in PR #635 and released in v2026.3.18.
*   **[Bug] Docker Config Crash** (#629 - ⚠️ Critical)
    *   *Issue:* The "Getting Started" Docker command failed immediately due to outdated configuration schemas in the image (`Config error: top-level default_provider is not supported`).
    *   *Analysis:* This represents a significant barrier to entry for new users, blocking the onboarding flow entirely. It was fixed in the latest release.

## 5. Bugs & Stability
*   **[Critical] Gateway Hang on Interactive Commands** (#644)
    *   *Description:* The gateway hangs completely (requiring `kill -9`) when asked to run interactive CLI tools like `htop` or `btop` via Telegram.
    *   *Status:* Open.
*   **[High] Memory System Failure** (#646)
    *   *Description:* A user reports the persistent memory system is failing to store or recall information during conversation triggers.
    *   *Status:* Open. No fix PR linked yet.
*   **[Medium] AIEOS Identity Not Loading** (#625)
    *   *Description:* Configuration for `identity.aieos_path` was being ignored.
    *   *Status:* **Fixed** in v2026.3.18 via PR #633.
*   **[Medium] Podman HTTP Gateway** (#629)
    *   *Description:* Generic Podman run commands failed due to schema mismatches.
    *   *Status:* **Fixed** in v2026.3.18.

## 6. Feature Requests & Roadmap Signals
*   **Qwen Code CLI Support** (#647): Request to add Qwen Code CLI as a provider due to generous free token limits.
*   **Adaptive Intelligence Pipeline** (#527): A massive, open PR introducing post-turn quality scoring and skill routing. This indicates a strong roadmap direction toward "learning" agents that optimize model selection per task.
*   **Cron CLI Enhancements** (#645, #643): Requests to make cron management fully functional via CLI (adding `--account` flags) and fixing JSON schema requirements for agent jobs. These are likely to land soon given the active PR status.

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Installation Experience:** The Docker configuration issue (#629) caused significant friction for new users trying to run the default container.
    *   **Observability:** Users are frustrated by generic error messages (e.g., "error.ApiError" in #619) and are requesting detailed logging to debug agent failures without reading the source code.
    *   **Integration Stability:** The Telegram integration is the most reported surface for bugs (draft errors, interactive hangs), suggesting it is a high-usage but sensitive component.
*   **Use Cases:**
    *   Users are actively deploying NullClaw on NixOS and via Podman, indicating a strong technical/DevOps-savvy user base.
    *   There is interest in using local/hybrid providers (Qwen, local MCP servers) to minimize costs.

## 8. Backlog Watch
*   **Memory System Integrity (#646):** As the memory system is a core value proposition, the report that it "doesn't seem to work" is a high-priority item for maintainer review to validate core functionality.
*   **Interactive Command Handling (#644):** The inability to run interactive tools without crashing the gateway is a severe regression for users relying on the agent for system administration tasks.
*   **Open Telemetry Diagnostics (#638):** A user is unable to connect the OTEL collector despite correct network configuration, suggesting potential documentation gaps or protocol issues in the diagnostics stack.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest: 2026-03-20

## 1. Today's Overview
IronClaw is experiencing a high-velocity development cycle with significant maintenance and feature advancement. The project remains highly active, with 100 updates (50 issues, 50 PRs) in the last 24 hours. A focus on code quality, performance optimization, and infrastructure hardening is evident, driven by an automated "Staging CI Review" process that identified numerous bugs and inefficiencies. The release of **v0.20.0** highlights progress in self-repair capabilities and testing frameworks.

## 2. Releases
**v0.20.0 (Released 2026-03-19)**
This release focuses on robustness and developer experience.
*   **Self-Repair Mechanisms:** Introduction of `stuck_threshold`, store, and builder logic to handle agent stalls ([#712](https://github.com/nearai/ironclaw/pull/712)).
*   **Testing Enhancements:** A new `FaultInjector` framework for `StubLlm` was added to improve testing resilience ([#1233](https://github.com/nearai/ironclaw/pull/1233)).
*   **UX Improvements:** The gateway settings page has been unified with subtabs for better organization.

## 3. Project Progress
*   **Merged/Closed Features:**
    *   **Performance:** Significant optimization of the embedding cache via LRU implementation to reduce redundant HTTP calls and memory overhead ([#1423](https://github.com/nearai/ironclaw/pull/1423), [#235](https://github.com/nearai/ironclaw/pull/235)).
    *   **Connectivity:** Managed tunnels targeting issues and SIGPIPE errors were addressed ([#1093](https://github.com/nearai/ironclaw/pull/1093)), alongside fixes for OAuth and MCP authentication flows ([#1375](https://github.com/nearai/ironclaw/pull/1375)).
    *   **Security & Safety:** A leak scan was implemented for WASM channel callbacks to prevent credential exposure ([#1377](https://github.com/nearai/ironclaw/pull/1377)).
*   **Active Discussions:**
    *   **XL Features:** Major PRs are open for "Adaptive Learning" (skill synthesis/user profiles) ([#1187](https://github.com/nearai/ironclaw/pull/1187)) and generic hosted OAuth/MCP auth ([#1375](https://github.com/nearai/ironclaw/pull/1375)).
    *   **Bug Triage:** A consolidation of staging CI fixes is underway ([#1427](https://github.com/nearai/ironclaw/pull/1427)).

## 4. Community Hot Topics
*   **[OPEN] Support "Socket Mode" for Slack channel** ([#1155](https://github.com/nearai/ironclaw/issues/1155))
    *   *Discussion:* Users are requesting WebSocket-based "Socket Mode" for Slack integration to avoid opening public inbound webhooks (NAT-friendly).
    *   *Underlying Need:* Improved deployment security and flexibility for users behind firewalls.
*   **[OPEN] Upgrade to v0.19.0 fails... Migration checksum mismatch** ([#1328](https://github.com/nearai/ironclaw/issues/1328))
    *   *Discussion:* Users upgrading from v0.18.0 are facing startup failures due to a modified migration file `V6__routines.sql`.
    *   *Underlying Need:* Stability in database migrations and clearer upgrade paths for production deployments.

## 5. Bugs & Stability
*   **[CRITICAL] Embedding cache clones embeddings on every hit** ([#1429](https://github.com/nearai/ironclaw/issues/1429))
    *   Identified by CI; causes high memory overhead and performance degradation. Fix in progress ([#1438](https://github.com/nearai/ironclaw/pull/1438)).
*   **[CRITICAL] Version mismatch in telegram artifact URL** ([#1414](https://github.com/nearai/ironclaw/issues/1414))
    *   High confidence risk of breakage in Telegram artifact delivery.
*   **[HIGH] Unbounded message Vec growth in routine tool loop** ([#826](https://github.com/nearai/ironclaw/issues/826))
    *   Routine loops accumulate messages without trimming, leading to large contexts and potential token limit overruns.
*   **[HIGH] Upgrade Failures:** As noted in topic [#1328](https://github.com/nearai/ironclaw/issues/1328).
*   **[HIGH] Thundering herd: concurrent requests for same uncached key** ([#1431](https://github.com/nearai/ironclaw/issues/1431))
    *   Cache stampede effects during high load.

## 6. Feature Requests & Roadmap Signals
*   **Adaptive Learning System:** PR [#1187](https://github.com/nearai/ironclaw/pull/1187) proposes a mechanism for skill synthesis and user profiles, signaling a push towards more autonomous agent capabilities.
*   **OpenAI Codex Integration:** PR [#744](https://github.com/nearai/ironclaw/pull/744) aims to allow ChatGPT Pro/Plus subscribers to use IronClaw without separate API keys, potentially lowering entry barriers.
*   **Slack Socket Mode:** Request [#1155](https://github.com/nearai/ironclaw/issues/1155) indicates strong demand for this specific networking feature.
*   **Per-Job MCP Filtering:** PR [#1243](https://github.com/nearai/ironclaw/pull/1243) suggests a move towards stricter resource isolation and security control for individual jobs.

## 7. User Feedback Summary
*   **Upgrade Anxiety:** The migration checksum issue ([#1328](https://github.com/nearai/ironclaw/issues/1328)) reflects a user pain point regarding database stability and upgrade safety.
*   **Deployment Constraints:** Requests for Socket Mode ([#1155](https://github.com/nearai/ironclaw/issues/1155)) and MCP tunnel fixes ([#1093](https://github.com/nearai/ironclaw/pull/1093)) indicate users are running IronClaw in restricted network environments where opening ports is difficult.
*   **Performance vs. Features:** The high volume of CI-generated issues regarding "Stringly-typed" parameters, N+1 queries, and O(n) loops suggests the codebase is suffering from technical debt as features are added rapidly.

## 8. Backlog Watch
*   **PR #635: Orphaned tool_results and parallel tool_result merging** ([#635](https://github.com/nearai/ironclaw/pull/635))
    *   *Status:* Open since March 6.
    *   *Impact:* Critical bug causing Anthropic API to return empty responses. Needs immediate attention.
*   **PR #333: Slack Socket Mode** ([#333](https://github.com/nearai/ironclaw/pull/333))
    *   *Status:* Recently closed/merged (referenced in activity).
    *   *Note:* Resolves the community request in #1155.
*   **PR #744: OpenAI Codex Provider** ([#744](https://github.com/nearai/ironclaw/pull/744))
    *   *Status:* Open since March 8.
    *   *Impact:* High value feature for users, large scope (XL).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-03-20**.

### 1. Today's Overview
LobsterAI is currently experiencing a **high-velocity development cycle** coinciding with the release of version **2026.3.19**. The project shows very high activity with 33 Pull Requests and 19 Issues updated in just 24 hours. The community focus is split between stabilizing the new release (which introduces enterprise WeChat upgrades and infrastructure changes) and expanding functionality (new Skills and i18n support). While feature addition is active, there is a notable surge in user-reported stability issues regarding the **OpenClaw gateway**, **model compatibility**, and **upgrade errors**, suggesting the latest version may have introduced some regressions that require immediate attention.

---

### 2. Releases
* **Version: 2026.3.19** (Released: 2026-03-19)
    *   **Enterprise Integration:** Upgraded dependencies related to Enterprise WeChat (`chore: 升级企业微信相关依赖`).
    *   **Infrastructure:** Includes changes to the Gateway restart logic and build fixes for macOS stub packages.
    *   **Documentation:** Updated `AGENTS.md` with OpenClaw and i18n guidelines.
    *   **Breaking/Regression Alerts:** Multiple user reports (Issues #500, #511, #540) indicate problems with upgrade paths and gateway stability immediately following this release.

---

### 3. Project Progress
* **Merged & Closed PRs (18 items):**
    *   **Build System:** Fixed macOS signing failures caused by residual `.bin` broken links after cleaning stub packages ([#520](https://github.com/netease-youdao/LobsterAI/pull/520)).
    *   **Windows Stability:** Fixed `EPERM` errors when the workspace is set to a drive root (e.g., `D:\`) ([#513](https://github.com/netease-youdao/LobsterAI/pull/513)) and optimized OpenClaw gateway startup sequences ([#527](https://github.com/netease-youdao/LobsterAI/pull/527)).
    *   **Sandbox Removal:** Removed sandbox functionality, aligning with the shift in architecture ([#523](https://github.com/netease-youdao/LobsterAI/pull/523)).
    *   **Gateway Logic:** Fixed Windows process stop event races to prevent erroneous restarts ([#528](https://github.com/netease-youdao/LobsterAI/pull/528)).

* **Active Development (Open PRs):**
    *   **New Skills:** Added `qrcode` (WiFi/URL generation) and `github-profile` (repo/user stats) skills ([#538](https://github.com/netease-youdao/LobsterAI/pull/538), [#537](https://github.com/netease-youdao/LobsterAI/pull/537)).
    *   **Internationalization (i18n):** A massive push to fix hardcoded Chinese strings, including OpenClaw gateway status messages, model selectors, and dark mode UI elements ([#536](https://github.com/netease-youdao/LobsterAI/pull/536), [#535](https://github.com/netease-youdao/LobsterAI/pull/535), [#532](https://github.com/netease-youdao/LobsterAI/pull/532)).
    *   **Core Fixes:** Implemented `max_completion_tokens` for OpenAI models, fixed scheduled task `NaN` bugs, and optimized database queries ([#515](https://github.com/netease-youdao/LobsterAI/pull/515), [#530](https://github.com/netease-youdao/LobsterAI/pull/530), [#533](https://github.com/netease-youdao/LobsterAI/pull/533)).

---

### 4. Community Hot Topics
* **Feature Request: Multi-Agent Orchestration**
    *   **Issue:** [#541](https://github.com/netease-youdao/LobsterAI/issues/541)
    *   **Topic:** Users are requesting a framework where multiple agents can coordinate and call each other, moving beyond single-agent execution.
    *   **Analysis:** This indicates a maturing user base looking to build complex, hierarchical workflows rather than just single-shot tasks.

* **Feature Request: OpenClaw vs. CoWorker Dual Kernel**
    *   **Issue:** [#497](https://github.com/netease-youdao/LobsterAI/issues/497)
    *   **Topic:** Users want the ability to switch freely between the "OpenClaw" and "CoWorker" engines within the settings.
    *   **Analysis:** Users perceive value in both engines (perhaps stability vs. features) and want flexibility rather than being locked into one.

* **Feedback: Feishu (Lark) Streaming Response**
    *   **Issue:** [#521](https://github.com/netease-youdao/LobsterAI/issues/521)
    *   **Topic:** Complaint that Feishu integration lacks real-time streaming (unlike ClawX), making the system feel unresponsive during long tasks.
    *   **Analysis:** Real-time feedback is critical for user patience in agent workflows; the current "wait until finish" approach is a major UX friction point.

---

### 5. Bugs & Stability
* **Severity: High - Gateway Instability**
    *   **Issue:** [#540](https://github.com/netease-youdao/LobsterAI/issues/540) - "OpenClaw frequent restarts, unusable."
    *   **Status:** Reported in v3.19. PR [#527](https://github.com/netease-youdao/LobsterAI/pull/527) attempted a fix for startup logic, but user reports suggest the issue persists.
* **Severity: High - Model Compatibility**
    *   **Issue:** [#501](https://github.com/netease-youdao/LobsterAI/issues/501) - OpenAI API fails with `max_tokens` error.
    *   **Status:** Fix available in open PR [#515](https://github.com/netease-youdao/LobsterAI/pull/515) (switches to `max_completion_tokens`). Needs urgent merge.
* **Severity: Medium - Regression in Upgrade Path**
    *   **Issue:** [#500](https://github.com/netease-youdao/LobsterAI/issues/500) - Upgrade from v2.2 to v3.17 fails on Windows 11; configuration loss.
    *   **Status:** Open.
* **Severity: Medium - Feishu Integration Broken**
    *   **Issue:** [#511](https://github.com/netease-youdao/LobsterAI/issues/511) - Bot does not reply in Feishu (while WeChat works).
    *   **Status:** Open.

---

### 6. Feature Requests & Roadmap Signals
* **Multi-Agents Support:** Explicit request for multi-agent coordination ([#541](https://github.com/netease-youdao/LobsterAI/issues/541)).
* **Deployment:** Requests for ARM64 server and Docker deployment support ([#539](https://github.com/netease-youdao/LobsterAI/issues/539)).
* **Model Support:** Requests for compatibility with custom OpenAI-response style APIs ([#492](https://github.com/netease-youdao/LobsterAI/issues/492)).
* **UI/UX:**
    *   Dark mode adaptation fixes ([#525](https://github.com/netease-youdao/LobsterAI/issues/525)).
    *   Startup interface text optimization ([#519](https://github.com/netease-youdao/LobsterAI/issues/519)).

---

### 7. User Feedback Summary
*   **Pain Points:**
    *   **Upgrade Anxiety:** Users are terrified of upgrading (v2.2 -> v3.17) due to broken configurations and lost settings.
    *   **Interface Inconsistency:** Heavy criticism on incomplete internationalization (i18n) and dark mode, making the tool feel unpolished for non-Chinese users.
    *   **Memory/Context Issues:** Reports of the agent "looping" or returning previous answers instead of addressing new prompts ([#498](https://github.com/netease-youdao/LobsterAI/issues/498)).
    *   **Integration Reliability:** Feishu (Lark) integration is currently perceived as less stable than WeChat integration.
*   **Positive Signals:**
    *   The rapid addition of community Skills (QR codes, GitHub profiles) shows an engaged ecosystem of developers building on top of the platform.

---

### 8. Backlog Watch
*   **Critical Unanswered Issues:**
    *   **[Feature Request] Support OpenClaw and CoWorker dual kernel switching** ([#497](https://github.com/netease-youdao/LobsterAI/issues/497)): This is a strategic architectural request that remains unaddressed.
    *   **[Bug] Feishu Bot not replying** ([#511](https://github.com/netease-youdao/LobsterAI/issues/511)): A critical integration failure for enterprise users.
*   **Stale PRs requiring attention:**
    *   **PR #515** (OpenAI token fix) is critical for anyone using the latest OpenAI models and should be prioritized for the next patch.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Digest: 2026-03-20

## 1. Today's Overview
TinyClaw is currently undergoing significant architectural refactoring to improve modularity and expand user interface capabilities, despite a quiet 24-hour window regarding issue tracking. While there were no new issues filed or closed, and no new releases published, development remains active on the pull request front. The focus appears to be split between backend modernization—specifically decoupling CLI logic—and enhancing the visual interaction layer. Overall project health appears stable, with engineering efforts directed towards technical debt reduction and feature expansion rather than bug fixing.

## 2. Releases
*No new releases published in the current reporting period.*

## 3. Project Progress
**Pull Requests Updated (Last 24h):**
Although no pull requests were merged today, the following PRs saw updates, signaling ongoing development:

*   **`refactor(core): extract CLI logic into adapter pattern` ([#242](https://github.com/TinyAGI/tinyagi/pull/242))**
    *   **Status:** Open
    *   **Progress:** This PR represents a major step in modernizing the codebase. By extracting provider-specific CLI invocation logic from `invoke.ts` into independent adapter modules, the project is moving towards a more maintainable and scalable architecture. The introduction of a standardized `AgentAdapter` interface suggests preparation for easier integration of new AI providers in the future.
*   **`feat(office): redesign the live office workspace` ([#212](https://github.com/TinyAGI/tinyagi/pull/212))**
    *   **Status:** Open
    *   **Progress:** Active development continues on the `/office` experience. The recent update implies the team is iterating on the design and implementation of the live workspace environment, likely aiming to improve user interaction and agent visualization capabilities.

## 4. Community Hot Topics
*No significant comment activity or reaction counts (👍) were detected in the last 24 hours to classify "Hot Topics."*

However, the two open PRs currently represent the primary focus of the engineering community:
*   **Backend Architecture:** The community's attention is on the adapter pattern refactoring ([#242](https://github.com/TinyAGI/tinyagi/pull/242)), addressing the need for a cleaner separation of concerns within the core invocation logic.
*   **Frontend Experience:** The redesign of the office workspace ([#212](https://github.com/TinyAGI/tinyagi/pull/212)) is the other focal point, highlighting a demand for a more robust or visually appealing interactive environment.

## 5. Bugs & Stability
*No new bugs, crashes, or regressions were reported in the Issues section today.*
*   **Stability Status:** The lack of new issues suggests the current main branch is relatively stable, or users are waiting for the pending refactors to stabilize before reporting edge cases related to older logic.

## 6. Feature Requests & Roadmap Signals
Based on the open pull requests, we can infer the following roadmap signals:
*   **Multi-Provider Support:** The refactoring in PR [#242](https://github.com/TinyAGI/tinyagi/pull/242) indicates a strategic move to support diverse AI backends (Claude, Codex, OpenCode) more uniformly. This suggests the roadmap includes plugging in additional providers or standardizing how existing ones are managed.
*   **Enhanced Workspace UI:** PR [#212](https://github.com/TinyAGI/tinyagi/pull/212) signals that the "Live Office" feature is a priority. Users can expect a redesigned interface, potentially moving away from static command-line outputs towards a richer, graphical workspace for agent collaboration.

## 7. User Feedback Summary
*Data Unavailable.* Due to zero comments and zero new issues in the last 24 hours, there is insufficient data to generate a summary of user pain points, satisfaction levels, or specific use cases for this period.

## 8. Backlog Watch
With 0 active issues in the tracker, the current backlog is clear. However, two open Pull Requests require attention to prevent stagnation:
*   **PR [#242](https://github.com/TinyAGI/tinyagi/pull/242):** A complex refactor that needs code review to ensure the new adapter pattern is correctly implemented before merge.
*   **PR [#212](https://github.com/TinyAGI/tinyagi/pull/212):** A feature update that has been open since March 13th; recent updates suggest it is nearing completion but requires final review and testing.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Project Digest: Moltis (2026-03-20)

## 1. Today's Overview
Moltis has displayed moderate activity in the last 24 hours with no new releases published. The project saw an equal split of activity between Issues and Pull Requests (4 and 3 respectively), with all items remaining open, indicating an active development cycle currently focused on review and implementation. Key themes for the day include platform stability (Windows compatibility), repository governance (preventing agent hook bypasses), and ecosystem expansion (adding Novita AI). The lack of merged PRs suggests code is currently undergoing integration review or testing.

## 2. Releases
*No new releases published on 2026-03-20.*

## 3. Project Progress
While no Pull Requests were merged in the last 24 hours, significant feature development and maintenance work is currently in review:

*   **Windows Session Stability:** PR [#436](https://github.com/moltis-org/moltis/pull/436) addresses a critical file-locking bug (`LockFileEx os error 5`) specific to Windows. The author proposes replacing `append(true)` with `write(true)+seek` to properly handle file access permissions.
*   **Provider Expansion:** PR [#451](https://github.com/moltis-org/moltis/pull/451) works to add **Novita AI** as a new OpenAI-compatible provider, registering models like `deepseek-v3.2` and `glm-5`.
*   **Governance Controls:** PR [#455](https://github.com/moltis-org/moltis/pull/455) introduces a `block-no-verify` hook to prevent AI agents from bypassing local git quality gates (pre-commit/push hooks).

## 4. Community Hot Topics
*   **[Feature]: Tool search** ([#313](https://github.com/moltis-org/moltis/issues/313))
    *   **Activity:** 6 comments, 2 reactions.
    *   **Analysis:** This is the most discussed active thread. Users are expressing a need for better discoverability mechanisms within the agent's toolkit. The volume of comments suggests this is a high-priority quality-of-life improvement for users managing complex skill sets.

## 5. Bugs & Stability
*   **Skill Manifest Corruption** ([#452](https://github.com/moltis-org/moltis/issues/452))
    *   **Severity:** Medium-High.
    *   **Details:** A silent failure where skills with invalid names (but valid slugs) are unpacked into `installed-skills` but omitted from `skills-manifest.json`. This creates a "zombie" state where files exist but the system doesn't recognize them, likely confusing users expecting the skill to function.
*   **Windows File Locking** ([#436](https://github.com/moltis-org/moltis/pull/436))
    *   **Status:** Fix PR open.
    *   **Details:** Rust's `OpenOptions::append(true)` behavior on Windows strips necessary write permissions, causing crashes during session handling.

## 6. Feature Requests & Roadmap Signals
*   **Tool Search:** The continued activity on [#313](https://github.com/moltis-org/moltis/issues/313) strongly signals that improved tool discovery is a desired roadmap addition.
*   **Git Governance:** The rapid proposal of [#454](https://github.com/moltis-org/moltis/issues/454) and the associated PR [#455](https://github.com/moltis-org/moltis/pull/455) indicate a user demand for stricter control over autonomous agent actions, specifically regarding repository integrity.
*   **Multi-Agent Business Logic:** Issue [#453](https://github.com/moltis-org/moltis/issues/453) suggests users are attempting to scale Moltis for business use cases by having "managerial agents" spawn other agents, a capability that may require architectural support.

## 7. User Feedback Summary
*   **Pain Points:** Windows users are facing stability issues regarding file locks. Developers relying on git hooks are concerned about agents bypassing quality checks (e.g., `--no-verify`).
*   **Use Cases:** Users are integrating niche LLM providers (Novita AI) and attempting to build complex multi-agent hierarchies for business automation.
*   **Dissatisfaction:** There is frustration regarding "silent failures" in skill management (Issue #452), where unpacking succeeds but registration fails without clear error messages.

## 8. Backlog Watch
*   **Issue [#313](https://github.com/moltis-org/moltis/issues/313) (Tool Search):** Created on March 3rd and still open. With high engagement, this item risks stagnation without explicit maintainer assignment or roadmap placement.
*   **Issue [#453](https://github.com/moltis-org/moltis/issues/453) (Managerial Agents):** Newly opened, but addresses a complex architectural request. Requires clarification on whether Moltis natively supports "agent spawning" or if this requires user-space implementation.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest: 2026-03-20

## 1. Today's Overview
CoPaw is experiencing **extremely high development velocity** following the recent `v0.1.0` release, with 50 issues and 50 pull requests updated in the last 24 hours. The project appears to be in a stabilization phase, actively triaging a surge of user-reported bugs related to the new version, particularly concerning **upgrade failures** and **channel integrations** (Feishu/Lark, Telegram). Concurrently, the team is pushing forward with features like **"Agents Square"** and local embedding support. However, there are indicators of **regression instability**, with multiple users reporting deadlocks, upgrade blockers, and UI inconsistencies after migrating from `v0.0.7`.

## 2. Releases
**New Release: [v0.1.0](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0)**
*   **Multi-Agent / Multi-Workspace Architecture**: The flagship feature allows running multiple agents simultaneously, each with isolated workspaces, configs, and memory. Includes a console agent selector.
*   **Multimodal Support**: Added support for image and file uploads in the console.

**Recent Release: [v0.1.0-beta.4](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0-beta.4)**
*   **Fixes**: Resolved import issues for `create_local_chat_model` and console multimodal message handling.

**Migration Note**:
*   Users upgrading from `v0.0.7` to `v0.1.0` are facing significant friction. Reports indicate "space upgrade failures" and broken channel configurations (specifically Feishu/Lark authentication errors).

## 3. Project Progress
**Merged/Closed Advances (via PRs):**
*   **Architecture (v0.1.0)**: Successfully shipped the Multi-Agent architecture, enabling parallel task execution and isolated memory systems ([#13](https://github.com/agentscope-ai/CoPaw/issues/13)).
*   **Memory Management**: Improved tool result compaction configuration ([#1867](https://github.com/agentscope-ai/CoPaw/pull/1867)) and added timezone support for ReMe memory summarization ([#1814](https://github.com/agentscope-ai/CoPaw/pull/1814)).
*   **Resilience**: Added retry logic for HTTP 529 (Anthropic overloaded errors) ([#1891](https://github.com/agentscope-ai/CoPaw/pull/1891)).

**Active Development:**
*   **Agents Square**: Backend and UI routing for browsing and importing agent sources are being merged ([#1883](https://github.com/agentscope-ai/CoPaw/pull/1883)).
*   **Local Embeddings**: Support for local embedding models (BGE, Qwen3-VL) for long-term memory is in review ([#1789](https://github.com/agentscope-ai/CoPaw/pull/1789)).

## 4. Community Hot Topics
*   **Upgrade Failures (v0.1.0b3 -> v0.1.0)**
    *   **Issue**: [#1895](https://github.com/agentscope-ai/CoPaw/issues/1895)
    *   **Activity**: 5 comments
    *   **Analysis**: Users cannot upgrade their workspace environments. The prompt "Create space upgrade failed" suggests database migration or config serialization logic failed in the new release.
*   **Context Window & Model Errors (v0.1.0b3)**
    *   **Issue**: [#1873](https://github.com/agentscope-ai/CoPaw/issues/1873)
    *   **Activity**: 5 comments
    *   **Analysis**: A regression where the system incorrectly reports "context window exceeds limit (2013)" immediately after upgrade, blocking all chats.
*   **Tasks "Freezing" / Deadlocks**
    *   **Issue**: [#1827](https://github.com/agentscope-ai/CoPaw/issues/1827) (UI Freeze)
    *   **Issue**: [#1774](https://github.com/agentscope-ai/CoPaw/issues/1774) (CPU Loop)
    *   **Analysis**: Critical stability concerns. Users report agents hanging mid-task. One report identified an infinite loop in `ToolResultCompactor` causing 100% CPU usage.

## 5. Bugs & Stability
**Severity: High (Regressions & Crashes)**
1.  **System Deadlock / Event Loop Lockup**:
    *   **Issue**: [#1834](https://github.com/agentscope-ai/CoPaw/issues/1834)
    *   **Root Cause**: `TokenUsageManager.record()` uses `threading.Lock` inside an async method, blocking the entire event loop under load.
    *   **Fix**: PR [#1893](https://github.com/agentscope-ai/CoPaw/pull/1893) proposes replacing it with `asyncio.Lock`.
2.  **Upgrade Blocker (v0.1.0)**:
    *   **Issue**: [#1895](https://github.com/agentscope-ai/CoPaw/issues/1895)
    *   **Impact**: Users unable to use the latest version.
3.  **Feishu/Lark Auth Failure**:
    *   **Issue**: [#1786](https://github.com/agentscope-ai/CoPaw/issues/1786)
    *   **Error**: `AuthenticationError: Please carry the API secret key...`
    *   **Context**: Env vars seem ignored after upgrade to v0.1.0b2/b3.

**Severity: Medium (Feature breakage)**
4.  **Telegram Audio Missing**:
    *   **Issue**: [#1516](https://github.com/agentscope-ai/CoPaw/issues/1516)
    *   **Fix**: PR [#1896](https://github.com/agentscope-ai/CoPaw/pull/1896) addresses the `data` vs `source` field mismatch.
5.  **Double Agent Output**:
    *   **Issue**: [#1892](https://github.com/agentscope-ai/CoPaw/issues/1892)
    *   **Symptom**: Model returns the response text twice (observed with Qwen GGUF models).

## 6. Feature Requests & Roadmap Signals
*   **QQ Direct Message (DM) Support**: High demand for processing DMs in QQ channels, as sandbox restrictions limit standard chat usage ([#1641](https://github.com/agentscope-ai/CoPaw/issues/1641)).
*   **HTTP-based MCP**: Users want to connect to MCP servers via HTTP, not just stdio, with proper header expansion ([#676](https://github.com/agentscope-ai/CoPaw/issues/676), [#1585](https://github.com/agentscope-ai/CoPaw/issues/1585)).
*   **Routing Logic**: Request for "Channel Routing" to dispatch messages to different agents based on rules (PR [#1889](https://github.com/agentscope-ai/CoPaw/pull/1889) is currently open).

## 7. User Feedback Summary
*   **Frustration with Stability**: Comments in [#1846](https://github.com/agentscope-ai/CoPaw/issues/1846) ("Is this project dead? No updates for a week") highlight user anxiety, though the high volume of recent commits disproves this.
*   **Performance Concerns**: Windows users using Ollama report very slow response times ([#1808](https://github.com/agentscope-ai/CoPaw/issues/1808)).
*   **Upgrade Pain**: The "silent failure" nature of some upgrades (e.g., web UI prompts update, but pip sees old version) is confusing users ([#1866](https://github.com/agentscope-ai/CoPaw/issues/1866)).

## 8. Backlog Watch
*   **Swagger/API Docs**: PR [#1847](https://github.com/agentscope-ai/CoPaw/pull/1847) attempts to fix Swagger docs being blocked by SPA routing, a developer experience issue.
*   **Audio Compatibility**: Discord (`.ogg`) and Telegram audio handling remain partially broken or in need of patches ([#902](https://github.com/agentscope-ai/CoPaw/issues/902), [#1516](https://github.com/agentscope-ai/CoPaw/issues/1516)).

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# Project Digest: ZeptoClaw
**Date:** 2026-03-20
**Status:** Active Development

### 1. Today's Overview
ZeptoClaw is currently in a high-development phase with no releases published in the immediate cycle, indicating that the team is focusing on merging significant underlying features rather than stabilization. Activity levels are robust, with 3 Pull Requests updated in the last 24 hours alongside active bug tracking. The project is expanding its ecosystem integrations (adding new AI providers) while simultaneously refining its core Agent Client Protocol (ACP) implementation, which appears to be the current focal point for the engineering team.

### 2. Releases
**No new releases published in this period.**

### 3. Project Progress
While no Pull Requests were fully merged in the last 24 hours, significant progress is evident on three major fronts:
*   **ACP Implementation:** Substantial work continues on [#356 (ACP stdio + HTTP)](https://github.com/qhkm/zeptoclaw/pull/356), which aims to provide standard input/output and HTTP channels for the Agent Client Protocol. This is critical for enabling ZeptoClaw to function as a subprocess for other tools.
*   **Provider Expansion:** The ecosystem is growing via [#390 (Novita AI)](https://github.com/qhkm/zeptoclaw/pull/390), which adds support for the Novita AI API, enhancing the range of available LLM backends.
*   **Developer Experience:** Infrastructure improvements are ongoing in [#287 (Dev Tools)](https://github.com/qhkm/zeptoclaw/pull/287), focusing on standardizing the local development and pre-PR testing environment.

### 4. Community Hot Topics
*   **[Issue #388: ACP HTTP Initialization & Semantics](https://github.com/qhkm/zeptoclaw/issues/388)**
    *   **Status:** Open
    *   **Analysis:** This is the primary topic of discussion, directly linked to the ongoing ACP implementation. The community/maintainers are identifying critical protocol flaws where HTTP notifications are incorrectly receiving response bodies and initialization flags are shared globally across clients rather than being session-specific. This suggests a high demand for robust multi-agent or multi-client session management.

### 5. Bugs & Stability
*   **[Critical: Protocol Logic Error in ACP HTTP](https://github.com/qhkm/zeptoclaw/issues/388)**
    *   **Description:** The `initialize` handshake is stored as a global flag. This creates a race condition where once one client initializes, subsequent clients can skip the handshake entirely, leading to potential security risks and undefined behavior in session management.
    *   **Fix Status:** A fix is actively being worked on within the context of PR [#356](https://github.com/qhkm/zeptoclaw/pull/356).

### 6. Feature Requests & Roadmap Signals
*   **Novita AI Provider:** The submission of PR [#390](https://github.com/qhkm/zeptoclaw/pull/390) indicates a user/maintainer desire to support a wider variety of OpenAI-compatible endpoints, specifically Novita AI.
*   **Standardized Development Tooling:** PR [#287](https://github.com/qhkm/zeptoclaw/pull/287) signals a roadmap focus on improving contributor velocity and reducing integration issues by enforcing consistent pre-PR testing states (`cargo test`, `cargo clippy`).

### 7. User Feedback Summary
Feedback currently derives from technical implementation details:
*   **Protocol Correctness:** Users are stress-testing the new ACP channels, finding that the HTTP implementation does not strictly adhere to expected session semantics (global vs. local state).
*   **Environment Consistency:** There is an implicit request for better tooling to ensure code quality (linting/tests) before code enters the review queue.

### 8. Backlog Watch
*   **[PR #287: Dev tools for consistent pre-PR state](https://github.com/qhkm/zeptoclaw/pull/287)**
    *   **Created:** March 9
    *   **Note:** This PR has been open for nearly two weeks but was updated recently. It is crucial for long-term project health and maintainability, ensuring that all contributors run the same checks before submitting code.

---
*Data sourced from GitHub public activity logs for `qhkm/zeptoclaw`.*

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw (RivonClaw) Project Digest
**Date:** 2026-03-20

## 1. Today's Overview
EasyClaw (operating under the RivonClaw moniker for releases) is undergoing a significant architectural evolution focused on UI modernization and user experience refinement. The project exhibited high activity today with **3 major Pull Requests merged** and **2 new releases** (v1.7.3 and v1.7.2) published, indicating a push to stabilize a new feature branch. The repository is transitioning from core functionality to a more polished, productized state, with heavy emphasis on authentication flows and component reusability. While maintenance is active, user engagement in the issues section remains low, suggesting the project is in a transitional phase between major updates.

## 2. Releases
The project released two versions in rapid succession to address installation friction and introduce major UI improvements.

*   **[v1.7.3: RivonClaw v1.7.3](https://github.com/gaoyangz77/easyclaw/releases)**
    *   **Focus:** Stability and User Access.
    *   **Key Note:** This release specifically addresses macOS Gatekeeper issues. Users facing "'RivonClaw' is damaged and can't be opened" errors are provided with terminal commands to bypass the security restriction for unsigned apps.
*   **[v1.7.2: RivonClaw v1.7.2](https://github.com/gaoyangz77/easyclaw/releases)**
    *   **Major Changes:**
        *   **UI Overhaul:** Complete component refactor, separation of themes, and a redesigned "Skills" page.
        *   **Authentication:** Introduced captcha-based authentication and a centralized settings system.
        *   **Configuration:** Added SQLite-backed account configuration and a "channel group-allow-from" editor.
        *   **SDK:** Refactored Plugin SDK with internationalization support.
    *   **Migration Note:** Users should expect significant visual changes and new authentication prompts.

## 3. Project Progress
The development team focused heavily on closing the gap on UI refactoring, successfully merging three distinct PRs to overhaul the user interface and authentication experience.

*   **[PR #24: Account UI redesign popover](https://github.com/gaoyangz77/easyclaw/pull/24)** (Closed by @chinayin)
    *   **Advancement:** Replaced the standalone `/account` navigation page with a dynamic popover dropdown triggered by the avatar.
    *   **Details:** Implemented distinct views for logged-in (avatar, email, plan) and logged-out (welcome/login) states, matching the application's existing dark mode theme.
*   **[PR #23: Redesign auth modal & account page](https://github.com/gaoyangz77/easyclaw/pull/23)** (Closed by @chinayin)
    *   **Advancement:** Modernized the login and registration flow.
    *   **Details:** Added pill-shaped tab switchers, password visibility toggles, password strength bars, and compact captcha rows. The account page now uses a split-card layout for consistency.
*   **[PR #20: Component Refactor + Theme Separation](https://github.com/gaoyangz77/easyclaw/pull/20)** (Closed by @chinayin)
    *   **Advancement:** Technical debt reduction and standardization.
    *   **Details:** Extracted sidebar actions into `<BottomActions>`, consolidated all inline SVGs into a centralized `icons.tsx` utility, and updated theme usage to rely on CSS variables (via `themeColors`).

## 4. Community Hot Topics
Community interaction is currently centered around clarifying project scope and seeking technical connection channels.

*   **[#22: "Multi-browser" functionality clarification](https://github.com/gaoyangz77/easyclaw/issues/22)**
    *   **Topic:** A user questioned whether the "multi-browser" feature refers to multi-user support or cross-platform consistency, and asked for details on the impact of logging in vs. remaining logged out.
    *   **Analysis:** This indicates potential confusion regarding the app's value proposition. Users are trying to determine if this is a personal automation tool or a multi-user platform. The lack of answers suggests the maintainer is prioritizing code refactoring over documentation currently.
*   **[#12: Request for Community Group](https://github.com/gaoyangz77/easyclaw/issues/12)** (Closed)
    *   **Topic:** A user requested a technical exchange group, citing the project's architecture as highly aligned with their expectations.
    *   **Analysis:** While closed, this highlights strong user interest in the underlying architecture. High appreciation for the codebase suggests that once the UI refactor stabilizes, the project could see increased contributor interest.

## 5. Bugs & Stability
*   **Installation Blocker (macOS):** Users on macOS are prevented from opening the application due to Gatekeeper blocking the unsigned binary (Error: "'RivonClaw' is damaged").
    *   **Severity:** Medium (Workaround available).
    *   **Status:** addressed in v1.7.3 release notes with manual terminal instructions.
*   **No Open Critical Bugs:** No critical crashes or regressions were reported in the open issues tracker in the last 24h.

## 6. Feature Requests & Roadmap Signals
*   **Authentication Clarification:** The questions in [#22](https://github.com/gaoyangz77/easyclaw/issues/22) signal a need for better documentation explaining the benefits of the "Login" vs. "No Login" states introduced in v1.7.2.
*   **Community Infrastructure:** The request in [#12](https://github.com/gaoyangz77/easyclaw/issues/12) suggests a roadmap need for official communication channels (Discord/WeChat) to facilitate technical discussion.

## 7. User Feedback Summary
*   **Positive:** Users are highly impressed with the project's architecture ("架构非常符合我预期的架构"), indicating strong technical approval.
*   **Neutral/Confused:** There is uncertainty about specific feature definitions ("Multi-browser") and the new account system.
*   **Pain Points:** The primary friction point is platform-specific (macOS installation warnings), which disrupts the out-of-the-box experience.

## 8. Backlog Watch
*   **Issue #22:** Requires a maintainer response to clarify feature scope. Without this, user adoption may be hindered by misunderstanding.
*   **Documentation:** The "ReadMe" or "Docs" likely need updating to reflect the new Auth modal and Account page changes introduced in today's PRs, as users are already asking about how login affects functionality.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*