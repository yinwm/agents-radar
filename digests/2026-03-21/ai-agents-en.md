# OpenClaw Ecosystem Digest 2026-03-21

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-03-21 01:14 UTC

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

# OpenClaw Project Digest: 2026-03-21

## 1. Today's Overview
OpenClaw is experiencing an extremely high-volume development cycle, with **500 issues and 500 pull requests updated in the last 24 hours**. While no new release was published today, the project is rapidly iterating on the `v2026.3.x` branch, focusing heavily on stabilizing connectivity (gateways, WebSocket, and mobile pairing) and resolving critical regressions introduced in recent versions. The community is highly engaged, though stability concerns regarding recent updates (v2026.3.8 - v2026.3.13) are dominating the conversation.

## 2. Releases
**Status:** No new releases published today.
*   **Current Context:** Development is concentrated on the `v2026.3.x` series. Users are encouraged to track the `main` branch for fixes regarding gateway heartbeats, CLI timeouts, and mobile pairing stability.

## 3. Project Progress
**Merged/Closed Highlights:**
*   **Core Stability:** Multiple workflow and process management improvements were merged, including fixes for Docker builds post-extension migration (`#48523`) and a CLI "doctor" command that now exits with code 1 on critical errors (`#10578`).
*   **Channel Improvements:** A fix for WhatsApp Web listener mismatches (`#47427`) and immediate hotfixes for Ollama tool call recovery (`#51094`) and WhatsApp listener maps (`#51101`) were closed.
*   **Feature Advancements:**
    *   **iOS Pairing:** Significant enhancements to the iOS QR pairing flow (`#51340`) have been merged, improving onboarding security.
    *   **Plugin SDK:** A new `before_message_process` hook (`#50366`) was merged, allowing plugins to intercept and route messages before agent processing.
    *   **Dynamic Model Resolution:** GitHub Copilot extension can now dynamically resolve any model ID (`#51325`), and OpenAI Codex model resolution was fixed (`#49512`).

## 4. Community Hot Topics
*   **Internationalization (i18n) Debate** ([#3460](https://github.com/openclaw/openclaw/issues/3460) - 106 comments)
    *   **Summary:** The most discussed issue remains the official stance on internationalization. The maintainers stated they lack the bandwidth to support multiple languages, but the community continues to push for it, submitting numerous PRs.
    *   **Underlying Need:** A strong desire to make OpenClaw accessible to non-English speaking users despite maintainer resource constraints.
*   **ClawHub & Community Skills** ([#50090](https://github.com/openclaw/openclaw/issues/50090) - 7 comments)
    *   **Summary:** Users are highlighting the gap between the promise of a "ClawHub" ecosystem for sharing skills and the reality of the current implementation.
    *   **Underlying Need:** A more streamlined, functional way to discover and install community-created agent capabilities.

## 5. Bugs & Stability
**Critical Regressions & Crashes:**
1.  **Gateway Heartbeat Failure** ([#45772](https://github.com/openclaw/openclaw/issues/45772) - 20 comments)
    *   **Severity:** High.
    *   **Issue:** Gateway heartbeat timer stops after 1-2 triggers, introduced in `v2026.3.8`. This causes agents to permanently stop responding.
2.  **WebSocket/CLI Timeouts** ([#47265](https://github.com/openclaw/openclaw/issues/47265) - 8 comments, [#46892](https://github.com/openclaw/openclaw/issues/46892) - 10 comments)
    *   **Severity:** High.
    *   **Issue:** `v2026.3.13` broke CLI WebSocket connections with "gateway closed (1000)" errors. A 3-second handshake timeout is also causing spurious disconnects on busy event loops.
    *   **Fix PR:** [#51348](https://github.com/openclaw/openclaw/pull/51348) attempts to fix model overrides that block restarts.
3.  **macOS Gateway "Never Ready"** ([#6156](https://github.com/openclaw/openclaw/issues/6156) - 15 comments)
    *   **Severity:** High.
    *   **Issue:** Users on macOS cannot complete the Setup Wizard; the gateway never reports readiness.
4.  **Slack Socket Mode Regression** ([#45311](https://github.com/openclaw/openclaw/issues/45311) - 8 comments)
    *   **Severity:** Medium.
    *   **Issue:** `v2026.3.12` broke Slack inbound event delivery despite successful socket connection.
5.  **Auth Failures** ([#23538](https://github.com/openclaw/openclaw/issues/23538) - 23 comments, [#49191](https://github.com/openclaw/openclaw/issues/49191) - 13 comments)
    *   **Issue:** Anthropic setup-token and Google Vertex ADC authentication are failing with 401 errors due to improper token handling (e.g., sending `"<authenticated>"` as a literal string).

## 6. Feature Requests & Roadmap Signals
*   **External Memory Provider API** ([#49233](https://github.com/openclaw/openclaw/issues/49233) - 10 comments)
    *   **Signal:** Users want to eliminate the 30-60s agent blackout during context compaction by delegating memory to an external system.
*   **Thinking Config per Agent** ([#21097](https://github.com/openclaw/openclaw/issues/21097) - 5 comments)
    *   **Signal:** Request to support `thinkingDefault` in individual `agents.list` entries rather than globally, allowing cost optimization (e.g., high thinking for complex agents, low for simple ones).
*   **Extensible Web Search** ([#11399](https://github.com/openclaw/openclaw/issues/11399) - 6 comments)
    *   **Signal:** With Brave Search API no longer free, users want plugin-based extensibility to add Tavily or other search providers.

## 7. User Feedback Summary
*   **Frustration with Stability:** The `v2026.3.x` cycle is causing fatigue. Multiple users report that upgrading breaks previously working features (WebSocket CLI, Slack, macOS Gateway), forcing rollbacks to `v2026.3.8` or earlier.
*   **Quality of Life Pain Points:**
    *   **Text Leaks:** Internal processing text between tool calls is leaking into public channels (Slack/iMessage), exposing internal errors to end-users ([#25592](https://github.com/openclaw/openclaw/issues/25592)).
    *   **UI Regressions:** Visual bugs, such as the context limit warning icon covering the chat view ([#44906](https://github.com/openclaw/openclaw/issues/44906)), are blocking usage.
    *   **Docker/Dockerless friction:** Users struggle with `nvm`-installed nodes missing TLS certs ([#49088](https://github.com/openclaw/openclaw/issues/49088)) and Docker builds failing due to missing dependencies ([#48797](https://github.com/openclaw/openclaw/issues/48797)).

## 8. Backlog Watch
*   **Stale OAuth/Bug Issues:** Several high-impact bugs remain open for weeks/months, including Signal daemon race conditions ([#22676](https://github.com/openclaw/openclaw/issues/22676)), Gemini infinite polling loops ([#15738](https://github.com/openclaw/openclaw/issues/15738)), and Google Chat webhook failures ([#22362](https://github.com/openclaw/openclaw/issues/22362)).
*   **Context Corruption:** A critical issue where context corruption exposes raw API errors to the chat surface ([#11038](https://github.com/openclaw/openclaw/issues/11038)) remains unresolved.
*   **Auth Race Conditions:** OAuth token refresh race conditions causing failovers ([#26322](https://github.com/openclaw/openclaw/issues/26322)) need attention.

---

## Cross-Ecosystem Comparison

**Ecosystem Intelligence Report: AI Agent & Assistant Landscape**
**Date:** March 21, 2026

### 1. Ecosystem Overview
The open-source AI agent ecosystem is undergoing a phase of **hyper-fragmentation and specialization**, moving away from monolithic "do-everything" architectures toward distinct verticals (e.g., security-focused, enterprise-integrated, or lightweight local-first). **Stability remains the primary bottleneck** across the landscape; high-velocity development cycles are universally causing regressions, particularly in WebSocket connectivity, memory management, and provider integrations. There is a clear industry shift toward **multi-agent workflows** and **persistent memory systems (RAG/Graph)**, moving beyond simple stateless chat interfaces.

### 2. Activity Comparison

| Project | 24h Issues | 24h PRs | Release Status | Health Score* |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | No Release (Stabilizing) | B (High Friction) |
| **LobsterAI** | 35 | 26 | v2026.3.20 | C (Critical Bugs) |
| **ZeroClaw** | 50 | 50 | v0.5.4 (Multiple) | C+ (High Instability) |
| **PicoClaw** | 23 | 61 | Nightly Build | B+ (Active) |
| **NanoBot** | 38 | 69 | Rolling/Nightly | A- (High Velocity) |
| **IronClaw** | 41 | 50 | v0.21.0 | C (Migration Issues) |
| **CoPaw** | 50 | 50 | v0.1.0.post1 | C (Upgrade Pain) |
| **NanoClaw** | 7 | 25 | No Release | B (Feature Sprint) |
| **NullClaw** | 0 | 24 | No Release | A (Stable/Enterprise) |
| **Moltis** | 3 | 4 | No Release | B+ (Refining) |
| **TinyClaw** | 0 | 4 | v0.0.16 | A (Streamlining) |
| **ZeptoClaw** | 2 | 0 | No Release | B (Architecting) |
| **EasyClaw** | 1 | 0 | v1.7.3 | C (Reactive) |

*\*Health Score based on ratio of feature development vs. critical bug reports and community sentiment.*

### 3. OpenClaw's Position
**Advantages:** OpenClaw remains the undisputed leader in **community scale** and **integration breadth** (WhatsApp, Slack, iOS, mobile pairing). Its plugin ecosystem and `before_message_process` hooks allow for extensibility that peers lack.
**Disadvantages vs. Peers:**
*   **Technical Debt:** Unlike the more modern Rust-based **NanoBot** or the streamlined **TinyClaw**, OpenClaw struggles with legacy Node.js stability issues (Docker, CLI timeouts).
*   **Iteration Speed:** OpenClaw's 500 daily issues indicate a support-heavy maintenance mode, whereas **ZeroClaw** and **LobsterAI** are shipping features (Memory Graphs, Personas) at a faster pace.
*   **Community Sentiment:** There is notable fatigue regarding OpenClaw's `v2026.3.x` regressions compared to the relative stability of **NullClaw** or the "fresh start" appeal of **NanoBot**.

### 4. Shared Technical Focus Areas
*   **Persistent Memory (The "Graph" Shift):**
    *   **ZeroClaw** & **NanoClaw** are racing to integrate `mem0` (GraphRAG/Neo4j) to solve context window limits.
    *   **OpenClaw** is seeing requests for "External Memory Provider APIs" to bypass internal blackouts.
*   **Multi-Agent Orchestration:**
    *   **NanoClaw** (Agent-to-Agent comms), **CoPaw** (Agents Square), and **IronClaw** (ACP Support) are all building infrastructure for agents to delegate tasks to other specialized agents.
*   **Enterprise/Asian Market Integration:**
    *   **NullClaw**, **PicoClaw**, and **LobsterAI** are heavily prioritizing WeCom, DingTalk, Lark (Feishu), and QQ integration, signaling that the "ChatOps" battle is moving to Asian enterprise platforms.
*   **Observability & Cost Tracking:**
    *   **NanoClaw** (API usage tracking), **IronClaw** (Debug Inspector), and **LobsterAI** (Token stats) reflect a user demand for "OpenTelemetry for Agents" to manage skyrocketing LLM costs.

### 5. Differentiation Analysis
*   **Security vs. Usability:** **ZeroClaw** is betting on "Safe by Default" (autonomy levels, strict safety policies), which is causing user friction. In contrast, **PicoClaw** and **NanoBot** prioritize "hackability" and ease of integration, accepting higher risk for greater flexibility.
*   **Architecture Shifts:**
    *   **NanoBot** is rewriting its core in Rust (`nanobot-rs`) for performance.
    *   **TinyClaw** is pursuing a "Zero-Config" philosophy to lower the barrier to entry.
    *   **IronClaw** is focusing on a "Design-First" approach with heavy UX/UI overhaul (Glassmorphism).
*   **Target User:**
    *   *Personal/Tinkerer:* **TinyClaw**, **EasyClaw**.
    *   *Enterprise/Prosumer:* **OpenClaw**, **NullClaw**, **LobsterAI**.
    *   *Infrastructure/Devs:* **IronClaw**, **Moltis**.

### 6. Community Momentum & Maturity
*   **Rapidly Iterating (High Volatility):** **ZeroClaw** and **LobsterAI** are shipping features daily but suffering from "update fatigue" and critical stability bugs (crashes, hallucinations).
*   **Stabilizing/Enterprise-Ready:** **NullClaw** stands out today for closing 24 PRs focused on reliability (SSE stalls, legacy compat) without introducing critical regressions. **TinyClaw** also scores well for removing setup friction.
*   **Stressed/At Risk:** **OpenClaw** and **IronClaw** are facing "Population Crises"—their user bases are growing faster than their ability to stabilize the codebase, leading to massive issue backlogs (500+ for OpenClaw).

### 7. Trend Signals for Developers
1.  **The "Reasoning" Model Bottleneck:** Projects like **NullClaw** (Moonshot) and **IronClaw** are scrambling to adapt to new "reasoning_content" fields in LLM APIs. *Agent developers must standardize parsing for these new deep-thinking models.*
2.  **Voice is the Frontier:** **PicoClaw** and **ZeroClaw** are seeing massive upvotes for TTS/ASR issues. *Text-only agents are becoming obsolete; voice modalities are a required differentiator.*
3.  **The "Local-First" Demand:** **NanoBot** and **PicoClaw** issues show users aggressively trying to run agents on Ollama/LM Studio to avoid API costs and surveillance. *Support for local inference is no longer optional.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest: 2026-03-21

## 1. Today's Overview
The project is demonstrating exceptional growth velocity with **69 Pull Requests** and **38 Issues** updated in the last 24 hours, indicating a highly active development phase. While no formal release was published today, a significant number of merged PRs (32) suggest a potential "rolling release" or `nightly` update cycle is in progress. The community is highly engaged, with robust discussion around configuration complexity, multi-modal capabilities, and stability improvements for local LLMs.

## 2. Releases
No new official releases were published today.

## 3. Project Progress
Significant features were advanced via merged PRs, focusing on infrastructure, language expansion, and tooling:

*   **New Language & Architecture (PR #2313):** A Rust MVP (`nanobot-rs`) was merged, introducing a Rust-based crate with CLI, provider, and agent loop implementations. This marks a major step towards performance and memory safety improvements.
*   **Documentation & Onboarding (PR #2310):** Improvements to the onboarding wizard, specifically removing redundant GitHub Copilot OAuth configurations to streamline user setup.
*   **Channel Enhancements (PR #2306):** Implemented base64 media uploads for QQ and WeCom channels. This removes the dependency on public URLs/IPs for file delivery, improving security and deployment flexibility.
*   **Cron & Execution (PR #2311):** Implemented `system_event` execution for cron jobs, allowing shell commands to run directly without invoking the full agent loop (useful for maintenance tasks).

## 4. Community Hot Topics
The community is focused heavily on usability and integration depth.

*   **[Enhancement] nanobot-webui (Issue #1922):**
    *   **Status:** Open | 👍 6
    *   **Discussion:** User @Good0007 introduced a self-hosted web management panel.
    *   **Analysis:** There is a clear demand for a GUI to manage the complexity of the JSON config, manage MCP servers, and view chat history. This is currently the most upvoted non-bug item.
    *   [Link to Discussion](https://github.com/HKUDS/nanobot/issues/1922)

*   **[Feature] Feishu/Lark Thread Support (PR #2307 & Issue #2256):**
    *   **Status:** Open PR
    *   **Discussion:** Users (@A11Might) requested that the bot reply within the specific thread in topic groups rather than the general channel.
    *   **Analysis:** Critical for enterprise adoption where Lark/Feishu topic groups are used for project management. A PR is currently pending review.
    *   [Link to Issue](https://github.com/HKUDS/nanobot/issues/2256) | [Link to PR](https://github.com/HKUDS/nanobot/pull/2307)

*   **[Enhancement] WhatsApp "Message Self" Support (Issue #218):**
    *   **Status:** Closed (Implemented)
    *   **Discussion:** Users wanted to test the bot by sending messages to themselves on WhatsApp, which was previously filtered out.
    *   **Analysis:** Highlights the need for better testing workflows and personal assistant use cases.
    *   [Link to Issue](https://github.com/HKUDS/nanobot/issues/218)

## 5. Bugs & Stability
Stability concerns are primarily related to specific provider integrations and output handling.

*   **[Regression] Gemini-3-Flash-Preview (Issue #2185):**
    *   **Severity:** High
    *   **Details:** Upgrading from `0.1.4` to `0.1.4post5` breaks usage of `gemini-3-flash-preview`.
    *   **Analysis:** A regression was likely introduced in recent changes to provider handling or tool calling logic. [Link](https://github.com/HKUDS/nanobot/issues/2185)

*   **[Bug] Telegram Double Responses (Issue #2235):**
    *   **Severity:** Medium
    *   **Details:** Telegram users see replies twice (often one disappears).
    *   **Analysis:** Identified as a likely issue with the "faux streaming" implementation. Affects perceived polish of the interaction. [Link](https://github.com/HKUDS/nanobot/issues/2235)

*   **[Bug] WeCom Restart Port Error (PR #2308):**
    *   **Severity:** Medium
    *   **Fix:** Merged PR to add `SO_REUSEPORT` support to the WeCom Flask server to prevent "Address already in use" errors on restart. [Link](https://github.com/HKUDS/nanobot/pull/2308)

## 6. Feature Requests & Roadmap Signals
Users are pushing for better observability and standardization.

*   **LLM Trace Observability (Issue #2154):**
    *   **Request:** Users want a standardized way (interface/API) to trace LLM execution paths for debugging, rather than modifying internal code.
    *   **Prediction:** Likely to be addressed in upcoming nightly builds as the focus on "enterprise-readiness" grows.

*   **Agent Evaluation Harness (PR #2283):**
    *   **Request:** A deterministic framework for evaluating agent task completion without making live API calls.
    *   **Status:** PR is Open. This signals a move towards standardizing benchmarking for the agent.

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Configuration Complexity:** Users struggle with manually editing `~/.nanobot/config.json` (spawning the webui project).
    *   **Local Model Reliability:** Users report "hallucinations" and infinite loops (Issue #2298) when using smaller local models (Qwen2.5, Ollama), requesting logic to break repetitive tool loops.
    *   **Provider Setup:** Authentication errors with DashScope, Z.ai, and local vLLM remain common hurdles for new users.
*   **Positive Feedback:** The new interactive `nanobot onboard` wizard (Issue #2018/2019) is receiving positive feedback for simplifying the initial setup.

## 8. Backlog Watch
*   **DingTalk Identity (Issue #1418):** Open since March 2, regarding the agent's inability to see sender names (only staffId). This is a persistent UX gap for enterprise users.
*   **DingTalk File Support (Issue #1864):** Open since March 11, regarding the inability to handle file uploads from the user side.
*   **ContextVars for Tool Routing (Issue #2220):** An architectural proposal to use `ContextVar` for task-local tool routing. This needs maintainer review to approve the direction for async-safety hardening.

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Project Digest: ZeroClaw (2026-03-21)

## 1. Today's Overview
ZeroClaw is experiencing a period of **extremely high development velocity** and friction. The project is pushing significant updates across memory (`mem0`), channels (Slack, QQ, Lark), and tooling, evidenced by 10 new releases in a single day. However, the rapid iteration is causing instability: 50 issues and 50 PRs were updated in the last 24 hours, with user reports indicating regressions, severe hallucinations, and tool execution failures. The community is vocal about the balance between security and usability, with a strong demand for better documentation and feature parity checks.

## 2. Releases
Multiple releases were published today, focusing on platform expansion and tooling enhancements.
*   **v0.5.4 (Stable):**
    *   **Enhancements:** Added `Avian` as an OpenAI-compatible provider; enhanced the QQ channel with rich media and cron delivery; expanded Jira tools with `myself` and `list_projects` actions.
    *   **Migration:** No specific breaking changes noted, but users integrating Avian or QQ should verify the new configs.
*   **v0.5.4-beta.487:**
    *   **New Features:** Integrated `mem0` (OpenMemory) as a backend for persistent memory.
    *   **Channels:** Implemented reaction support for Slack.
    *   **Tools:** Added alias fallbacks for `web_search` providers and a native "verifiable intent" lifecycle module.
*   **v0.5.2 (Stable):**
    *   **UX/Channels:** Added a `/stop` command to cancel in-flight tasks across Discord, Mattermost, and Telegram. Implemented TTS voice replies for Telegram.
    *   **Security:** Began injecting security policy summaries into agent prompts.
*   **Hardware Support:** Recent builds (v0.5.2+) added ARM cross-compilation targets (armv7) and ARM64 fixes for Raspberry Pi users.

## 3. Project Progress
*   **Advanced Features:**
    *   **Memory Architecture:** The project is aggressively moving towards persistent memory with the integration of the `mem0` backend (#3965 merged).
    *   **Multimodal & Vision:** A fix for Gemini was merged to restore prompt-guided tool calling and add vision support (#3932).
    *   **Provider Expansion:** Support for Bailian (Aliyun), DeepMyst, and local Whisper transcription (STT) is actively being developed.
*   **Fixes Merged:**
    *   Fixed QQ channel connectivity by handling WebSocket Ping frames (#4041).
    *   Fixed `web_search` provider routing to allow alias fallbacks (#4038).
    *   Corrected the SafetySection in the prompt builder to respect `autonomy.level = "full"` (#4037), preventing the agent from asking for permission unnecessarily in high-autonomy modes.

## 4. Community Hot Topics
*   **[#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478) - "Security overrides everything" (👍 6, 43 comments)**
    *   *Summary:* Users are frustrated that the strict security policy prevents basic operations (like installing ffmpeg) even when permissions are seemingly opened up.
    *   *Analysis:* This highlights a critical UX gap between the intent of the "Safety" system and the user's expectation of control. Users feel they are fighting the configuration rather than the bot doing the work.
*   **[#3882](https://github.com/zeroclaw-labs/zeroclaw/issues/3882) - Support for Aliyun Coding Plan (9 comments)**
    *   *Summary:* Request to support Aliyun's specific "Coding Plan" model, which currently returns 405 errors.
    *   *Analysis:* Indicates strong demand in the Chinese market for specialized coding models via ZeroClaw.
*   **[#3540](https://github.com/zeroclaw-labs/zeroclaw/issues/3540) - Feishu/Lark Channel Broken (8 comments)**
    *   *Summary:* Compiling with `channel-lark` feature results in startup failures.
    *   *Analysis:* Rapid development is breaking core channel integrations. A PR (#3866) was just opened to fix Feishu markdown card support, indicating active maintenance but also instability.

## 5. Bugs & Stability
*   **Severe (S0/S1) Issues:**
    *   **Hallucinations & Loops:** Issue [#3982](https://github.com/zeroclaw-labs/zeroclaw/issues/3982) reports severe hallucinations where the agent invents command output. Issue [#4039](https://github.com/zeroclaw-labs/zeroclaw/pull/4039) (Open PR) aims to fix "repeated tool result loops."
    *   **Crashes on ARM64:** Issue [#3537](https://github.com/zeroclaw-labs/zeroclaw/issues/3537) notes silent daemon crashes on Raspberry Pi 4 (S0). Newer ARM targets were added in CI, but the runtime stability is still in question.
    *   **MCP Tool Discovery:** Issue [#4042](https://github.com/zeroclaw-labs/zeroclaw/issues/4042) reports that agents cannot find MCP servers/tools. A fix is in PR [#4096](https://github.com/zeroclaw-labs/zeroclaw/pull/4096).
    *   **Text Truncation Panic:** Issue [#4062](https://github.com/zeroclaw-labs/zeroclaw/issues/4062) details a hard panic when truncating multi-byte (CJK) tool arguments (S3).
*   **Regressions:**
    *   Issue [#4093](https://github.com/zeroclaw-labs/zeroclaw/issues/4093) highlights that "Provider streaming" work was stranded on a deleted `dev` branch and never reached `master`, causing feature loss.

## 6. Feature Requests & Roadmap Signals
*   **Token Efficiency:** Issue [#3892](https://github.com/zeroclaw-labs/zeroclaw/issues/3892) requests an analyzer layer to reduce context bloat, crucial for local LLM users with smaller context windows.
*   **Declarative Config:** Issue [#4045](https://github.com/zeroclaw-labs/zeroclaw/issues/4045) asks for declarative cron configuration (VCS-friendly) rather than web-ui only setup.
*   **Windows Usability:** Issue [#3693](https://github.com/zeroclaw-labs/zeroclaw/issues/3693) pleads for a clearer setup process (bat files) on Windows, citing the difficulty of managing feature flags (`channel-lark` vs `web-gui`).
*   **Database-First Memory:** Issue [#4028](https://github.com/zeroclaw-labs/zeroclaw/issues/4028) proposes a move to a full pgvector/graph architecture for memory, signaling a desire for more robust knowledge management than the current implementation.

## 7. User Feedback Summary
*   **Pain Points:** The primary friction point is **Configuration vs. Capability**. Users are confused by feature flags (Windows issues) and feel restricted by the "Security" layer which denies tools without clear error messages or override paths.
*   **Satisfaction:** Users appreciate the rapid addition of new providers (Avian, Aliyun, DeepMyst) and the addition of interrupt commands (`/stop`).
*   **Dissatisfaction:** "Hallucinations" (making up tool outputs) and "Silent Failures" (ARM crashes) are eroding trust in the agent's reliability.

## 8. Backlog Watch
*   **Feature Parity:** Issue [#3839](https://github.com/zeroclaw-labs/zeroclaw/issues/3839) requests a feature matrix comparing ZeroClaw to OpenClaw, suggesting users are unclear about *why* they should switch or what is missing.
*   **Documentation:** Issue [#4072](https://github.com/zeroclaw-labs/zeroclaw/issues/4072) asks for a map between "Features" and "Config Keys," a fundamental requirement for usability that is currently missing.
*   **Stranded Code:** Issue [#4093](https://github.com/zeroclaw-labs/zeroclaw/issues/4093) needs immediate maintainer attention to recover lost streaming features or officially deprecate them.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest: 2026-03-21

## 1. Today's Overview
PicoClaw is experiencing a **high-velocity development phase**, with **61 Pull Requests** and **23 Issues** updated in the last 24 hours. The project is currently in a "Nightly" release cycle (v0.2.3-nightly), indicating active integration of new features. Activity is heavily concentrated on **stability fixes** (Docker, Cron, Agent loops), **channel enhancements** (Matrix encryption, WhatsApp multimodal), and **provider compatibility** (OpenAI strict mode, LM Studio). While feature velocity is high, there are emerging signals of technical debt regarding configuration management, documentation accuracy, and edge-case handling in agent logic.

## 2. Releases
* **Version:** `v0.2.3-nightly.20260321.100720bb`
* **Type:** Automated Nightly Build
* **Note:** Users are advised to exercise caution as this is an unstable build.
* **Details:** [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.3...main)

## 3. Project Progress
*   **Agent Logic & Stability:**
    *   **PR #1818 (Closed):** Refined the `agent` loop to distinguish between "empty model responses" and "max tool iterations reached," preventing misleading error messages. ([Link](https://github.com/sipeed/picoclaw/pull/1818))
    *   **PR #1844 (Open):** Introduced "Scoped Steering" to prevent cross-conversation message leakage during active agent turns. ([Link](https://github.com/sipeed/picoclaw/pull/1844))
*   **Cron System Reliability:**
    *   **PR #1842 (Open):** Fixed a critical bug where the cron store would overwrite externally added jobs and saved state unnecessarily every second. ([Link](https://github.com/sipeed/picoclaw/pull/1842))
    *   **PR #1839 (Open):** Fixed routing for cron jobs to ensure responses are actually published to the correct channel. ([Link](https://github.com/sipeed/picoclaw/pull/1839))
*   **Infrastructure & Docker:**
    *   **PR #1846 (Open):** Added a new `docker-compose` file tailored for local builds and SELinux-enabled environments. ([Link](https://github.com/sipeed/picoclaw/pull/1846))
*   **Documentation:**
    *   **PR #1837 (Closed):** A massive cleanup effort fixing 25+ documentation inaccuracies and adding 60 missing channel docs across 5 languages. ([Link](https://github.com/sipeed/picoclaw/pull/1837))

## 4. Community Hot Topics
*   **[Issue #1648] TTS/ASR Support (16 comments):** A highly active debate on the architecture for adding Text-to-Speech and Automatic Speech Recognition. Users are anxious for the integration of PR #1642 into the main gateway. ([Link](https://github.com/sipeed/picoclaw/issues/1648))
*   **[Issue #28] LM Studio Easy Connect (9 comments):** Persistent community request for easier integration with LM Studio, highlighting a desire for local-first AI workflows. ([Link](https://github.com/sipeed/picoclaw/issues/28))
*   **[Issue #806] WebUI Support (6 comments):** Ongoing discussion regarding the refactoring of the Web User Interface to lower the barrier to entry for non-technical users. ([Link](https://github.com/sipeed/picoclaw/issues/806))
*   **[PR #1780] QQ Channel Stability:** A significant effort to make reconnection intervals and rate limits configurable for the QQ channel, addressing reliability concerns in specific regions. ([Link](https://github.com/sipeed/picoclaw/pull/1780))

## 5. Bugs & Stability
*   **[Critical] Cron Job Failures:**
    *   **Issue #1058:** Cron tasks with `deliver=false` (default) silently discard LLM responses. **Fix incoming** in PR #1839.
    *   **PR #1842:** Cron store overwrites manual CLI additions on every tick.
*   **[High] Docker/Container Issues:**
    *   **Issue #1825:** Containers do not recover automatically after receiving `SIGINT`/`SIGTERM` due to `restart: on-failure` policy.
    *   **Issue #1763:** `aarch64 .deb` package installation failures.
*   **[Medium] Agent/Loop Logic:**
    *   **Issue #1815:** Misleading error messages suggesting `max_tool_iterations` when the model simply returns an empty string. **Fix:** PR #1818.
    *   **Issue #629:** Agent fails to retry LLM calls upon HTTP 500 errors, causing the task to hang.
*   **[Low] Provider Specifics:**
    *   **Issue #1790:** OpenRouter "free" model endpoints failing validation.
    *   **Issue #1491:** Persistent config loading errors regarding `glm-4.7`.

## 6. Feature Requests & Roadmap Signals
*   **Voice Interaction:** Strong demand for **TTS/ASR** support (Issue #1648) suggests voice capabilities are a top priority for the next minor release.
*   **Security & Encryption:** **PR #1841** is adding End-to-End Encryption (E2EE) support for the Matrix channel, addressing privacy needs.
*   **Observability:** **Issue #1848** requests granular control over logging levels to reduce noise, while **Issue #1796** proposes an "Event-driven Hooks System" for better extensibility.
*   **Context Management:** **Issue #1836** proposes "Conversation Compact" to handle context window limits in long-running tasks without losing history.

## 7. User Feedback Summary
*   **Pain Points:** Users are struggling with **configuration complexity** (Issue #1491, #28) and **debugging opaque failures** (Issue #629, #1058). The silence of failing cron jobs is a major friction point.
*   **Platform Diversity:** There is a clear demand for broader platform support, specifically **LM Studio** (Issue #28), **Email** (Issue #1794), and **OpenAI-compatible API endpoints** (Issue #1738).
*   **Documentation Gap:** While PR #1837 addressed many inaccuracies, users (Issue #1830) still feel guidance is insufficient for complex setups, calling for better i18n and onboarding.

## 8. Backlog Watch
*   **Issue #1737 (WebUI Chat):** Users report the WebUI chat input is disabled despite a working backend, suggesting a disconnect in the frontend integration.
*   **Issue #1755 (SOUL.md):** The architectural debate on whether `SOUL.md` should remain freeform or adopt an optional schema is unresolved, impacting agent consistency.
*   **PR #1460 & #1683 (OpenAI Compatibility):** These long-running PRs aim to fix tool call serialization and "Strict Mode" for third-party providers. Their status is critical for users relying on non-OpenAI backends.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest: 2026-03-21

## 1. Today's Overview
NanoClaw is experiencing a surge of high-velocity development. In the last 24 hours, the project saw **25 updated Pull Requests** (primarily new features) and **7 updated Issues**. The activity is heavily skewed toward feature expansion (23 open PRs) rather than stabilization (only 2 closed PRs), indicating an active "sprint" phase. Key themes today include multi-platform expansion (adding Twilio, Signal, Proton, White Noise), enhanced memory capabilities (Graph RAG via Mem0), and improved tooling (API usage tracking, CLI skills).

## 2. Releases
**No new releases** published in the last 24 hours.

## 3. Project Progress
**Merged/Closed Features:**
*   **Multi-Tenant Web & Dashboard:** A major feature PR (#1298) implementing a web channel (`WebClaw`) and multi-tenant infrastructure was closed today, suggesting this complex feature may have been merged, deferred, or is undergoing final review.
*   **Refactoring:** ESLint configuration was added and applied (#1297) to improve code quality and maintenance.
*   **Cross-Group Communication:** A bug fix for IC01 relay command processing (#1284) was closed, resolving logic errors where a shared operator account caused unintended command triggers.
*   **Community Features:** Support for reading incoming emoji reactions (#1288) was closed (implemented).

**New Features in Review:**
*   **Memory Systems:** Introduction of `/add-mem0-graph` (#1256) for persistent, graph-enhanced memory using Neo4j and Qdrant.
*   **Connectivity:** Significant expansion of channels including Signal (#1057), Twilio for WhatsApp (#1294), and Proton Mail (#1117).
*   **Tooling:** Introduction of API usage tracking (#1111) and a CLI skill (`claw`) (#1296).

## 4. Community Hot Topics
*   **Usage Analytics & Cost Management**
    *   **PR #1111:** [feat: add API usage tracking](https://github.com/qwibitai/nanoclaw/pull/1111)
    *   **Analysis:** There is a strong demand for observability. Users want to track costs and token usage per group/category. This PR addresses the "black box" concern of running AI agents at scale.

*   **Universal Connectivity (Signal & Proton)**
    *   **PR #1057:** [feat(skill): add Signal messenger channel](https://github.com/qwibitai/nanoclaw/pull/1057)
    *   **PR #1117:** [feat(skill): add Proton suite](https://github.com/qwibitai/nanoclaw/pull/1117)
    *   **Analysis:** The community is pushing for NanoClaw to be a true "universal inbox." These high-complexity PRs indicate users value privacy-focused (Signal) and enterprise-grade (Proton) integrations.

*   **Model Flexibility**
    *   **PR #1255:** [feat: add MiniMax OAuth](https://github.com/qwibitai/nanoclaw/pull/1255)
    *   **PR #1205:** [feat: add /model command](https://github.com/qwibitai/nanoclaw/pull/1205)
    *   **Analysis:** Users want to avoid vendor lock-in (Anthropic/Claude) and desire the ability to switch models or providers at runtime.

## 5. Bugs & Stability
**High Severity:**
*   **Data Corruption Risk:**
    *   **Issue #1272:** [Bug: DB migration incorrectly marks Telegram direct chats as is_group=1](https://github.com/qwibitai/nanoclaw/issues/1272)
    *   **Impact:** A database migration script incorrectly labels all Telegram chats as groups, breaking 1:1 direct messaging logic.
    *   **Status:** Open. No fix PR linked yet.

*   **Soft Failure State:**
    *   **Issue #1289:** [feat: add pre-flight credential validation on startup](https://github.com/qwibitai/nanoclaw/issues/1289)
    *   **Impact:** Starting without valid credentials (e.g., missing `TELEGRAM_BOT_TOKEN`) creates "zombie" directories and DB entries rather than failing fast.
    *   **Status:** Fix available in PR #1290.

**Medium Severity:**
*   **UX Confusion:** Issue #1075 (Linux docs mismatch) highlights documentation discrepancies between the README and official website.

## 6. Feature Requests & Roadmap Signals
*   **Per-Group Personas:** There is significant interest in dynamic agent personalities.
    *   **Signal:** Issue #1291 and PR #1292 propose using WhatsApp group descriptions as the system prompt. This suggests users want agents that adapt to the specific social context of different chats.
*   **Agent-to-Agent Communication:**
    *   **Signal:** PR #1295 (`/add-a2a`) allows different AI agents (Cursor, Windsurf) to talk to NanoClaw. This signals a trend toward "Multi-Agent Workflows" rather than just human-to-bot chat.
*   **Improved Onboarding:** Issue #1275 requests an auto-prompt when the bot is added to a new group, fixing the current "silent failure" UX which confuses new users.

## 7. User Feedback Summary
**Positive Sentiment:** Users are actively building complex skills (memory graphs, new channels) and sharing them via PRs, indicating high satisfaction with the extensibility of the platform.
**Pain Points:**
*   **Configuration Drift:** Users struggle with knowing if the bot is working (Issue #1289) or if a group is registered (Issue #1275).
*   **Platform Friction:** The distinction between "Groups" and "DMs" in Telegram is causing backend friction (Issue #1272), suggesting the internal abstraction layer needs refinement.

## 8. Backlog Watch
*   **Long-Term Feature:**
    *   **PR #586:** [feat: allow agents to send cross-group messages](https://github.com/qwibitai/nanoclaw/pull/586) (Open since Feb 28). This "inter-group routing" feature remains in limbo, despite high utility for automation workflows.
*   **Stability:**
    *   **PR #565:** [feat: add PID lockfile guard](https://github.com/qwibitai/nanoclaw/pull/565) (Open since Feb 27). A safeguard against duplicate instances that corrupt state has not yet been merged, representing a lingering stability risk.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest: 2026-03-21

## 1. Today's Overview
NullClaw is demonstrating high development velocity with significant improvements in platform stability and observability. The project closed 24 Pull Requests in the last 24 hours, successfully addressing critical infrastructure gaps such as SSE stream stalls, legacy Linux compatibility, and response parsing for emerging reasoning models. Active development remains focused on enterprise integrations (WeChat, DingTalk, Lark) and expanding provider support. While no new release was published today, the volume of merged fixes suggests a version bump may be imminent to stabilize the deployed codebase.

## 2. Releases
*No new releases published in the last 24 hours.*

## 3. Project Progress
**Merged & Closed Features:**
*   **Observability & Integration:** A major PR (#596) was merged introducing an abstraction layer for rich outbound messaging (`outbound.Payload`), enabling unified interactive messaging (DingTalk/Lark Card 2.0) with automated text fallbacks.
*   **Provider Expansion:** Support for Tencent Hunyuan and Baichuan models was added to `compat_providers` (#595), alongside the implementation of necessary Tencent cryptographic primitives (AES-256-CBC, TC3-HMAC-SHA256) in (#593).
*   **Reliability Fixes:** The team merged a fix (#597) to detect stalled SSE streams using `curl` speed limits, preventing silent hangs. Additionally, `native_tools` support was explicitly enabled for Z.AI/GLM providers (#577), resolving usability issues for these models.
*   **Subagent Capabilities:** The limitation where subagents could not access installed skills was resolved in (#558), allowing full skill delegation to worker agents.
*   **Runtime:** The `wasm3` interpreter was added to the runtime by default (#568), reducing external dependencies for tool execution.

## 4. Community Hot Topics
*   **[Discussion] Rich Messaging Architecture**
    *   **PR #596**: [feat(channels): abstract OutboundPayload...](https://github.com/nullclaw/nullclaw/pull/596)
    *   **Analysis:** This highly active discussion highlights the community's push towards making NullClaw a viable enterprise agent for Asian markets. The focus on DingTalk and Lark Card 2.0 indicates a demand for structured, interactive bot outputs rather than plain text.

*   **[Discussion] Ollama Cloud Authentication**
    *   **PR #615**: [feat(providers): support Ollama cloud API key...](https://github.com/nullclaw/nullclaw/pull/615)
    *   **Analysis:** Users are hosting Ollama instances in the cloud and require Bearer token authentication, moving beyond local-only keyless setups.

## 5. Bugs & Stability
**High Severity:**
*   **[OPEN] Reasoning Content Parsing (Models):** Issue #576 revealed that Moonshot AI's `kimi-k2.5` model failed because NullClaw did not parse the `reasoning_content` field.
    *   *Status:* Fix PR #578 was merged today, but user verification is pending.
    *   *Link:* [Issue #576](https://github.com/nullclaw/nullclaw/issues/576)

**Medium Severity:**
*   **[OPEN] Stalled SSE Streams:** Providers keeping connections open without sending data caused indefinite hangs.
    *   *Status:* Fix PR #597 was merged today (adds `curl --speed-limit`).
    *   *Link:* [PR #597](https://github.com/nullclaw/nullclaw/pull/597)

*   **[OPEN] OpenTelemetry Diagnostics:** User reported inability to connect OTel collector in containerized environments (Issue #638).
    *   *Status:* Open, active troubleshooting.
    *   *Link:* [Issue #638](https://github.com/nullclaw/nullclaw/issues/638)

*   **[OPEN] Custom Provider Reasoning:** User reports Custom OpenAI-compatible providers generate hallucinations because reasoning is disabled by default (Issue #659).
    *   *Status:* Open.
    *   *Link:* [Issue #659](https://github.com/nullclaw/nullclaw/issues/659)

## 6. Feature Requests & Roadmap Signals
*   **Qwen Code CLI Support:** Issue #647 requests adding "Qwen Code Cli" as a provider to leverage generous free token tiers.
*   **Configurable Timezones:** Requested in #540 and implemented in #546 (Merged). Users increasingly need local time context injected into prompts rather than hardcoded UTC.
*   **Subagent Skill Access:** Now resolved (PR #558), this was a major request for improving agent modularity.

## 7. User Feedback Summary
**Pain Points:**
*   **API Compatibility Fatigue:** Users are struggling with the "long tail" of OpenAI-compatible providers (Moonshot, Z.AI, Qwen) that implement tool calling or reasoning content slightly differently.
*   **Enterprise Setup Complexity:** The flurry of PRs regarding WeChat, DingTalk, and Lark "runbooks" suggests users find the initial authentication and flow setup for these platforms difficult and require better documentation.

**Positive Signals:**
*   Successful handling of the `kimi-k2.5` reasoning model fix indicates the project is responsive to shifts in LLM API standards (e.g., the move toward "reasoning" fields).

## 8. Backlog Watch
*   **Issue #659 (Custom Provider Reasoning):** Needs architectural decision on how to expose "enable reasoning" flags for custom generic providers.
*   **Issue #638 (Otel Diagnostics):** Needs reproduction steps or container configuration validation to ensure networking isn't the root cause.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest: 2026-03-21

## 1. Today's Overview
IronClaw is exhibiting **high-velocity development** with significant technical debt being addressed alongside new feature integration. Following the release of **v0.21.0**, the project has seen a surge in activity with 50 PRs and 41 issues updated in the last 24 hours. The codebase is undergoing substantial refactoring, particularly in the "XL" sized `ux-overhaul` and `routines` logic, indicating a transition period toward greater stability and polish. However, the community has flagged **critical security vulnerabilities** (CRITICAL severity) and high-risk bugs regarding Google integrations and database migrations that require immediate attention from maintainers.

## 2. Releases
**New Release: v0.21.0** (2026-03-20)
*   **Structured Fallbacks for Jobs**: Added logic to handle failed or stuck jobs more gracefully ([#236](https://github.com/nearai/ironclaw/pull/236)).
*   **Performance Enhancements**:
    *   Implemented an **LRU embedding cache** to optimize workspace search ([#1423](https://github.com/nearai/ironclaw/pull/1423)).
    *   Fixed a CRITICAL performance regression where the embedding cache was cloning data on every hit ([#1429](https://github.com/nearai/ironclaw/issues/1429)).
*   **Webhooks**: Routines can now be triggered via webhook callbacks ([#1254](https://github.com/nearai/ironclaw/pull/1254)).

## 3. Project Progress
Major development efforts are focused on reliability and user experience (UX):
*   **Routines & Reliability**: PRs #1470 and #1471 are open to normalize notifications and add bounded retries for transient failures in the routines system.
*   **OAuth Security**: PR #1484 aims to tighten OAuth callback state handling, addressing rate-limiting and validation fragility.
*   **UX Overhaul**: A massive "Apple-level" design overhaul is in progress ([#1277](https://github.com/nearai/ironclaw/pull/1277)), bringing glassmorphism, mobile layout fixes, and interactive REPL selectors.
*   **Import Capabilities**: New PRs #1498 and #1505 are adding native importers for Claude and OpenAI conversation histories.
*   **Database & Config**: PR #1448 removes redundant LLM config from the bootstrap `.env` to simplify setup.

## 4. Community Hot Topics
*   **Database Migration Failure**: Users are unable to upgrade to v0.19.0/v0.21.0 due to a `V6__routines` checksum mismatch in PostgreSQL ([Issue #1328](https://github.com/nearai/ironclaw/issues/1328)). This is a blocker for existing users.
*   **Google OAuth Blockades**: Users report that Google is blocking IronClaw's WASM tools due to sensitive info access requests ([Issue #902](https://github.com/nearai/ironclaw/issues/902)).
*   **Google Auth Bugs**: A flurry of bugs (issues #1500, #1502, #1503) regarding Google Slides integration and auth link generation suggests recent changes to Google tools have introduced regressions.
*   **Missing Documentation**: Users are struggling to find configuration docs for tool limits and skills ([Issue #1174](https://github.com/nearai/ironclaw/issues/1174)).

## 5. Bugs & Stability
*   **[CRITICAL] Security Vulnerabilities**: Automated CI review found **Cross-channel approval thread hijacking** (authorization bypass) and **TOCTOU race conditions** in approval thread resolution ([Issues #1485](https://github.com/nearai/ironclaw/issues/1485), [#1486](https://github.com/nearai/ironclaw/issues/1486)). Fixes are being tracked in [#1495](https://github.com/nearai/ironclaw/pull/1495).
*   **[HIGH] Database Migration**: See #1328 above. Root cause identified as modifying an already-applied migration in place.
*   **[HIGH] SSRF Risk**: Staging CI identified a Server-Side Request Forgery risk via configurable embedding base URLs ([Issue #1103](https://github.com/nearai/ironclaw/issues/1103)).
*   **[Medium] Gemini Integration**: `gemini-3.1-flash-lite-preview` is failing because function calls are missing `thought_signature` parts ([Issue #1510](https://github.com/nearai/ironclaw/issues/1510)).

## 6. Feature Requests & Roadmap Signals
*   **ACP Support**: Request to add Agent Client Protocol (ACP) job mode to delegate to other coding agents ([Issue #1506](https://github.com/nearai/ironclaw/issues/1506)).
*   **AWS Bedrock Embeddings**: Users want native Bedrock embedding support to avoid separate OpenAI/Ollama keys ([Issue #1501](https://github.com/nearai/ironclaw/issues/1501)).
*   **Self-Update Mechanism**: Request for an in-app way to update the IronClaw binary itself ([Issue #1480](https://github.com/nearai/ironclaw/issues/1480)).
*   **Debug Inspector**: Users want a "Debug Inspector" panel in the Web Gateway to see full system prompts and tool outputs ([Issue #1493](https://github.com/nearai/ironclaw/issues/1493)).

## 7. User Feedback Summary
*   **Pain Points**: The "Google Suite" of tools is currently a major source of friction, with authentication failures and blocking screens dominating recent comments. The lack of documentation ("Where is the documentation?") remains a barrier to entry for new users configuring advanced features like skills and signals.
*   **Positive Signals**: Users are actively requesting complex integrations (ACP, Bedrock, Email/Password signup) and engaging with "power user" features like routine webhooks, indicating a sophisticated and invested user base.

## 8. Backlog Watch
*   **Schema Coercion**: PR #1397 (parameter coercion for complex schemas) has been open since March 19 and is critical for WASM tool stability.
*   **PDF Replacement**: PR #1435 (replacing `pdf-extract` with `pdf_oxide`) is open and pending merge to fix dependency issues.
*   **Light Theme**: The request for a Light Theme ([Issue #761](https://github.com/nearai/ironclaw/issues/761)) is closed but seemingly not yet implemented, suggesting it may be waiting for the design system overhaul in #1277.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-03-21

## 1. Today's Overview
LobsterAI is experiencing a period of **extremely high activity and turbulence**. In the last 24 hours, the project saw **35 new issues** and **26 PR updates**, coupled with a rapid-fire release (**2026.3.20**). While development velocity is high—evidenced by new features like POPO WebSocket support and agent personae—the project is facing significant **stability and growing pains**. Critical reports involving data leakage (cross-user conversations), Windows startup failures, and memory leaks suggest that the core infrastructure is struggling to scale under the weight of new features.

## 2. Latest Releases
**Version 2026.3.20** (Released: 2026-03-20)
*   **Key Fix**: `fix: stop stubbing playwright-core and pdfjs-dist in OpenClaw runtime` ([PR #548](https://github.com/netease-youdao/LobsterAI/pull/548)).
*   **Analysis**: This release addresses a packaging/stubbing issue in the OpenClaw runtime that likely caused crashes or functional failures in browser automation tasks.

## 3. Project Progress
*   **Infrastructure & Security**:
    *   **Credential Security**: [PR #591](https://github.com/netease-youdao/LobsterAI/pull/591) (CLOSED) removed plaintext secrets from `openclaw.json`, migrating them to `${LOBSTER_*}` environment variables for better security.
    *   **CI/CD Setup**: [PR #589](https://github.com/netease-youdao/LobsterAI/pull/589) (OPEN) proposes a massive overhaul of GitHub engineering infrastructure, adding CI/CD pipelines, security scanning, and auto-labeling.
    *   **Logging Overhaul**: [PR #569](https://github.com/netease-youdao/LobsterAI/pull/569) (CLOSED) improved logging with daily rotation and export functionality.
*   **Features**:
    *   **IM Integration**: [PR #556](https://github.com/netease-youdao/LobsterAI/pull/556) (CLOSED) added WebSocket long-connection mode for POPO IM, and [PR #558](https://github.com/netease-youdao/LobsterAI/pull/558) (CLOSED) enabled one-click Feishu bot creation via QR code.
    *   **Cowork UI**: [PR #557](https://github.com/netease-youdao/LobsterAI/pull/557) (OPEN) introduces an attachment @mention reference system to clarify which files/images are being analyzed.
    *   **Model Updates**: [PR #508](https://github.com/netease-youdao/LobsterAI/pull/508) (CLOSED) added MiniMax M2.7 support.
*   **Stability Fixes**:
    *   **Session Management**: [PR #565](https://github.com/netease-youdao/LobsterAI/pull/565) (CLOSED) fixed a bug where manual stops triggered "Timeout" errors.
    *   **macOS Signing**: [PR #520](https://github.com/netease-youdao/LobsterAI/pull/520) (CLOSED) resolved macOS code signing failures caused by residual .bin symlinks.

## 4. Community Hot Topics
*   **🔒 CRITICAL: Data Leakage** ([#561](https://github.com/netease-youdao/LobsterAI/issues/561))
    *   *Summary*: A user reported seeing strangers' Feishu conversations appearing in their local LobsterAI instance.
    *   *Analysis*: This is the most severe issue reported today. It suggests either a backend routing error, a local cache confusion, or an authentication breach. **Immediate priority.**
*   **🛑 Persistent "Stopped" State** ([#554](https://github.com/netease-youdao/LobsterAI/pull/554), [#570](https://github.com/netease-youdao/LobsterAI/issues/570), [#575](https://github.com/netease-youdao/LobsterAI/issues/575))
    *   *Summary*: Multiple users report that if they delete a session while the AI is generating, the "Send" button permanently becomes "Pending"/"Stop", or the task continues running in the background.
    *   *Analysis*: A state synchronization bug between the frontend Redux store and the backend OpenClaw gateway.
*   **🚨 Gateway Crashes & Loops** ([#540](https://github.com/netease-youdao/LobsterAI/issues/540), [#572](https://github.com/netease-youdao/LobsterAI/issues/572), [#581](https://github.com/netease-youdao/LobsterAI/issues/581))
    *   *Summary*: Users report the OpenClaw gateway enters a restart loop (every few seconds) or fails to start entirely.
    *   *Analysis*: Instability in the gateway process, likely related to config validation errors or plugin loading failures (e.g., missing `memory-core`).

## 5. Bugs & Stability
*   **High Severity**:
    *   **Path Traversal Vulnerability** ([#543](https://github.com/netease-youdao/LobsterAI/issues/543)): Unvalidated `workingDirectory` allows `../` access to arbitrary files.
    *   **Windows Auto-Start Failure** ([#595](https://github.com/netease-youdao/LobsterAI/issues/595)): App exits silently after 3 seconds on Windows startup.
    *   **Memory Leak** ([#571](https://github.com/netease-youdao/LobsterAI/issues/571)): `stoppedSessions` Set in `coworkRunner.ts` accumulates IDs indefinitely, causing long-term memory growth.
    *   **Main Thread Blocking** ([#562](https://github.com/netease-youdao/LobsterAI/issues/562)): Synchronous SQLite writes block the UI. (Fix pending: [PR #573](https://github.com/netease-youdao/LobsterAI/pull/573)).
*   **Medium Severity**:
    *   **macOS Icon Corruption** ([#551](https://github.com/netease-youdao/LobsterAI/issues/551)): App icon turns into a question mark after reboot on Intel Macs.
    *   **IM Configuration "Hot Swapping"** ([#585](https://github.com/netease-youdao/LobsterAI/issues/585)): Switching models in settings doesn't update active IM (Feishu) connections without a restart.
    *   **Garbage History Injection** ([#594](https://github.com/netease-youdao/LobsterAI/issues/594)): Feishu integration triggers automatic sending of old queries.

## 6. Feature Requests & Roadmap Signals
*   **Token Usage Statistics** ([#582](https://github.com/netease-youdao/LobsterAI/issues/582)): Users want built-in cost tracking per model/provider.
*   **Offline/Enterprise Deployment** ([#587](https://github.com/netease-youdao/LobsterAI/issues/587)): Request for better air-gapped enterprise support.
*   **Skill Discovery UX** ([#567](https://github.com/netease-youdao/LobsterAI/issues/567)): Users want a `/` command in the input box to select skills, rather than hunting through file trees.
*   **Agent Personas** ([PR #544](https://github.com/netease-youdao/LobsterAI/pull/544)): Upcoming feature to switch agent "roles" (e.g., Technical Expert, Virtual Girlfriend).

## 7. User Feedback Summary
*   **Configuration Clarity**: Users are confused by the workspace setup ([#579](https://github.com/netease-youdao/LobsterAI/issues/579)) and deeply hidden image-input settings ([#588](https://github.com/netease-youdao/LobsterAI/issues/588)).
*   **IM Reliability**: While the *setup* of IMs (Feishu/POPO) is getting easier (QR codes), the *runtime* reliability is low. Reports of robots replying with history, failing to switch models, or simply not replying are common.
*   **Desktop Experience**: The Windows experience is rough (startup failures, path issues), while macOS users are plagued by signing issues and icon corruption.

## 8. Backlog Watch
*   **[PR #576](https://github.com/netease-youdao/LobsterAI/pull/576)** (OPEN): Targets Windows gateway startup reliability. Crucial for fixing the "exit after 3 seconds" and startup loops.
*   **[PR #573](https://github.com/netease-youdao/LobsterAI/pull/573)** (OPEN): Targets SQLite async I/O. Critical for UI responsiveness.
*   **[Issue #561](https://github.com/netease-youdao/LobsterAI/issues/561)**: The data leakage issue requires an immediate security audit before any other features ship.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Digest — 2026-03-21

**Project:** TinyClaw (TinyAGI/tinyclaw)
**Date:** 2026-03-21
**Status:** **Active Development** 🟢

---

### 1. Today's Overview
TinyClaw exhibited high development velocity on 2026-03-21, focusing heavily on user experience (UX) simplification and architectural refactoring. While no active issues were reported in the last 24 hours, the team successfully merged four Pull Requests alongside the release of **v0.0.16**. The primary theme of the day was "streamlining": the project removed setup friction, standardized event handling, and decoupled core logic to support future multi-modal expansions. The project appears healthy, with active maintenance progressing toward a more robust and modular agent architecture.

### 2. Releases
**New Release: v0.0.16**
- **Link:** [Release v0.0.16](https://github.com/TinyAGI/tinyclaw/releases)
- **Core Highlight: Zero-Config Onboarding:** This update eliminates the previous setup wizard. Users running `tinyagi` for the first time will experience automatic bootstrapping of the agent workspace, dependency validation, and immediate daemon launch with sensible defaults.
- **Migration Notes:** No breaking changes reported. Existing users should be able to upgrade seamlessly, enjoying a faster initialization process.

### 3. Project Progress
Significant advancements were made in reducing technical debt and improving the "out-of-the-box" experience. The following items were merged/closed:

*   **Streamlined Onboarding ([PR #244](https://github.com/TinyAGI/tinyclaw/pull/244))**
    *   *Status:* Closed
    *   *Impact:* The CLI now auto-creates settings (workspace: `~/tinyagi-workspace`) and validates dependencies (tmux, jq) automatically. This lowers the barrier to entry for new users significantly.
*   **Core Architecture Refactor ([PR #242](https://github.com/TinyAGI/tinyclaw/pull/242))**
    *   *Status:* Closed
    *   *Impact:* Provider-specific CLI logic has been extracted into an Adapter pattern. This standardizes how different LLM providers (Claude, Codex, OpenCode) are invoked, making the codebase more maintainable and extensible.
*   **Event System Redesign ([PR #245](https://github.com/TinyAGI/tinyclaw/pull/245))**
    *   *Status:* Closed
    *   *Impact:* Simplified Server-Sent Events (SSE) nomenclature (removing `chain_*` in favor of `message:*` and `agent:*`). The "office" page components were also extracted into composable hooks, improving frontend modularity.
*   **Live Workspace Update ([PR #212](https://github.com/TinyAGI/tinyclaw/pull/212))**
    *   *Status:* Closed
    *   *Impact:* Continued redesign of the `/office` experience, enhancing the visual or functional aspect of the live agent workspace.

### 4. Community Hot Topics
There are currently no "hot" discussion topics based on comment volume or reactions, as recent activity is purely development-focused with 0 comments on merged PRs. However, the active PR below indicates a specific interest in expanding provider support:

*   **Novita AI Integration ([PR #243](https://github.com/TinyAGI/tinyclaw/pull/243))**
    *   *Status:* Open
    *   *Discussion:* This PR adds [Novita AI](https://novita.ai) as a built-in provider. It leverages the existing OpenAI-compatible codex harness, indicating community demand for diverse, easily integrable LLM backends without adding heavy CLI dependencies.

### 5. Bugs & Stability
*   **Assessment:** **Stable.**
*   No issues, crashes, or regressions were reported in the last 24 hours.
*   The refactoring in PR #242 and PR #245 (closed today) appears to be stability-oriented, focusing on code cleanliness and event consistency rather than fixing critical crashes.

### 6. Feature Requests & Roadmap Signals
Based on the merged PRs and open discussions, the following features are prioritized for upcoming versions:

*   **LLM Provider Flexibility:** The open [PR #243](https://github.com/TinyAGI/tinyclaw/pull/243) suggests a roadmap direction toward supporting a wider variety of OpenAI-compatible APIs (like Novita AI) with minimal configuration overhead.
*   **Improved Observability:** The changes to SSE events in [PR #245](https://github.com/TinyAGI/tinyclaw/pull/245) (renaming to `agent:invoke`, `agent:progress`) signal a focus on better debugging and monitoring capabilities for agent actions.

### 7. User Feedback Summary
*   **Pain Points Addressed:** The changes in v0.0.16 ([PR #244](https://github.com/TinyAGI/tinyclaw/pull/244)) directly address user friction regarding setup complexity. Users previously struggled with a setup wizard; the move to "zero-config" suggests feedback that the previous onboarding was too cumbersome.
*   **Satisfaction:** The rapid closure of the "Live Office" redesign ([PR #212](https://github.com/TinyAGI/tinyclaw/pull/212)) indicates responsiveness to user desires for a better visual/interactive workspace.

### 8. Backlog Watch
*   **Action Required:** [PR #243 (Add Novita AI)](https://github.com/TinyAGI/tinyclaw/pull/243) remains open. Maintainers should review this to determine if Novita AI meets the project's criteria for a first-class provider.
*   **Clean Slate:** With 0 open issues in the last 24 hours, the immediate backlog is clear. The recent refactoring (#242) suggests the project is in a consolidation phase, cleaning up technical debt before adding major new features.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Project Digest: Moltis (2026-03-21)

## 1. Today's Overview
Moltis has demonstrated active development velocity on 2026-03-21, with a focus on cross-platform stability and provider ecosystem expansion. While no formal releases were published, the merge of dependency updates and the bustling activity in the Pull Request queue suggest the team is preparing for a future cycle. The project is currently addressing technical debt related to Windows compatibility and refining provider integrations, specifically for Google Gemini and MiniMax. However, the emergence of Windows-specific bugs in the issue tracker indicates that recent changes may have introduced regressions for that user base.

## 2. Releases
**No new releases published today.**

## 3. Project Progress
**Merged & Closed:**
*   **Dependency Maintenance:** [PR #390](https://github.com/moltis-org/moltis/pull/390) (Closed) successfully bumped the `quinn-proto` dependency from 0.11.13 to 0.11.14, ensuring the project stays up-to-date with the latest QUIC protocol implementations.

**Advancing Features:**
*   **Google Gemini Integration:** [PR #33](https://github.com/moltis-org/moltis/pull/33) remains active, adding robust support for Google Gemini (both API Key and OAuth flows). This represents a significant expansion of Moltis's AI provider capabilities.
*   **Gateway Security:** [PR #449](https://github.com/moltis-org/moltis/pull/449) is advancing features to sanitize channel configurations and mask secrets, a critical enhancement for security hygiene.

## 4. Community Hot Topics
**Top Discussion:**
*   **Matrix Support Request:** [Issue #233](https://github.com/moltis-org/moltis/issues/233) (Feature: Matrix Support)
    *   **Activity:** Updated recently with 2 comments and 1 thumbs up.
    *   **Analysis:** There is clear community interest in integrating Moltis with the Matrix protocol. This aligns with the project's "channel" strategy, potentially making Moltis a bridge between AI agents and decentralized communication protocols.

**Active Development:**
*   **MiniMax Provider Fixes:** [PR #448](https://github.com/moltis-org/moltis/pull/448) has sparked discussion regarding the correct handling of system messages in the MiniMax provider history, ensuring instruction adherence during chat sessions.

## 5. Bugs & Stability
**Critical Stability Alerts:**
1.  **Windows Installer Failure:** [Issue #457](https://github.com/moltis-org/moltis/issues/457)
    *   **Severity:** High (Blocks installation)
    *   **Details:** Users report `handler.sh not found` during the Windows installation process.
    *   **Status:** A fix is likely being prepared in [PR #436](https://github.com/moltis-org/moltis/pull/436), which addresses broader Windows file handling logic.
2.  **Windows File Locking (CRITICAL):** [PR #436](https://github.com/moltis-org/moltis/pull/436)
    *   **Severity:** Critical (Data Loss/Crash risk)
    *   **Details:** Identifies a root cause where `OpenOptions::append(true)` on Windows strips `FILE_WRITE_DATA` access, leading to `os error 5`. This PR is currently open and seeks to replace append mode with write+seek to fix the locking issue.
3.  **Onboarding Configuration:** [Issue #458](https://github.com/moltis-org/moltis/issues/458)
    *   **Severity:** Medium (UX Friction)
    *   **Details:** Importing configs from `openclaw` fails to populate examples in `moltis.toml`, leaving users with a blank configuration slate.

## 6. Feature Requests & Roadmap Signals
*   **Matrix Protocol:** The explicit request for [Matrix Support](https://github.com/moltis-org/moltis/issues/233) signals a roadmap shift toward decentralized chat protocols.
*   **Gemini Provider:** The ongoing work in [PR #33](https://github.com/moltis-org/moltis/pull/33) indicates that Google Gemini support is imminent for the next release.
*   **Secrets Management:** The active [PR #449](https://github.com/moltis-org/moltis/pull/449) suggests that robust handling of API keys and OAuth tokens is a priority for the upcoming roadmap.

## 7. User Feedback Summary
*   **Windows User Pain:** Users on Windows are experiencing significant friction, ranging from installation failures ([Issue #457](https://github.com/moltis-org/moltis/issues/457)) to deep file system locking bugs ([PR #436](https://github.com/moltis-org/moltis/pull/436)).
*   **Migration Complexity:** The report in [Issue #458](https://github.com/moltis-org/moltis/issues/458) highlights that users migrating from `openclaw` expect a smoother transition with pre-filled configuration examples.
*   **Provider Flexibility:** User engagement with PRs regarding MiniMax ([PR #448](https://github.com/moltis-org/moltis/pull/448)) and Google Gemini ([PR #33](https://github.com/moltis-org/moltis/pull/33)) indicates a demand for diverse AI provider support beyond the default options.

## 8. Backlog Watch
*   **Dependency Hygiene:** [PR #456](https://github.com/moltis-org/moltis/pull/456) is currently open, bumping major dependencies (`tar`, `aws-lc-sys`, `quinn-proto`). Maintainers should prioritize merging this to keep the supply chain secure.
*   **Unresolved Bugs:** While [PR #436](https://github.com/moltis-org/moltis/pull/436) addresses the file locking mechanism, it has not yet been merged. The Windows `LockFileEx` error remains a significant unresolved risk for users on that platform until this PR is integrated.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest: 2026-03-21

## 1. Today's Overview
CoPaw is exhibiting **high development velocity** approaching a significant milestone (v0.1.x/v1.0), with **50 issues and 50 PRs** updated in the last 24 hours. The project is currently in a stabilization phase, grappling with legacy migration pain points, specifically regarding "Skills" management and Docker workspace transitions. Community activity is robust, with substantial discussion surrounding memory management stability and feature requests for multi-agent orchestration.

## 2. Releases
**New Release: `v0.1.0.post1`**
*   **Status:** Patch release.
*   **Key Changes:**
    *   **Fix:** Added HTTP 529 to retryable status codes to handle Anthropic API overload errors (PR #1891).
    *   **Fix:** Token usage improvements.
*   **Assessment:** This release addresses specific API reliability issues. Users are encouraged to upgrade to avoid Anthropic connectivity drops.

## 3. Project Progress
*   **Docker & Migration:** A critical PR was merged/closed regarding **Docker image migration** (PR #1949). It fixes legacy workspace migration for the new multi-agent structure when `COPAW_WORKING_DIR` is customized, resolving data loss issues for containerized users.
*   **Documentation:** The team merged significant documentation updates, specifically a **Windows Desktop upgrade guide** (PR #1973) to assist users transitioning from older versions.
*   **Agent Interruption:** A unified `/stop` command mechanism (PR #1913) has been implemented to handle stuck agent tasks across all channels.

## 4. Community Hot Topics
*   **Runtime Cancellation Errors:** [Issue #1976](https://github.com/agentscope-ai/CoPaw/issues/1976) (11 comments)
    *   *Topic:* "RuntimeError: Task has been cancelled!" is affecting users.
    *   *Analysis:* Suggests instability in the async task handling layer, likely related to recent refactoring in agent hooks or memory management.
*   **Skills System Regressions:** [Issue #1711](https://github.com/agentscope-ai/CoPaw/issues/1711) (9 comments) & [Issue #1945](https://github.com/agentscope-ai/CoPaw/issues/1945) (3 comments)
    *   *Topic:* Skills cannot be disabled/deleted in v0.1.0b2; file auto-regeneration issues.
    *   *Analysis:* A major "file sync mechanism" regression is preventing users from managing agent skills, causing frustration with the new version's architecture.
*   **Memory Compression Instability:** [Issue #1596](https://github.com/agentscope-ai/CoPaw/issues/1596) (7 comments)
    *   *Topic:* Memory compression triggers too aggressively ("forgetting" recent context or hallucinating old info).
    *   *Analysis:* Users feel the "intelligent" memory management is currently unpredictable and degrades conversation quality.

## 5. Bugs & Stability
*   **Critical - Resource Exhaustion:** [Issue #1774](https://github.com/agentscope-ai/CoPaw/issues/1774) (Open)
    *   *Description:* CPU 100% usage/dead loop due to `MemoryCompactionHook` infinite recursion.
    *   *Status:* **No fix PR linked yet.** High severity for Docker/deployed instances.
*   **High - Audio Handling:** [Issue #1835](https://github.com/agentscope-ai/CoPaw/issues/1835) (Open)
    *   *Description:* Agent breaks completely after receiving audio from Feishu; `InvalidSchema` error for local file paths.
    *   *Status:* Related to file path handling vs. web URLs.
*   **Medium - Double Output:** [Issue #1892](https://github.com/agentscope-ai/CoPaw/issues/1892) (Open)
    *   *Description:* Agent outputs duplicate responses when using llama.cpp.
*   **Medium - Channel Failures:** [Issue #1987](https://github.com/agentscope-ai/CoPaw/issues/1987) (Open)
    *   *Description:* Custom channels fail to start due to `getattr` on dict type.
    *   *Fix:* PR [1991](https://github.com/agentscope-ai/CoPaw/pull/1991) is open and ready to review.

## 6. Feature Requests & Roadmap Signals
*   **Multi-Agent Orchestration:** [Issue #1990](https://github.com/agentscope-ai/CoPaw/issues/1990) & [Issue #1587](https://github.com/agentscope-ai/CoPaw/issues/1587)
    *   *Request:* Automatic Master-Sub agent scheduling. Users currently have to manually switch/copy-paste between agents.
    *   *Prediction:* The incoming "Agents Square" feature (PR #1883) may be the foundation for this, but native orchestration logic is still missing.
*   **History Search:** [Issue #1578](https://github.com/agentscope-ai/CoPaw/issues/1578)
    *   *Request:* Searchable conversation history.
    *   *Probability:* High. Basic UX requirement for long-term usage.
*   **Cloud Sandbox Integration:** [PR #1972](https://github.com/agentscope-ai/CoPaw/pull/1972)
    *   *Signal:* Integration of "OpenSandbox" for remote code execution is in active development, signaling a move toward safer/more scalable tool execution.

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Upgrade Friction:** Users report broken skills, missing files, and dependency conflicts when moving from v0.0.x to v0.1.x.
    *   **Memory "Amnesia":** The new memory compression is perceived as too aggressive or buggy, leading to context loss.
    *   **Windows Experience:** Installation is slow, and Port 8088 conflicts (Hyper-V/WSL2) are frequent blockers.
*   **Sentiment:** There is noticeable frustration regarding the "product thinking" (Issue #1551), specifically the lack of multi-user isolation and advanced channel features compared to competitors. However, first-time contributors are actively pitching in with fixes (docs, docker, channel tweaks), showing strong community support.

## 8. Backlog Watch
*   **Dependency Conflicts:** [Issue #1741](https://github.com/agentscope-ai/CoPaw/issues/1741) (Closed)
    *   *Note:* While closed, the upgrade path for Windows/Conda users remains rocky due to PyYAML and other version clashes. Monitoring needed for post-release feedback.
*   **Network Isolation (Offline):** [Issue #1708](https://github.com/agentscope-ai/CoPaw/issues/1708) (Closed)
    *   *Note:* Users complaining about forced calls to `huggingface.co`. Ensuring full offline capability is a recurring need.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest: 2026-03-21

## 1. Today's Overview
ZeptoClaw is currently in a development phase focused on tooling refinement and architectural planning. There is no active code integration (merges) or new release activity reported for the last 24 hours. The project health appears stable with moderate discussion, specifically regarding the integration of testing fixtures borrowed from the `pi_agent_rust` ecosystem. Activity is concentrated on open feature requests rather than bug remediation.

## 2. Releases
*No new releases published.*

## 3. Project Progress
*No pull requests were merged or closed in the last 24 hours.*

## 4. Community Hot Topics
The primary focus of recent discussions involves architectural decisions and testing standards:

*   **[feat] Core templates based on Containerfiles mapped-to/launched-in orchestrated Firecracker VM's** ([#387](https://github.com/qhkm/zeptoclaw/issues/387))
    *   **Activity:** High (6 comments since March 17).
    *   **Analysis:** This issue discusses a controversial architectural shift to treat "Coding Agent Frameworks" (like pi-coding-agent, claude-code, copilot-cli) as isolated applications running inside orchestrated Firecracker VMs. The community is debating the trade-offs between security isolation (reducing the security surface) and feature creep.
    *   **Link:** https://github.com/qhkm/zeptoclaw/issues/387

## 5. Bugs & Stability
*No critical bugs, crashes, or stability regressions were reported in the last 24 hours.*

## 6. Feature Requests & Roadmap Signals
Based on the issues updated today, the following features are likely on the roadmap:

*   **Low-Code Testing Framework:** Issue [#391](https://github.com/qhkm/zeptoclaw/issues/391) signals a strong push toward "Conformance fixture testing." This involves adding a JSON-based runner that allows defining tool regression tests (input args + expected output) without writing Rust code.
*   **Enhanced Tooling Capabilities:** The same issue mentions requirements for "edit fuzzy matching" and "output truncation," suggesting future iterations will focus on better handling of large codebases and command outputs.
*   **Link:** https://github.com/qhkm/zeptoclaw/issues/391

## 7. User Feedback Summary
*   **Desire for Extensibility:** The request for JSON-based testing fixtures indicates a user preference for high-level extensibility without requiring low-level (Rust) knowledge for test case creation.
*   **Security vs. Complexity:** The commentary in [#387](https://github.com/qhkm/zeptoclaw/issues/387) highlights a user concern regarding the complexity of running agent frameworks, favoring isolation via Firecracker VMs to mitigate security risks.

## 8. Backlog Watch
*   **Architectural Proposal (Open since 2026-03-17):** The Firecracker VM integration proposal ([#387](https://github.com/qhkm/zeptoclaw/issues/387)) remains open and tagged as controversial. While not a bug, it represents a significant technical debt or direction decision that requires maintainer resolution to determine the future deployment model of the agents.
*   **Tool Conformance (Created 2026-03-20):** Issue [#391](https://github.com/qhkm/zeptoclaw/issues/391) is new but represents a shift in development standards; it currently has zero comments and is waiting for maintainer or community triage.

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

Here is the **EasyClaw Project Digest** for March 21, 2026.

### 1. Today's Overview
The project is currently in a **reactive maintenance phase**, addressing platform-specific deployment issues following a recent version release. While code integration (PRs) is stagnant with no merges today, the maintainers released **v1.7.3** to specifically target macOS installation friction. However, a critical functional regression has been reported on the Windows platform (Issue #25), indicating that the recent v1.7.x update cycle may have introduced configuration parsing errors that break core agent functionality.

### 2. Releases
*   **[v1.7.3: RivonClaw v1.7.3](https://github.com/gaoyangz77/easyclaw/releases)**
    *   **Focus:** Installation stability for macOS.
    *   **Key Changes:** Addresses the "Gatekeeper" blocking mechanism where macOS warns the app is damaged.
    *   **Documentation:** Updated installation instructions to guide users on how to bypass unsigned app security blocks via Terminal.
    *   **Migration:** No breaking changes reported, but users on macOS must follow the new terminal instructions to launch the application.

### 3. Project Progress
*   **Merged PRs:** None.
*   **Fixes/Advancements:** The primary progress today is operational rather than functional. The release of v1.7.3 represents a fix for the **onboarding experience** (installability), removing a major barrier to entry for macOS users who were previously blocked by OS-level security warnings.

### 4. Community Hot Topics
*   **[#25: Windows11 v1.7.2 Tool Configuration Error](https://github.com/gaoyangz77/rivonclaw/issues/25)**
    *   **Status:** Open (Active).
    *   **Topic:** A "400 [] is too short - 'tools'" error preventing the agent from functioning.
    *   **Analysis:** This is currently the most critical topic as it represents a total failure of the agent logic on Windows. The error suggests that the agent's tool configuration array is being parsed as empty or invalid during runtime. This likely stems from a change in the backend code structure in version 1.7.2 that handles tool definitions.

### 5. Bugs & Stability
*   **High Severity: Runtime Logic Failure (Windows)**
    *   **Issue:** [#25](https://github.com/gaoyangz77/rivonclaw/issues/25)
    *   **Symptom:** The application returns a "400 [] is too short - 'tools'" error when attempting to generate a response.
    *   **Impact:** The AI assistant is completely non-functional for affected Windows users.
    *   **Fix Status:** No fix PR exists yet. The immediate workaround is likely downgrading to a version prior to 1.7.2 until a patch is released.

### 6. Feature Requests & Roadmap Signals
*   **Implied Request:** The error regarding "tools" suggests the user is trying to utilize the agent's advanced features (tool-calling/functionality).
*   **Prediction:** The next version (v1.7.4 or v1.7.5) will likely be a hotfix specifically targeting the `tools` parameter validation on Windows to resolve the logic error identified in Issue #25.

### 7. User Feedback Summary
*   **Pain Points:**
    1.  **Platform Trust (macOS):** Users struggle to run unsigned applications, requiring technical workarounds (Terminal commands) that lower the user experience.
    2.  **Broken Functionality (Windows):** Users report that the app is essentially unusable due to backend configuration errors.
*   **Satisfaction:** Low for Windows users (v1.7.2); Mixed for macOS users (fixed by v1.7.3, but requires manual intervention).

### 8. Backlog Watch
*   **[#25](https://github.com/gaoyangz77/rivonclaw/issues/25):** This issue requires immediate maintainer attention. As a blocker that prevents the app from working on a major OS, it should take precedence over feature development.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*