# OpenClaw Ecosystem Digest 2026-03-19

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-03-18 17:14 UTC

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

# OpenClaw Project Digest: 2026-03-19

## 1. Today's Overview
OpenClaw is experiencing an **extremely high volume of development activity**, with 500 Issues and 500 Pull Requests updated in the last 24 hours alone. Despite this intense velocity, no new official releases were published today, indicating a potential accumulation of unreleased fixes. The community is highly engaged, discussing critical infrastructure improvements (i18n), security warnings, and stability concerns regarding recent versions. The project appears to be in a fast-paced "sprint" state, but the lack of releases suggests users might be waiting on fixes that are already committed but not yet deployed.

## 2. Latest Releases
**None**
*Note: No new releases were published in the last 24 hours despite significant commit and PR activity.*

## 3. Project Progress
*Note: Progress is inferred from newly opened or active PRs, as "Merged/Closed" PRs were not explicitly detailed in the top 30 list provided.*

**Active Development Areas:**
*   **Unified Provider System:** PR #41496 (Open) proposes a significant architectural change to unify provider APIs (Chat, Embeddings, ASR) with a `registerProvider` capability system.
*   **Rescue & Watchdog:** PR #46502 (Open) is working on adding a core watchdog service and cron engine to repair unhealthy gateway profiles, addressing stability concerns.
*   **New Search Integration:** PR #41596 (Open) aims to add "Parallel" as a new search/fetch provider for LLM-optimized results.
*   **Subagent Improvements:** PR #40700 (Open) seeks to include partial progress when subagents time out, and PR #49004 attempts to fix orphaned session store entries.

## 4. Community Hot Topics
*   **[Top Feature] Internationalization (i18n) Support**
    *   **Issue:** [#3460](https://github.com/openclaw/openclaw/issues/3460) (103 comments)
    *   **Analysis:** There is massive community demand for multi-language support. The maintainers have explicitly stated they lack the bandwidth to support it currently, inviting community contributions. This is the highest-traffic non-bug discussion.
*   **[Top OS Request] Linux/Windows Clawdbot Apps**
    *   **Issue:** [#75](https://github.com/openclaw/openclaw/issues/75) (63 reactions, 41 comments)
    *   **Analysis:** Users are demanding feature parity for desktop apps (currently available on macOS, iOS, Android) for Linux and Windows environments.
*   **[Security Alert] Phishing Scam Warning**
    *   **Issue:** [#49836](https://github.com/openclaw/openclaw/issues/49836) (25 comments)
    *   **Analysis:** A fake repository is propagating a phishing airdrop scam. The community is actively discussing mitigation and awareness.
*   **[Token Cost] High Token Consumption with Claude**
    *   **Issue:** [#2868](https://github.com/openclaw/openclaw/issues/2868) (14 comments, 7 reactions)
    *   **Analysis:** Users report unexpectedly high token costs when switching to Claude models (Sonne), potentially related to how tool outputs or contexts are managed.

## 5. Bugs & Stability
*   **Critical Gateway Stability (v2026.3.x Regressions)**
    *   **Issue:** [#48205](https://github.com/openclaw/openclaw/issues/48205) (Gateway Restarts ~50 mins) - Users report unexplained gateway restarts.
    *   **Issue:** [#45772](https://github.com/openclaw/openclaw/issues/45772) (Heartbeat Timer Stops) - Heartbeat feature dies after 1-2 triggers (v2026.3.8).
    *   **Severity:** High - Affects core reliability.
*   **Critical Install/Onboarding Failures**
    *   **Issue:** [#49338](https://github.com/openclaw/openclaw/issues/49338) - `dist/gateway.js` missing in npm package for v2026.3.13, preventing installs.
    *   **Issue:** [#6156](https://github.com/openclaw/openclaw/issues/6156) - macOS Gateway setup wizard stuck on retry.
    *   **Issue:** [#39447](https://github.com/openclaw/openclaw/issues/39447) - npm install fails on Ubuntu 24.04.
*   **Webchat & Control UI Regressions**
    *   **Issue:** [#49544](https://github.com/openclaw/openclaw/issues/49544) - Model switcher in Webchat prepends wrong provider ID.
    *   **Issue:** [#45753](https://github.com/openclaw/openclaw/issues/45753) - Control UI pairing fails with gateway timeout.
*   **Messaging Channels**
    *   **Issue:** [#34741](https://github.com/openclaw/openclaw/issues/34741) - WhatsApp desync (No active listener).
    *   **Issue:** [#48388](https://github.com/openclaw/openclaw/issues/48388) - Feishu filenames garbled (encoding issue).

## 6. Feature Requests & Roadmap Signals
*   **Centralized Filename Encoding:** Issue [#48788](https://github.com/openclaw/openclaw/issues/48788) proposes a utility to handle multi-encoding Content-Disposition (Shift-JIS, EUC-KR, etc.) to fix file handling issues globally.
*   **Operon-Guard Skill:** PR [#49387](https://github.com/openclaw/openclaw/pull/49387) introduces a "pre-flight trust verification" skill for AI agents to detect prompt injections and PII leaks.
*   **Voice Wake Word:** Issue [#147](https://github.com/openclaw/openclaw/issues/147) requests integration with "Brabble" for distributed voice wake (Star Trek style).

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Regression Anxiety:** There is a distinct pattern of users reporting features that "worked before" failing in recent versions (e.g., CLI handshake failing with `gateway closed (1000)` in [#48167](https://github.com/openclaw/openclaw/issues/48167), Google Vertex ADC auth breaking in [#49191](https://github.com/openclaw/openclaw/issues/49191)).
    *   **Cost Management:** Users are sensitive to token usage, specifically calling out Claude models ([#2868](https://github.com/openclaw/openclaw/issues/2868)) and runaway heartbeat loops causing excessive API calls ([#3181](https://github.com/openclaw/openclaw/issues/3181)).
    *   **Platform Fragmentation:** Linux and Windows users feel like second-class citizens regarding the desktop apps ([#75](https://github.com/openclaw/openclaw/issues/75)).
*   **Satisfaction:** Users actively contributing PRs to fix bugs indicate high engagement and a willingness to help maintain the project despite current instability.

## 8. Backlog Watch
*   **Stale Issues:** Several high-severity bugs remain "Stale" or open for months without resolution:
    *   **IRC Duplicate Connections:** [#21154](https://github.com/openclaw/openclaw/issues/21154) (Open since Feb).
    *   **Mac App Config Overwrites:** [#21009](https://github.com/openclaw/openclaw/issues/21009) (Mac App stripping auth keys).
    *   **Windows Restart Crashes:** [#19819](https://github.com/openclaw/openclaw/issues/19819) (SIGUSR1 restart crashes).
    *   **Vision Handling:** [#23452](https://github.com/openclaw/openclaw/issues/23452) (Systemic issues with image recognition across channels).

---

## Cross-Ecosystem Comparison

# Ecosystem Analysis Report: Personal AI Assistant & Agent Landscape (2026-03-19)

## 1. Ecosystem Overview
The open-source AI agent ecosystem is currently undergoing a phase of **explosive growth and architectural divergence**. The landscape is dominated by two distinct paradigms: **heavyweight orchestration frameworks** (exemplified by OpenClaw, IronClaw, and LobsterAI) which prioritize feature depth and provider integration, and **lightweight, opinionated clients** (NanoBot, NanoClaw, PicoClaw) which prioritize speed and specific deployment targets (e.g., local-only or containerized). A major trend across the ecosystem is the **hard pivot towards multi-language support (i18n)** and the standardization of **Observability (OpenTelemetry)** as production readiness becomes a priority over mere functionality. Concurrently, there is a visible split regarding "Autonomy," with projects like Zeroclaw tightening security defaults while others like NanoClaw face community pressure to decouple from single-vendor lock-in (Anthropic).

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score* |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | No Release (High Churn) | 🟡 High Load / Unstable |
| **IronClaw** | 50 | 43 | No Release | 🟢 Stabilizing |
| **CoPaw** | 50 | 50 | **v0.1.0-beta.3** | 🟢 High Velocity |
| **Zeroclaw** | 40 | 50 | **v0.5.0** (Major) | 🟡 Growing Pains |
| **TinyClaw** | 0 | 13 | **v0.0.15** (Rebrand) | 🟢 Consolidating |
| **NanoClaw** | 18 | 50 | No Release | 🟡 Tech Debt |
| **NanoBot** | 30 | 58 | No Release | 🟡 Regression Anxiety |
| **NullClaw** | 5 (Updated) | 33 | **v2026.3.17** | 🟢 Enterprise Focus |
| **LobsterAI** | 13 | 10 | No Release | 🔵 Update Fatigue |
| **PicoClaw** | 30 | 84 | **Nightly** | 🟢 Refactoring |
| **EasyClaw** | 4 | 1 | **v1.7.1** (Hotfix) | 🔴 Windows Instability |
| **Moltis** | 1 | 1 | No Release | 🔵 Maintenance |
| **ZeptoClaw** | 3 | 2 | No Release | 🟢 Niche Hardening |

*\*Health Score is based on release stability vs. issue volume and community sentiment.*

## 3. OpenClaw's Position
**OpenClaw** remains the undisputed market leader in terms of sheer community mass and developer bandwidth, acting effectively as the "reference implementation" for the ecosystem.
*   **Advantages:** It possesses the largest pool of community contributors (evidenced by 500 active PRs) and the most extensive third-party integration library. It is the primary dependency for forks like **LobsterAI**.
*   **Technical Approach:** OpenClaw is pursuing a "Unified Provider" architecture (PR #41496) to normalize API differences, whereas competitors like **IronClaw** are focusing on specific "Routines" engines and **NanoClaw** is prioritizing specific deployment patterns (e.g., bare metal).
*   **Community Size:** With active issue counts an order of magnitude higher than peers (500 vs. ~50), OpenClaw faces a unique "scaling pain" where bandwidth is the bottleneck for critical requests like i18n and platform parity.

## 4. Shared Technical Focus Areas
*   **Internationalization (i18n):**
    *   **OpenClaw:** Top community request (#3460); maintainers lack bandwidth.
    *   **CoPaw:** Actively updating web console for multi-language support in v0.1.0-beta.3.
    *   **NanoClaw:** High priority for user experience.
*   **Observability & Tracing:**
    *   **NanoBot:** Integrating Langfuse (#2189).
    *   **NullClaw:** Added OTLP support in v2026.3.17.
    *   **PicoClaw:** Requesting OpenTelemetry GenAI support (#1731).
*   **Multi-Vendor / Decoupling:**
    *   **NanoClaw:** "Support runtime(s) other than Claude" (Issue #80) is the defining strategic debate.
    *   **IronClaw:** Rapidly adding Gemini, Aliyun, and MiniMax providers.
*   **Security & Credentials:**
    *   **NullClaw:** Implemented 90-day secret rotation.
    *   **NanoBot:** Moving to runtime secret resolution (PR #2212).
    *   **ZeptoClaw:** Proposing Firecracker VMs for isolation (Issue #387).

## 5. Differentiation Analysis
| Feature Focus | Key Projects | Differentiation Strategy |
| :--- | :--- | :--- |
| **"Do Everything" Framework** | **OpenClaw**, **IronClaw** | Massive plugin ecosystems; suitable for complex orchestrations and enterprise "Routines." |
| **Lightweight / Local-First** | **NanoBot**, **TinyAGI**, **PicoClaw** | Focus on resource efficiency and "living" agents (e.g., TinyAGI's memory hierarchy). |
| **Enterprise / Ops-Ready** | **NullClaw**, **LobsterAI** | Built-in observability, hot-reloading, and specific corporate channel integrations (Feishu, DingTalk). |
| **Security Hardened** | **ZeptoClaw**, **Zeroclaw** | Focus on sandboxing (Firecracker) and strict execution policies. |
| **Desktop GUI Wrapper** | **EasyClaw** (RivonClaw) | Focus on native macOS/Windows UX rather than backend extensibility. |

## 6. Community Momentum & Maturity
*   **Rapidly Iterating (The "Sprints"):** **CoPaw** and **IronClaw** are displaying high velocity with clear roadmaps (Beta releases and "Bug Bashes"). **TinyAGI** is undergoing a successful rebrand and consolidation.
*   **Stabilizing:** **NullClaw** shows signs of moving from "feature add" to "enterprise hardening" (secrets, tracing).
*   **Plateauing / Strained:** **OpenClaw** is experiencing technical debt strain (regressions in v2026.3.x, missing npm files). **NanoBot** is facing growing pains regarding its "lightweight" claim due to Node.js dependency bloat.
*   **Maintenance Mode:** **Moltis** is purely addressing critical crashes (panics) with low feature churn.

## 7. Trend Signals
*   **The "Claude-Lock" Anxiety:** There is a palpable fear across the community (strongest in **NanoClaw** Issue #80, but visible in **IronClaw** and **Zeroclaw** provider additions) of vendor lock-in. Projects are racing to support OpenAI, Gemini, and local models (vLLM/Ollama) to mitigate API ban risks.
*   **"Tool Misuse" & Prompt Injection:** As agents become more autonomous, **IronClaw** (Issue #1364) and **Zeroclaw** (Issue #1478) are highlighting that LLMs are misusing tools or bypassing safety filters. This is driving the "Security vs. Usability" crisis where users want power (Zeroclaw) but devs are adding guardrails.
*   **Container Fatigue:** Users are pushing back against Docker-only architectures. **NanoClaw** (Issue #1225) and **NanoBot** (Issue #660) both see active requests for "bare metal" installs to reduce overhead.
*   **Cost & Token Efficiency:** With the rise of large context models, **LobsterAI** and **OpenClaw** users are demanding visibility into token usage and context compression features to control API costs.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-03-19
**Repository:** [HKUDS/nanobot](https://github.com/HKUDS/nanobot)

---

### 1. Today's Overview
NanoBot is experiencing a period of high activity and rapid iteration. In the last 24 hours, the project saw 58 updated PRs and 30 updated issues, indicating a push toward feature stabilization and expansion. However, this churn has introduced stability regressions, particularly for users upgrading to recent `post` releases (e.g., `v0.1.4.post5`), with reports of broken voice transcription and duplicate messaging. The community is actively engaged in high-level architectural discussions, focusing on "Observability" (tracing) and "Security" (secret management), suggesting these are key priorities for the project's evolution.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
While no PRs were marked as "merged" in the raw data provided for the last 24h, significant development work is underway in open PRs:
*   **Security & Config Management:** Work has begun on resolving [#2172](https://github.com/HKUDS/nanobot/issues/2172) via PR [#2212](https://github.com/HKUDS/nanobot/pull/2212) and [#2218](https://github.com/HKUDS/nanobot/pull/2218) to support environment variable references (`{env:VAR}`) and runtime secret resolution, moving away from plaintext API keys.
*   **WhatsApp Experience:** PR [#2216](https://github.com/HKUDS/nanobot/pull/2216) was opened to add `group_policy` controls, allowing the bot to reply only when mentioned in groups.
*   **Observability:** Integration with Langfuse (observability) is being actively discussed in preparation for future support.

### 4. Community Hot Topics
*   **[Feature Request] Enqueueing user messages during agent loops** ([#2133](https://github.com/HKUDS/nanobot/issues/2133) - 13 comments)
    *   *Summary:* Users want the ability to interrupt or guide an agent *during* a long task without stopping the loop or waiting for it to finish.
    *   *Analysis:* Highlights a UX friction point where the "global lock" mechanism blocks real-time interactivity.
*   **[Bug] Infinite loop response with llama3.3-70b-instruct** ([#1240](https://github.com/HKUDS/nanobot/issues/1240) - 13 comments)
    *   *Summary:* Agent gets stuck repeating queries until interrupted.
    *   *Analysis:* A core stability concern for specific model providers.
*   **[Architecture] Support for Langfuse observability** ([#2189](https://github.com/HKUDS/nanobot/issues/2189) - 4 comments)
    *   *Summary:* Request for tracing/logging to debug LLM calls.
    *   *Analysis:* Strong signal that "Power Users" need better debugging tools than simple stdout logging.

### 5. Bugs & Stability
*   **[High Severity] Regression: Voice Transcription Failure** ([#2141](https://github.com/HKUDS/nanobot/issues/2141))
    *   Users report that upgrading to `v0.1.4.post5` breaks voice transcription in Telegram, citing missing `summarize` skill dependencies.
*   **[High Severity] Regression: Duplicate Messages** ([#2208](https://github.com/HKUDS/nanobot/issues/2208))
    *   Android users specifically report receiving duplicate Telegram messages after upgrading.
*   **[Medium Severity] Anthropic Provider Broken** ([#2200](https://github.com/HKUDS/nanobot/issues/2200))
    *   Sudden `BadRequestError` from Anthropic provider suggests an API compatibility or schema issue.
*   **[Medium Severity] Jina Search 422 Error** ([#2194](https://github.com/HKUDS/nanobot/issues/2194))
    *   Web search fails completely with Jina provider; fallback to DuckDuckGo is also reported as non-functional.

### 6. Feature Requests & Roadmap Signals
*   **Observability (Tracing):** Multiple requests ([#2189](https://github.com/HKUDS/nanobot/issues/2189), [#2154](https://github.com/HKUDS/nanobot/issues/2154), [#2158](https://github.com/HKUDS/nanobot/issues/2158)) for Trace IDs and Langfuse integration suggest this is a high-priority item for the next milestone.
*   **Security:** The strong reaction to Issue [#2172](https://github.com/HKUDS/nanobot/issues/2172) (Secret References) indicates immediate demand for secure credential management.
*   **Performance:** PR [#2202](https://github.com/HKUDS/nanobot/pull/2202) proposes parallel tool execution to address the "agent loop is too slow" complaint ([#2098](https://github.com/HKUDS/nanobot/issues/2098)).
*   **Multi-tenancy:** Request for strict workspace/data isolation per user ([#2102](https://github.com/HKUDS/nanobot/issues/2102)).

### 7. User Feedback Summary
*   **Pain Points:** The "Ultra-lightweight" claim is being challenged due to the inclusion of Node.js in the Docker image ([#660](https://github.com/HKUDS/nanobot/issues/660)). Users are also frustrated by the lack of real-time interactivity (waiting for agent loops to finish) ([#2133](https://github.com/HKUDS/nanobot/issues/2133)).
*   **Configuration Fatigue:** Users are happy with the new interactive config wizard ([#2018](https://github.com/HKUDS/nanobot/issues/2018)) but frustrated with the lack of support for multiple custom model configurations ([#1991](https://github.com/HKUDS/nanobot/issues/1991)).
*   **Usability in Production:** Users are deploying custom solutions for boot notifications ([#2160](https://github.com/HKUDS/nanobot/issues/2160)) and UI dashboards ([#2213](https://github.com/HKUDS/nanobot/issues/2213)), indicating a desire for these features to be integrated into the core.

### 8. Backlog Watch
*   **Node.js Dependency:** Issue [#660](https://github.com/HKUDS/nanobot/issues/660) (Open since Feb 14) regarding the "bloated" Node.js dependency remains unresolved, challenging the project's "lightweight" positioning.
*   **MCP Tool Image Handling:** Issue [#1792](https://github.com/HKUDS/nanobot/issues/1792) regarding images obtained from MCP tools not being sent correctly is closed in PR but worth monitoring for regressions.

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## Zeroclaw Project Digest: 2026-03-19

### 1. Today's Overview
Zeroclaw is experiencing a **high-velocity development cycle**, transitioning from the beta 0.5.x series to the stable `v0.5.0` release. The project shows robust activity with 40 updated issues and 50 updated PRs in the last 24 hours. While the release cadence is high (9 recent releases), the community is signaling **growing pains regarding stability and user experience**. There is a noticeable tension between the rapid addition of new features (channels, providers, tools) and the maintenance of core stability, particularly concerning Docker environments and ARM64 architecture. The maintainer, **Argenis**, is actively driving releases, though community contribution in the form of merged PRs appears to be lagging behind the influx of new issues.

### 2. Releases
**Major Release:** [v0.5.0](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.5.0)
This marks a significant milestone for the project. Key highlights include:
*   **New Channels:** Official support for **Reddit**, **Bluesky**, and generic **Webhooks** has been added to the adapter list.
*   **Self-Healing CLI:** A new `self-test` command (with quick/full modes) and a sophisticated 6-phase `update` command with rollback capabilities have been introduced to improve deployment reliability.
*   **Infrastructure:** CI pipelines now utilize pre-built binaries for Docker images to speed up delivery.
*   **Healthchecks:** Added `status --format=exit-code` specifically for Docker healthchecks.

**Pre-Releases:** The project aggressively iterated through `v0.5.0-beta.341` to `v0.5.0-beta.351`, introducing features like **WhatsApp voice notes**, **Anthropic provider support**, and a **Knowledge Graph** for expertise capture.

### 3. Project Progress
*   **Docker & CI Hygiene:** There is a strong focus on fixing the developer experience.
    *   PR [#3897](https://github.com/zeroclaw-labs/zeroclaw/pull/3897) & [#3893](https://github.com/zeroclaw-labs/zeroclaw/pull/3893): Change the default Docker container command from `gateway` to `daemon`. This is a critical fix as the previous default started only the API server, preventing channel listeners (Telegram, Matrix, etc.) from spawning.
    *   PR [#3880](https://github.com/zeroclaw-labs/zeroclaw/pull/3880): Fixed Docker builds failing due to `.dockerignore` conflicts.
*   **Runtime Stability:**
    *   PR [#3885](https://github.com/zeroclaw-labs/zeroclaw/pull/3885): Fixed conversation context loss in the Claude Code CLI provider.
    *   PR [#3886](https://github.com/zeroclaw-labs/zeroclaw/pull/3886): Squashed a bug where "one-shot" cron jobs would re-execute indefinitely.
*   **Channel Enhancements:**
    *   PR [#3895](https://github.com/zeroclaw-labs/zeroclaw/pull/3895): Added interrupt support for Matrix channels (canceling tasks on new messages).
    *   PR [#3891](https://github.com/zeroclaw-labs/zeroclaw/pull/3891): Introduced a global `/stop` command to cancel in-flight tasks across all channels.

### 4. Community Hot Topics
*   **Security vs. Usability Crisis:**
    *   Issue [#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478) (👍 5): Users are frustrated by Zeroclaw's strict security defaults. Complaints range from the bot refusing to install `ffmpeg` to restricting shell access despite users opening up all configurations. The sentiment is: *"It's so secure it's useless as an autonomous agent."*
*   **Feature Parity & Documentation:**
    *   Issue [#3839](https://github.com/zeroclaw-labs/zeroclaw/issues/3839): Users are confused about the differences between Zeroclaw, Openclaw, and Ironclaw, requesting a clear feature matrix.
    *   Issue [#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503): High demand for **Napcat/Onebot** channel support, which is currently missing.

### 5. Bugs & Stability
**Critical Severity (Data Loss / Crash):**
*   **ARM64 Instability:** Issue [#3537](https://github.com/zeroclaw-labs/zeroclaw/issues/3537) reports the daemon crashes silently on Raspberry Pi 4 / ARM64 (v0.2.1+), which is a regression from v0.1.7. Similarly, Issue [#3714](https://github.com/zeroclaw-labs/zeroclaw/issues/3714) notes containers exiting immediately on DGX Spark (ARM64).
*   **Docker "Exit Code 0":** Related to the ARM64 issues, users report containers starting and then immediately stopping (Issue [#3714](https://github.com/zeroclaw-labs/zeroclaw/issues/3714)).

**High Severity (Workflow Blocked):**
*   **Missing Web Dashboard:** Issue [#3580](https://github.com/zeroclaw-labs/zeroclaw/issues/3580). The web dashboard returns a build instruction error page instead of the UI, blocking CLI-less management.
*   **MCP Tools Not Activating:** Issue [#3826](https://github.com/zeroclaw-labs/zeroclaw/issues/3826). In daemon/Telegram mode, deferred MCP tools are never activated (tool_search is never called).
*   **OpenRouter Timeout:** Issue [#3842](https://github.com/zeroclaw-labs/zeroclaw/issues/3842). OpenRouter provider ignores `provider_timeout_secs`, failing exactly at 120s with opaque decode errors.

### 6. Feature Requests & Roadmap Signals
*   **Alibaba Cloud Coding Plan:** PR [#3889](https://github.com/zeroclaw-labs/zeroclaw/pull/3889) and Issue [#3882](https://github.com/zeroclaw-labs/zeroclaw/issues/3882) indicate strong intent to add support for Alibaba's Coding Plan API for programming assistance.
*   **MQTT Support:** PR [#3896](https://github.com/zeroclaw-labs/zeroclaw/pull/3896) proposes an `mqtt_publish` tool, suggesting roadmap movement toward distributed/multi-agent architectures (leader/follower patterns).
*   **Runtime Model Switching:** Issue [#3854](https://github.com/zeroclaw-labs/zeroclaw/issues/3854) requests the ability to switch AI models mid-conversation, a feature critical for cost vs. performance tuning.
*   **Token Efficiency:** Issue [#3892](https://github.com/zeroclaw-labs/zeroclaw/issues/3892) highlights a critical need for an "analyzer layer" to strip unnecessary context, as the current implementation is too token-hungry for local LLMs with small context windows.

### 7. User Feedback Summary
**Pain Points:**
1.  **Configuration Complexity:** Users find the configuration (TOML) and migration between versions brittle and difficult (Issue [#3851](https://github.com/zeroclaw-labs/zeroclaw/issues/3851), [#3838](https://github.com/zeroclaw-labs/zeroclaw/issues/3838)).
2.  **The "Too Safe" Problem:** A segment of the power-user community feels the agent is over-nannied, requiring manual intervention for tasks that should be automated (Issue [#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478)).
3.  **Compilation on Small Devices:** Users on Orange Pi/Raspberry Pi are struggling to compile or run the pre-built binaries due to architecture mismatches (Issue [#3848](https://github.com/zeroclaw-labs/zeroclaw/issues/3848)).

**Satisfaction:**
Users seem pleased with the rapid addition of new channels (Bluesky, Reddit) and the new "Knowledge Graph" feature for expertise capture.

### 8. Backlog Watch
*   **Slack Threading:** Issue [#3888](https://github.com/zeroclaw-labs/zeroclaw/issues/3888) requests a `thread_replies` toggle for Slack (similar to Mattermost) to improve mobile visibility.
*   **Skill Caching:** Issue [#3845](https://github.com/zeroclaw-labs/zeroclaw/issues/3845) highlights that adding new skills to the workspace directory does not refresh them in a long-running daemon process, requiring a restart.
*   **Cross-Compilation:** Issue [#3848](https://github.com/zeroclaw-labs/zeroclaw/issues/3848) requests an official cross-compilation strategy for small ARM devices.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# Project Digest: PicoClaw (2026-03-19)

## 1. Today's Overview
PicoClaw is experiencing a period of high activity and rapid iteration, currently centered around a major "Agent Refactor." In the last 24 hours, the project tracked 114 active items (30 Issues, 84 PRs), with 38 PRs merged/closed indicating a high velocity of integration. The `nightly` branch remains active, suggesting the main branch is in a volatile but feature-rich state. The community is highly engaged, particularly regarding Agent capabilities (Soul/Personality), TTS/ASR integration, and stability in multi-agent environments (Subagents).

## 2. Releases
*   **Version:** `nightly` (v0.2.3-nightly.20260318.513537d2)
*   **Status:** Automated build (Unstable).
*   **Changelog:** The nightly build covers the delta between `v0.2.3` and `main`.
    *   **Key Integrations:** This build likely includes the recently merged support for **Agent Identity (`SOUL.md`/`USER.md`)** and the **DingTalk rich card client**.
    *   **Usage:** Users are advised to use with caution due to the ongoing "Agent refactor" modifying core behaviors.

## 3. Project Progress
Several significant features and fixes have been finalized or are in the final stages of review:

*   **Agent Identity System (#890 - CLOSED):** The core definition of an Agent has been expanded. `SOUL.md` (personality) and `USER.md` (user preferences) are now automatically loaded into the agent context, allowing for more personalized and persistent AI interactions.
*   **Resilience & Failover (#1707 - CLOSED):** A new configuration `api_keys` has been added to `ModelConfig`, supporting automatic failover when multiple API keys are provided. This improves reliability for commercial provider users.
*   **Subagent Tool Registry (#1711 - CLOSED):** A critical bug where subagents spawned via the `spawn` tool lost access to tools (returning "tool not found") has been fixed.
*   **DingTalk Enhancement (#1251 - OPEN):** Implementation of a new DingTalk client supporting rich card messages and updates is ready for review.
*   **Exec Tool Modernization (#1752 - OPEN):** A major update to the `exec` tool is in review, adding **PTY support** (for interactive commands) and **background execution** (for long-running tasks).

## 4. Community Hot Topics
The community is intensely debating the future architecture of the "Agent."

*   **[Meta] Agent Refactor (#1216):** The most significant strategic discussion. Maintainers and users are debating how to define agent semantics, conversation flows, and context boundaries to prevent technical debt.
*   **[Agent] SOUL.md & USER.md Updates (#1756):** Users are requesting that Agents be explicitly instructed to update their own `SOUL.md` and `USER.md` files, creating a "living" personality that evolves over time.
*   **[Feature] TTS/ASR Support (#1648):** High demand for voice interaction. Users are pushing for a flexible audio architecture to integrate Text-to-Speech and Speech-to-Text capabilities into the gateway.
*   **[Feature] WebUI Support (#806):** A request with high community engagement (👍 7). Users want a browser-based interface to lower the barrier to entry compared to the current TUI (Terminal UI).

## 5. Bugs & Stability
Recent reports indicate friction with specific provider integrations and concurrency issues.

*   **[CRITICAL] Subagent Spawning Failure (#1713):** Users reported that subagents spawned via the `spawn` tool have no tools (`tools` field missing in payload).
    *   *Status:* Fix PR #1711 is closed/merged. Nightly users should verify if this is resolved.
*   **[HIGH] Feishu/Lark Auth Expiry (#1307):** Feishu (Lark) integration breaks after 12 hours due to access token expiry, requiring manual restarts or intervention.
*   **[HIGH] GLM/Coding Plan Compatibility (#1652, #1658):** Errors using GLM Coding Plan (balance errors) and Claude (tool use name string errors) suggest recent changes to tool definitions may have broken compatibility with specific strict providers.
*   **[MED] OpenRouter Spawn Bug (#1716):** Model slugs (e.g., `openrouter/...`) are not normalized correctly during async spawn, causing 400 errors.
*   **[MED] Feishu Table Limits (#1727):** The API returns errors when the agent generates cards with too many markdown tables.

## 6. Feature Requests & Roadmap Signals
Based on new issues, the roadmap is expanding toward observability and multimodal inputs.

*   **Observability (OTel) (#1731):** A request to add **OpenTelemetry (OTel) GenAI support** for enterprise-level monitoring. This signals a push for PicoClaw to be production-ready in enterprise environments.
*   **Exec Tool Enhancement (#1733):** Users want to run long-background tasks (like `docker build`) and interactive TUIs via the agent, currently blocked by synchronous execution.
*   **OpenAI API Channel (#1738):** Users want to expose PicoClaw *as* an OpenAI-compatible endpoint, allowing it to be dropped into existing ecosystems as a replacement for the OpenAI API.
*   **Filter Thinking Output (#1714):** Request for a UI toggle to hide `think` tags (`

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-03-19

## 1. Today's Overview
NanoClaw is experiencing a **significant surge in development activity**, with 50 Pull Requests and 18 Issues updated in the last 24 hours. The project appears to be in a rapid iteration phase, heavily focused on expanding its ecosystem (new "Skills" and integrations like Telegram and Email) while simultaneously addressing critical architectural concerns regarding security and credential management. While feature velocity is high, the influx of automated "merge-forward failed" issues and recurring high-priority bugs suggests the project is currently technically strained, particularly around containerization and runtime environments.

## 2. Latest Releases
*No new releases published in the last 24 hours.*

## 3. Project Progress
*Significant Merges & Advancements:*

*   **Credential Injection Flow:** PR #1239 ("Prefer injected credentials") is currently open and advancing the architecture to better support environment-based auth, a crucial step for production deployments.
*   **New Communication Channels:**
    *   **Telegram:** PR #1233 (Closed/Merged likely for review) added a Telegram channel with voice transcription capabilities via OpenAI Whisper.
    *   **Email:** PR #1235 (Open) introduces full IMAP/SMTP integration, treating email as both an inbox channel and an agent toolset.
*   **Explosive Skill Growth:** The community is rapidly extending functionality via the "Skills" system. New additions in the pipeline include:
    *   **Dashboard:** PR #1187 adds a web-based monitoring dashboard (`/add-dashboard`).
    *   **Memory:** PR #1195 adds persistent memory with full-text search (BM25/FTS5).
    *   **Security Auditing:** PR #1196 introduces an automated security audit skill.
    *   **Soul/Personality:** PR #1198 allows adding a persistent `SOUL.md` for agent personality.

## 4. Community Hot Topics
*   **Vendor Lock-in & Risk Management (#80)**
    *   *Issue:* [Support runtime(s) other than Claude](https://github.com/qwibitai/nanoclaw/issues/80)
    *   *Stats:* 25 Comments, 47 👍 reactions.
    *   *Analysis:* This is the defining strategic discussion for the project. Users are fearful of Anthropic revoking access for "OpenClaw"-like usage and are demanding flexibility to support alternatives (OpenAI, Gemini, vLLM). A recent PR (#1241) attempts to address this by documenting vLLM backend troubleshooting.
*   **Security Fundamentals (#865)**
    *   *Issue:* [Using containers alone doesn't make you more secure](https://github.com/qwibitai/nanoclaw/issues/865)
    *   *Stats:* High Priority, Closed.
    *   *Analysis:* A spirited debate on the illusion of container security. The author argued that trusting scripts at the agent level is unsafe. While closed, the discussion drove immediate action, evidenced by PR #1231 ("fix command injection, read-only agent src").
*   **Native vs. Docker Deployment (#1225)**
    *   *Issue:* [Run it without docker](https://github.com/qwibitai/nanoclaw/issues/1225)
    *   *Analysis:* Users are requesting a "bare metal" installation option, finding the Docker requirement too heavy for Windows/Linux environments without containerization.

## 5. Bugs & Stability
*High Severity:*
*   **Outdated Models in Containers (#1142)**: Containers are pinned to Agent SDK v0.2.34, forcing the use of outdated models (e.g., old Sonnet) instead of the latest defaults.
    *   *Fix Status:* OPEN.
*   **Credential Proxy Binding (macOS) (#1103)**: The proxy binds to `127.0.0.1`, which is unreachable in Apple Container environments (Linux VM), causing `ENOTFOUND` errors.
    *   *Fix Status:* OPEN.
*   **Unicode Corrupting Transcripts (#889)**: Bash output containing lone Unicode surrogates corrupts the `.jsonl` session history, causing subsequent API calls to fail with HTTP 400.
    *   *Fix Status:* OPEN (High Priority).
*   **Sync Failures (#1236)**: Updates to `agent-runner` source code do not propagate to existing groups, leaving them with outdated tools/MCP servers.
    *   *Fix Status:* OPEN.

*Stability Risks:*
*   There are multiple automated reports of **merge conflicts** in `skill/apple-container` and `skill/compact` branches (#1226, #1227, #1228), indicating the branch-based skill architecture is prone to merge conflicts during fast-paced development.

## 6. Feature Requests & Roadmap Signals
*   **Multi-Model Support:** Strong signals (Issue #80, PR #1241) suggest a roadmap priority is decoupling from the "Claude-only" constraint to support OpenAI, vLLM, and local models.
*   **Session Management:**
    *   **Reset Context:** Feature request #1211 asks for a `/new` command to clear session context and reduce token waste.
    *   **Recovery:** Bug #1216 highlights the need for auto-recovery when Claude Code session IDs expire.
*   **Credential Ease-of-Use:**
    *   Issue #1217 requests using the `primaryApiKey` from `~/.claude.json` (the standard CLI config) as a fallback, eliminating the need to manually set `ANTHROPIC_API_KEY`.
*   **Kubernetes Support:** Issue #1184 indicates difficulty running NanoClaw in restricted K8s environments (Sealos), suggesting a future need for "Official K8s manifests."

## 7. User Feedback Summary
*   **Pain Points:** The "Docker-required" architecture is a friction point for users on Windows or without container infrastructure (Issue #1225). Additionally, the complexity of manually configuring API keys is annoying users who already have the official Claude CLI installed (Issue #1217).
*   **Platform Proxy Issues:** Users in China (Issue #1210) are reporting failures when using proxy services like Alibaba DashScope to route Claude models, specifically citing model mapping errors (`claude-sonnet-4-5-20250929` not found).
*   **Architecture Appreciation:** Despite the bugs, users like Issue #1184 author praise the "minimalist approach" and "lightweight, secure alternative" to bloated agent frameworks, validating the core project vision.

## 8. Backlog Watch
*   **Issue #80 (Non-Claude Runtimes):** This remains the elephant in the room. With 47 upvotes and high anxiety regarding API bans, this requires a definitive roadmap update from maintainers.
*   **Issue #1224 (TOS Compliance):** A reopened discussion about replacing the Agent SDK with the official Claude Code CLI to avoid Terms of Service violations. This aligns with Issue #80 and needs architectural direction.
*   **Apple Container Networking:** Issue #1103 highlights a fundamental networking gap for macOS users that is not present in Docker Desktop, requiring a specific patch for Apple Container environments.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest: 2026-03-19

## 1. Today's Overview
NullClaw is demonstrating high project velocity with **33 Pull Requests** updated in the last 24 hours (27 merged/closed), signaling an intense focus on stabilization and feature expansion ahead of the recent v2026.3.17 release. Development activity is heavily skewed towards security hardening, observability, and platform support (Linux/NixOS), with a significant batch of "closed" issues indicating successful triage. The repository is highly active, transitioning rapidly from feature implementation (e.g., adaptive intelligence, encryption) to resolving integration bugs reported by early adopters of the new version.

## 2. Latest Releases
**v2026.3.17** (Released 2026-03-17)
*   **Observability:** Added OTLP support and runtime observability wiring by @DonPrus.
*   **Channels:** Introduced hardened external channel plugins.
*   **Maintenance:** Version bump PR #614.
*   **Impact:** This release focuses on enterprise readiness (tracing) and plugin stability.

## 3. Project Progress (Merged/Closed PRs)
The team merged a significant volume of code, focusing on security hygiene, service management, and agent reliability:
*   **Security & Secrets:**
    *   **(#538)** Implemented automatic secret key rotation (90-day cycle) for long-term security.
    *   **(#535)** Stopped logging pairing code secrets to prevent leakage in logs.
    *   **(#534)** Added a safety block for "yolo" autonomy mode on non-loopback gateways to prevent accidental exposure.
    *   **(#609)** Encrypted persisted API keys in `config.json`.
    *   **(#539)** Added audit warnings for wildcard allowlists.
*   **Platform & Tooling:**
    *   **(#605)** Added OpenRC support on Linux (service management).
    *   **(#541)** Fixed `http_request` tool to honor `http_timeout_secs` instead of hardcoding 60s.
    *   **(#598)** Improved cron diagnostics to help users debug why scheduled tasks aren't running.
*   **Agent Features:**
    *   **(#571)** Implemented hot-reloading for config and skills (no restart required).
    *   **(#275)** Added per-agent workspace isolation for named agents.

## 4. Community Hot Topics
High engagement areas indicate user focus on provider diversity, advanced agent behavior, and integration stability:
*   **Adaptive Intelligence Pipeline** ([PR #527](https://github.com/nullclaw/nullclaw/pull/527))
    *   *Status:* Open.
    *   *Discussion:* A major proposed feature introducing a "post-turn quality loop" to allow the agent to learn from interactions. This signals a push towards self-improving agents.
*   **Max Messenger Support** ([Issue #607](https://github.com/nullclaw/nullclaw/issues/607)) - *Closed*
    *   *Discussion:* Community debated supporting a state-promoted messenger with encryption concerns. Consensus leaned towards "no" or caution due to lack of E2E encryption.
*   **Config Documentation** ([Issue #613](https://github.com/nullclaw/nullclaw/issues/613))
    *   *Status:* Open.
    *   *Feedback:* Users find the generated `config.json` descriptions lacking practical use cases and default values.

## 5. Bugs & Stability
Several bugs were reported and fixed today, though some regressions appeared in the latest release:
*   **[High Severity] Telegram API Error:** ([Issue #626](https://github.com/nullclaw/nullclaw/issues/626)) Users experiencing `TEXTDRAFT_PEER_INVALID` errors when the bot attempts to send draft messages.
*   **[High Severity] Matrix Integration:** ([Issue #606](https://github.com/nullclaw/nullclaw/issues/607)) - *Closed*. Multiple critical failures reported: no auto-accept invites, ignoring mentions, and filtering issues. (Note: Marked closed, likely deferred or fixed in pending commits).
*   **[Medium Severity] AIEOS Identity Loading:** ([Issue #625](https://github.com/nullclaw/nullclaw/issues/625)) Configuration files are parsed correctly, but the AIEOS identity is not being injected into the system prompt.
*   **[Medium Severity] NixOS Build Failure:** ([Issue #612](https://github.com/nullclaw/nullclaw/issues/612)) Build fails on `nixos-25.11` for v2026.3.15.
*   **[Fixed] Android/Termux Build:** ([Issue #339](https://github.com/nullclaw/nullclaw/issues/339)) - *Open*. Issues with `build.zig.zon` on Android (Termux).
*   **[Fixed] Session Dangling Pointer:** ([PR #500](https://github.com/nullclaw/nullclaw/pull/500)) Fixed a regression where `/bind <agent>` would fail silently.

## 6. Feature Requests & Roadmap Signals
Users are asking for better multimodal support and provider flexibility:
*   **Vision Pipeline:** ([Issue #624](https://github.com/nullclaw/nullclaw/issues/624)) Request to send images/files directly to agents with automatic base64 encoding for multimodal LLMs.
*   **Search Aggregation:** ([Issue #623](https://github.com/nullclaw/nullclaw/issues/623)) Request to add `ddgs` (DuckDuckGo) metasearch to the `web_search` tool.
*   **Wife-Safe Mode (Streaming):** ([Issue #618](https://github.com/nullclaw/nullclaw/issues/618)) Request for the bot to wait for a stream of messages (e.g., 4 rapid texts) before responding to all of them at once.
*   **Provider Support:**
    *   **Gemini CLI:** ([PR #628](https://github.com/nullclaw/nullclaw/pull/628)) Integration using ACP mode.
    *   **Novita AI:** ([PR #621](https://github.com/nullclaw/nullclaw/pull/621)) - *Merged*. Added as OpenAI-compatible provider.
    *   **Ollama Cloud:** ([PR #615](https://github.com/nullclaw/nullclaw/pull/615)) Bearer auth support for hosted Ollama instances.

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Configuration Complexity:** Newcomers are struggling with opaque config options ([Issue #613](https://github.com/nullclaw/nullclaw/issues/613)) and loading AIEOS identities ([Issue #625](https://github.com/nullclaw/nullclaw/issues/625)).
    *   **Error Reporting:** Generic `error.ApiError` messages are frustrating testers who cannot diagnose the root cause ([Issue #619](https://github.com/nullclaw/nullclaw/issues/619)).
    *   **Platform quirks:** Termux users and NixOS users are hitting build-environment specific bugs.
*   **Positive:** Users are actively requesting advanced features (Adaptive Intelligence, Vision), indicating strong engagement with the core capabilities.

## 8. Backlog Watch
Older issues that remain unresolved or have seen recent updates needing attention:
*   **[Feature] OS-Native Credential Management** ([Issue #193](https://github.com/nullclaw/nullclaw/issues/193)) - *Closed*: A request to use macOS Keychain/Linux secret managers instead of plaintext files (Status: Recently closed, likely implemented or declined).
*   **[Bug] Android Install Issues** ([Issue #339](https://github.com/nullclaw/nullclaw/issues/339)) - *Open*: Persistent issues with build scripts on Termux/Android since early March.
*   **[Feature] Add Custom Provider** ([Issue #117](https://github.com/nullclaw/nullclaw/issues/117)) - *Open*: Long-standing request (created Feb 25) regarding adding Claude model support; PR #615 attempts to address provider extensibility.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the **IronClaw Project Digest** for **2026-03-19**.

### 1. Today's Overview
The IronClaw project is experiencing a **high-velocity development cycle**, with a heavy emphasis on stabilizing the "Routines" (automation) engine and expanding LLM provider integrations. While no new release was published today, the repository shows significant churn with **50 issues and 43 PRs updated** in the last 24 hours. A major "Staging CI Review" batch (PR #1359) has flagged several **CRITICAL and HIGH severity issues** related to performance (N+1 schema generation) and security (prompt injection, DoS risks), indicating a strong focus on code quality and technical debt reduction alongside feature additions.

### 2. Releases
**No new releases** were published in the last 24 hours.

### 3. Project Progress
*   **Routines Engine "full_job" Lifecycle**: Significant progress has been made on fixing the lifecycle logic for `full_job` routines. PRs #1374 and #1373 (open/closed variants) address **Issue #1317**, ensuring routine runs stay active until linked worker jobs complete, rather than marking as "OK" immediately after dispatch.
*   **Relay Architecture**: PR #1254 (Open) proposes a shift from Server-Sent Events (SSE) pulling to **webhook push-based callbacks** for relay events, which would simplify the `RelayChannel` architecture.
*   **LLM Provider Expansion**: Integration work is ongoing or finalized for **Gemini OAuth** (PR #1356), **Aliyun BaiLian** (PR #1299), and **MiniMax M2.7** (PR #1357).
*   **Duplicate Event Fix**: PR #1275 (Open) aims to prevent duplicate LLM responses when routines are triggered by events, a necessary fix for stable automation workflows.

### 4. Community Hot Topics
*   **Critical Staging CI Review (PR #1359)**: This promotion PR has sparked the creation of 14+ new issues analyzing a single batch of code. It is currently the most active area of discussion, highlighting systemic concerns about performance and safety.
    *   *Related:* [Issue #1361 (CRITICAL: N+1 Schema Gen)](https://github.com/nearai/ironclaw/issues/1361) | [Issue #1364 (HIGH: Prompt Injection)](https://github.com/nearai/ironclaw/issues/1364)
*   **Routines "Bug Bash"**: Maintainer `henrypark133` is driving a focused effort to harden the Routines feature.
    *   *Related:* [Issue #1317 (Job Completion Tracking)](https://github.com/nearai/ironclaw/issues/1317) | [Issue #1318 (Concurrency Limits)](https://github.com/nearai/ironclaw/issues/1318)
*   **Web UI Settings Gap**: User `ilblackdragon` has highlighted a significant UX gap where a robust Settings API exists but is exposed in the Web UI.
    *   *Related:* [Issue #1346 (Settings Tab Request)](https://github.com/nearai/ironclaw/issues/1346) | [Issue #1345 (Approval Rules)](https://github.com/nearai/ironclaw/issues/1345)

### 5. Bugs & Stability
**Severity: CRITICAL**
*   **[Issue #1361]** **N+1 Schema Generation:** The `Tool::schema()` call triggers regeneration on every LLM call. This creates a massive performance bottleneck identified by CI with 100% confidence.

**Severity: HIGH**
*   **[Issue #815]** **Token Budget Bypass:** User-supplied metadata can bypass configured token budgets, posing a resource exhaustion risk.
*   **[Issue #1364]** **Prompt Injection:** Routine prompts may fail to escape channel/user data, leading to injection vulnerabilities.
*   **[Issue #1287]** **Unbounded Retry-After:** The code accepts any `u64` value for HTTP Retry-After durations, potentially allowing DoS attacks via extremely long wait times.
*   **[Issue #1318]** **Concurrency Guardrail Failure:** `full_job` routines can bypass global concurrency limits because they are tracked based on dispatch time rather than actual job completion. (Fix: PR #1372).
*   **[Issue #1317]** **Premature Job Status:** `full_job` routines report success immediately after dispatch, ignoring the actual result of the linked job. (Fix: PR #1374).

**Severity: MEDIUM**
*   **[Issue #1205]** **Slack Tool Install Failure:** The tool is failing to download, returning HTTP 404.
*   **[Issue #1303]** **WASM Tool Schema Mismatch:** WASM tools exporting typed schemas are incorrectly advertised as permissive `{}` schemas to the LLM, leading to tool misuse. (Fix: PR #1348).

### 6. Feature Requests & Roadmap Signals
*   **Settings & Approval UI**: Users are strongly requesting a **Settings tab** in the Web Gateway to manage configurations and **persistent approval rules** (Issues #1346, #1345).
*   **Provider Hot-Reload**: Request to change LLM providers via the Web UI without restarting the process (Issue #1350).
*   **Routine Self-Recovery**: Request to add bounded retry logic for transient failures in routines to prevent immediate failure visible to the user (Issue #1320).
*   **SSO/OAuth Improvements**: High interest in better authentication flows, specifically Google Gemini OAuth integration (PR #1356) and fixing flaky OAuth tests (Issue #1280).

### 7. User Feedback Summary
*   **Positive**: A detailed guide (Issue #1347) shows users successfully deploying IronClaw as a **24/7 Telegram bot** on Ubuntu, proving the stability of the Telegram channel integration.
*   **Pain Points**:
    *   **Tool Discovery**: Issues #1333, #1335, and #1336 suggest that LLMs struggle to understand the complex semantics of tools like `create_job` and `time` because the schemas are either flat or lack contextual routing data.
    *   **Settings Friction**: Users are frustrated that they cannot configure "Always Allow" rules persistently or change LLM providers without a restart.

### 8. Backlog Watch
*   **Issue #605**: Test coverage for rate limiting (`rate_limit_cascade`) has been open since early March and is only just now seeing a fix attempt (PR #1358), indicating a lag in test coverage maintenance.
*   **Issue #1103**: SSRF (Server-Side Request Forgery) risk via embedding URLs remains open and unaddressed.
*   **Issue #1215**: Lack of `debug_assert!` invariants in critical code paths suggests a technical debt item that improves developer confidence (Fix in PR #1354).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Daily Digest
**Date:** 2026-03-19 | **Source:** github.com/netease-youdao/LobsterAI

## 1. Today's Overview
LobsterAI is currently in a highly active development phase, characterized by heavy refactoring of the backend architecture (specifically the migration to OpenClaw plugins) and a rapid release cadence. The project saw significant maintenance activity with 10 Pull Requests merged/closed, addressing critical stability issues in the gateway and scheduling systems. However, this aggressive update cycle appears to have introduced regressions for some users, as evidenced by a spike in new issues (13 in the last 24h) regarding settings loss and runtime crashes. The community is actively discussing the integrity of "forked" versions of the software, highlighting LobsterAI's growing popularity and influence in the AI agent space.

## 2. Releases
*No new releases published in the last 24 hours.* (Note: Issues reference 2026.3.16 and 2026.3.17 versions, indicating frequent recent updates).

## 3. Project Progress
**Core Architecture & Integration:**
*   **[Merged] #473:** Migrated the NetEase IM (NIM) gateway from a direct SDK implementation to the **OpenClaw plugin architecture**. This aligns NIM with other channels (DingTalk, Feishu, Telegram, etc.) and likely improves maintainability.
*   **[Merged] #471:** Replaced the `AGENTS.md` embedded method with **OpenClaw native Skills loading**, streamlining how agent capabilities are defined and loaded.

**Stability & Fixes:**
*   **[Merged] #487:** Fixed a critical UI freeze issue where modifying IM configuration during an active `cowork` session would cause the interface to hang permanently.
*   **[Merged] #484 & #486:** Implemented logic to restart the `openclaw gateway` upon failure and ensured configuration changes only trigger a restart when explicitly saved.
*   **[Merged] #477:** Fixed **scheduled task migration** issues. Specifically, it appended local timezone offsets to legacy `at` tasks to prevent an 8-hour time drift for UTC+8 users and handled tasks scheduled in the past.

**Dependencies & Models:**
*   **[Merged] #388:** Upgraded the default **MiniMax model to M2.7** (from M2.5) and updated the API endpoint.
*   **[Merged] #482:** Upgraded dependencies related to **WeCom** (WeChat Work).

## 4. Community Hot Topics
*   **[Issue #435] "Is this a wrapper? Interface highly similar"**
    *   **Link:** [netease-youdao/LobsterAI#435](https://github.com/netease-youdao/LobsterAI/issues/435)
    *   **Discussion:** Users are debating whether several competing tools ("Wind Claw", "Zeelin Claw") are unauthorized "skins" or forks of LobsterAI due to identical UI elements.
    *   **Analysis:** This signals that LobsterAI has established a de-facto standard UI for AI agents in China. It highlights a need for brand protection and clear licensing communication from the maintainers.

*   **[Issue #485] "Display context usage, compression, and thought process"**
    *   **Link:** [netease-youdao/LobsterAI#485](https://github.com/netease-youdao/LobsterAI/issues/485)
    *   **Discussion:** Users want visibility into Token usage (e.g., "120k/200k used") and visual feedback during "context compression" to distinguish between UI freezes and actual processing.
    *   **Analysis:** As context windows grow, "Token anxiety" is real. This is a high-value UX request for power users managing long-running agent tasks.

*   **[Issue #382] "Settings reset on every update"**
    *   **Link:** [netease-youdao/LobsterAI#382](https://github.com/netease-youdao/LobsterAI/issues/382)
    *   **Discussion:** Users are frustrated that frequent updates (e.g., 2026.3.16/17) require manual re-entry of all settings.
    *   **Analysis:** This indicates a regression in the configuration migration logic or an aggressive update strategy that is disrupting user workflows.

## 5. Bugs & Stability
*   **[CRITICAL] Gateway Instability:**
    *   **Issue #490:** Reports of `OpenClaw` repeatedly crashing and restarting during task execution (Version 2026.3.17). This breaks long-running agent tasks.
    *   **Fix Status:** PR #484 (merged) added restart capabilities, which may mitigate but implies underlying instability.
*   **[HIGH] Scheduled Task Data Loss:**
    *   **Issue #474:** Users reported that previous scheduled tasks disappeared after installing the 2026.3.16 version, and the Sandbox/Local setting options vanished.
    *   **Fix Status:** PR #477 (merged) explicitly addresses "legacy task migration," suggesting this was a known migration bug being fixed.
*   **[MEDIUM] Linux AppImage Errors:**
    *   **Issue #481:** Ubuntu 20.04 users facing shared memory access errors (`/tmp: No such file or directory`).
*   **[MEDIUM] Node.js Compatibility:**
    *   **Issue #476:** `npm install` fails on Ubuntu 22 with Node v24.1.0 due to a `null` reading error.

## 6. Feature Requests & Roadmap Signals
*   **Telegram Bot Support:** Requested in **[Issue #478](https://github.com/netease-youdao/LobsterAI/issues/478)**.
    *   *Signal:* High interest. The codebase already references Telegram in the plugin architecture (PR #473), suggesting this might be technically close or available but not yet user-facing.
*   **Manual Context Compression:** Requested in **[Issue #485](https://github.com/netease-youdao/LobsterAI/issues/485)** (manual trigger like Claude Code).
*   **Custom Model API Support:** **[Issue #492](https://github.com/netease-youdao/LobsterAI/issues/492)** asks if `openai-responses` format APIs are supported.

## 7. User Feedback Summary
*   **Pain Points:** The rapid release cycle is causing "update fatigue." Users are annoyed by settings resets (**#382**) and disappearing tasks (**#474**).
*   **Cost Concerns:** **[Issue #480](https://github.com/netease-youdao/LobsterAI/issues/480)** highlights that the system sends full system instructions on every new chat turn, "burning tokens" unnecessarily.
*   **Security/Safety Fears:** **[Issue #489](https://github.com/netease-youdao/LobsterAI/issues/489)** shows the agent attempting to execute "dangerous" commands (e.g., `rm -rf`), triggering user alarm about sandboxing efficacy.

## 8. Backlog Watch
*   **[Issue #124] Local Mode vs. Sandbox Mode:** Open since Feb 26. Users getting API errors in Local mode while Sandbox works fine. Needs investigation into authentication flow differences.
*   **[Issue #388] Model Upgrades:** While PR #388 was merged for MiniMax M2.7, the broader support for other custom models remains a discussion point in Issue #492.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Digest: 2026-03-19

## 1. Today's Overview
TinyClaw has undergone a massive transformation today, rebranding to **TinyAGI** with the release of v0.0.15. Development velocity is extremely high, with 13 pull requests updated in the last 24 hours (11 merged/closed, 2 open). The project appears to be in a consolidation phase, simplifying its architecture and standardizing installation methods following the rebrand. While no new issues were reported, the closure of multiple architectural PRs suggests a strong push towards stability and a streamlined developer experience.

## 2. Releases
### **v0.0.15 (TinyAGI)**
*   **Breaking Changes**: Complete rebrand from `TinyClaw` to `TinyAGI`. This includes renaming package names (`@tinyclaw/*` → `@tinyagi/*`), environment variables, CLI commands, and configuration directories (`~/.tinyclaw` → `~/.tinyagi`).
*   **Migration**:
    *   **Data Migration**: Automated scripts have been introduced to migrate user data and databases from the old `~/.tinyclaw` directory to `~/.tinyagi`.
    *   **Installation**: The default installation method is now a one-liner `curl` command. The `npx` installation method has been demoted to an alternative option.
*   **Architectural Refactoring**: The `packages/tinyagi` package has been merged into `packages/cli`, making `tinyagi` (Node.js) the primary CLI entrypoint.

## 3. Project Progress
*   **Rebranding & Consolidation**: The core project identity has shifted to TinyAGI. The codebase successfully merged internal packages ([#238](https://github.com/TinyAGI/tinyagi/pull/238)) and finalized the directory structure migration ([#191](https://github.com/TinyAGI/tinyagi/pull/191)).
*   **Installation UX**: Significant improvements were made to the installation workflow. The `curl` script is now the standard ([#237](https://github.com/TinyAGI/tinyagi/pull/237)), fixing issues with environment variable shadowing and ensuring symlinks are created correctly.
*   **Agent Intelligence**: A hierarchical memory system was finalized, allowing agents to save and recall knowledge across conversations using Markdown and YAML ([#209](https://github.com/TinyAGI/tinyagi/pull/209)).
*   **Queue Simplification**: The internal queue logic was flattened to remove conversation state tracking, opting for direct DMs with immediate response streaming ([#213](https://github.com/TinyAGI/tinyagi/pull/213)).

## 4. Community Hot Topics
*   **Preventing Agent Feedback Loops** ([#220](https://github.com/TinyAGI/tinyagi/pull/220))
    *   **Status**: Open
    *   **Analysis**: A critical bug was identified where multi-agent teams entered exponential feedback loops due to "fan-out" messaging. This PR aims to remove chatroom fan-out to prevent agents from triggering each other in a loop. It highlights the complexity of multi-agent orchestration.

*   **Periodic Memory Maintenance** ([#233](https://github.com/TinyAGI/tinyagi/pull/233))
    *   **Status**: Open
    *   **Analysis**: The community is looking to automate agent "reflection." This PR proposes triggering memory consolidation via the existing heartbeat cron job, suggesting a need for agents to autonomously manage their own knowledge growth without user intervention.

## 5. Bugs & Stability
*   **Installation Regression (Data Loss Risk)**:
    *   **Severity**: High (addressed in v0.0.15)
    *   **Fix**: [PR #239](https://github.com/TinyAGI/tinyagi/pull/239) and [#236](https://github.com/TinyAGI/tinyagi/pull/236).
    *   **Details**: During the rebrand, users upgrading from older versions risked losing their data if the directory wasn't migrated. Fixes were implemented to automatically migrate `~/.tinyclaw` to `~/.tinyagi` and rename database files on startup.
*   **Multi-Agent Instability**:
    *   **Severity**: Medium (Fix Pending)
    *   **Issue**: [PR #220](https://github.com/TinyAGI/tinyagi/pull/220).
    *   **Details**: Reports of agents in teams causing infinite loops or rapid API credit consumption due to recursive messaging.

## 6. Feature Requests & Roadmap Signals
*   **Web-Based Configuration**: The recent merge of [PR #214](https://github.com/TinyAGI/tinyagi/pull/214) indicates a roadmap priority on decoupling the setup process from the CLI. Users can expect a "TinyOffice" web interface for managing API keys and connections, rather than editing config files manually.
*   **Streaming Output**: The merge of [PR #196](https://github.com/TinyAGI/tinyagi/pull/196) confirms that real-time feedback of agent execution is a core requirement, likely leading to more responsive UI tools in the future.

## 7. User Feedback Summary
*   **Pain Points**: The rebrand caused potential friction for existing users regarding data preservation. The rapid closure of installation-related PRs indicates the team is prioritizing a "zero-config" onboarding experience.
*   **Use Cases**: The focus on memory systems and multi-agent loop prevention suggests users are deploying TinyAGI in complex, long-running tasks where context retention and agent stability are paramount.

## 8. Backlog Watch
*   **[PR #220](https://github.com/TinyAGI/tinyagi/pull/220) (Agent Feedback Loops)**: As of this digest, this remains open. Given the stability risk, this is likely the top priority for the next patch release.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest: 2026-03-19

**Today's Overview**
On March 19, 2026, the Moltis project demonstrates active maintenance focused on stability and web interaction reliability. Development activity is currently concentrated on resolving critical bugs related to legacy character encoding and network proxies. Although no new releases were published today, the submission of Pull Request #450 indicates a swift response to recent tooling failures. The repository shows 1 active issue and 1 open pull request updated in the last 24 hours, reflecting a targeted effort to polish the `web_fetch` and `web_search` capabilities.

## Latest Releases
*No new releases published on 2026-03-19.*

## Project Progress
*No pull requests were merged or closed today.* However, significant progress is represented in the open PR queue:
*   **[PR #450](https://github.com/moltis-org/moltis/pull/450)**: A fix has been submitted to address `web_fetch` panics. This PR targets a root cause where the system attempted to slice strings at arbitrary byte positions, leading to crashes on pages encoded in GBK, GB18030, or Big5.

## Community Hot Topics
*   **[#407: Network-filter Proxy failing / web_search broken](https://github.com/moltis-org/moltis/issues/407)**
    *   **Activity:** Updated on March 18; 1 comment.
    *   **Analysis:** This is the primary active discussion point. The user reports that the web_search function is inoperable due to an immediate proxy failure at startup. This suggests a potential regression in network configuration handling or an environmental dependency issue that is blocking core functionality for users relying on web integration.

## Bugs & Stability
*   **High Severity:** **[#407: Network-filter Proxy failing](https://github.com/moltis-org/moltis/issues/407)**
    *   **Description:** The `web_search` tool fails right after startup due to a proxy error.
    *   **Impact:** High; renders a core agent feature (web access) unusable.
    *   **Status:** Open; no linked fix PR yet.
*   **High Severity:** **[#420: `web_fetch` panic on non-UTF8 pages](https://github.com/moltis-org/moltis/issues/420)** (Referenced in PR #450)
    *   **Description:** The application crashes with "byte index is not a char boundary" when fetching legacy encoded pages.
    *   **Impact:** High; causes agent crashes (panic).
    *   **Status:** **Fix Available** in [PR #450](https://github.com/moltis-org/moltis/pull/450).

## Feature Requests & Roadmap Signals
*   **Improved Encoding Support:** The submission of PR #450 highlights a clear need for robust internationalization support. While technically a bug fix, addressing the panic on legacy encodings (GBK, GB18030, Big5) signals a roadmap priority for global stability and non-English web scraping.

## User Feedback Summary
*   **Pain Points:** Users are experiencing instability with web-based tools. The feedback highlights two distinct breakdowns: a startup failure preventing network access (Issue #407) and a runtime crash when accessing specific types of web content (Issue #420).
*   **Satisfaction:** Dissatisfaction is likely high among users requiring web search capabilities, as the tool appears currently broken or unstable depending on the target website's encoding.

## Backlog Watch
*   **[Issue #407](https://github.com/moltis-org/moltis/issues/407)**: While recently updated, this issue regarding the "Network-filter Proxy" requires immediate maintainer attention as it represents a total failure of the `web_search` functionality for the reporter. Investigating the root cause (config vs. code) should be prioritized to prevent user churn.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest: 2026-03-19

## 1. Today's Overview
CoPaw is demonstrating exceptionally high development velocity as it approaches the v0.1.0 release milestone, with **50 issues and 50 pull requests** updated in the last 24 hours. The project has successfully released **v0.1.0-beta.3**, focusing heavily on stabilizing the console UI, integrating local model capabilities, and enabling multimodal features (vision/file upload). Community engagement is robust, characterized by a high volume of bug reports regarding local model configurations (Ollama, llama.cpp) and feature requests for enhanced security and memory management.

## 2. Releases
*   **[v0.1.0-beta.3](https://github.com/agentscope-ai/CoPaw/releases/tag/v0.1.0-beta.3)**
    *   **Summary:** The third beta for the upcoming v0.1.0 release.
    *   **Key Changes:**
        *   Multi-language support updates in the web console.
        *   Optimizations for document navigation anchors in the UI.

## 3. Project Progress (Merged/Closed PRs)
*   **[PR #1783](https://github.com/agentscope-ai/CoPaw/pull/1783) (Closed):** Added support for the `streamable-http` transport type, addressing connectivity issues with certain MCP servers.
*   **[PR #1772](https://github.com/agentscope-ai/CoPaw/pull/1772) (Closed):** A major feature merge implementing **multimodal message support**, enabling image and file uploads directly in the web console. This resolves issues #636, #509, #1649, and others.
*   **[PR #1729](https://github.com/agentscope-ai/CoPaw/pull/1729) (Closed):** Upgraded the default MiniMax model to **M2.7** for improved performance.
*   **[PR #1557](https://github.com/agentscope-ai/CoPaw/pull/1557) (Closed):** Fixed a sequential injection bug for `reasoning_content` in the model formatter, preventing API request mismatches.
*   **[PR #1702](https://github.com/agentscope-ai/CoPaw/pull/1702) (Closed):** Updated `reme-ai` dependency to v0.3.0.8 to ensure compatibility with the memory manager.

## 4. Community Hot Topics
*   **[#1385 CPU Occupancy 100% Bug](https://github.com/agentscope-ai/CoPaw/issues/1385) (9 comments):** The most active discussion revolves around a critical bug where CoPaw's CPU usage hits 100% on Ubuntu 25.10. The user identified `mcp` and `read_file` as potential triggers and submitted a fix.
*   **[#1782 Model Configuration Error](https://github.com/agentscope-ai/CoPaw/issues/1782) (8 comments):** Users reported that after upgrading, local models (llama.cpp, Ollama) disappeared from defaults and threw "code 400" errors. Fixed in [PR #1788](https://github.com/agentscope-ai/CoPaw/pull/1788).
*   **[#430 Help Wanted](https://github.com/agentscope-ai/CoPaw/issues/430) (7 comments):** The official "Good First Issue" tracker remains a hub for community contribution efforts.

## 5. Bugs & Stability
*   **[Critical: Memory Search Failure](https://github.com/agentscope-ai/CoPaw/issues/1736):** `MemoryManager` fails to initialize `file_stores` because `start()` isn't called, breaking memory search functionality.
*   **[High: File Write Truncation](https://github.com/agentscope-ai/CoPaw/issues/1563):** The `write_file` tool truncates content, only writing partial data (e.g., 19% of a 33KB file).
*   **[Medium: UI Layout Issues](https://github.com/agentscope-ai/CoPaw/issues/1704):** Model selection dropdowns in the chat interface are obscured/cut off, hindering usability.
*   **[Medium: Model Registry Errors](https://github.com/agentscope-ai/CoPaw/issues/1727):** Specific Ollama models (e.g., `qwen3.5:4b`) return errors stating they do not support tools.

## 6. Feature Requests & Roadmap Signals
*   **Local Embeddings:** [PR #1789](https://github.com/agentscope-ai/CoPaw/pull/1789) is open, proposing local embedding models (BGE, Qwen3-VL) for long-term memory to enable fully offline vector search.
*   **Authentication & Security:** There is a strong signal from multiple issues ([#492](https://github.com/agentscope-ai/CoPaw/issues/492), [#333](https://github.com/agentscope-ai/CoPaw/issues/333)) requesting built-in password protection for the Web UI. [PR #1719](https://github.com/agentscope-ai/CoPaw/pull/1719) proposes setting credentials via environment variables for automated deployment.
*   **Execution Logs:** Users are requesting detailed execution chain logs ([#1474](https://github.com/agentscope-ai/CoPaw/issues/1474)) to better debug agent workflows.
*   **Token Statistics:** Request for session-based token consumption tracking ([#1751](https://github.com/agentscope-ai/CoPaw/issues/1751)).

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Local Model Setup:** Users are struggling significantly with configuring local providers (llama.cpp, Ollama, MLX), often facing "Unknown agent errors" or missing configurations post-update.
    *   **UI/UX Friction:** The console UI is receiving criticism for layout issues (dropdowns obscured) and missing basic features like image uploads (addressed in v0.1.0-beta.3) and chat history persistence.
    *   **Stability:** The 100% CPU bug and file truncation issues are causing frustration among users attempting file-heavy workflows.
*   **Positive Reception:** The rapid closure of issues regarding image uploads and multimodal support suggests the dev team is highly responsive to core feature gaps.

## 8. Backlog Watch
*   **[#676 HTTP MCP Support](https://github.com/agentscope-ai/CoPaw/issues/676):** Users want to use HTTP-based MCP servers (e.g., DingTalk), but the current implementation returns "Unprocessable Entity" errors despite recent PRs attempting to fix `streamable-http`.
*   **[#492 Web UI Authentication](https://github.com/agentscope-ai/CoPaw/issues/492):** A request for basic login/password protection has been open since March 3rd with increasing community demand, indicating security is a priority for public deployment.
*   **[#1381 Model Selection UI](https://github.com/agentscope-ai/CoPaw/issues/1381):** The model switching UI is reported as broken (display cutoff), severely impacting usability on smaller screens.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest: 2026-03-19

**1. Today's Overview**
ZeptoClaw is currently in an active development phase characterized by architectural security evolution and infrastructure hardening. While no new releases were published today, the project shows high engagement with 3 issues and 2 pull requests updated in the last 24 hours. The core focus appears to be shifting towards securing the execution environment (via Firecracker VMs) and standardizing the developer toolchain. Activity levels are healthy, with critical bugs related to HTTP protocol semantics and container permissions being addressed alongside new feature integrations for Google Vertex AI.

**2. Releases**
No new releases published today.

**3. Project Progress**
**Merged & Closed Items:**
*   **Fixed Container Permissions:** [Issue #369](https://github.com/qhkm/zeptoclaw/issues/369) was successfully closed. This PR resolved a `permission denied` error for Cargo in the `lint-container.sh` script when running rootless Podman. The fix involved remounting the registry cache to a writable user location (`/cargo-home`), improving the stability of CI and local development environments.

**In-Progress Features:**
*   **Google Vertex AI Integration:** [PR #364](https://github.com/qhkm/zeptoclaw/pull/364) advanced today, adding a first-class provider for Google Gemini models with enterprise-grade bearer token authentication.
*   **Developer Tooling:** [PR #287](https://github.com/qhkm/zeptoclaw/pull/287) received updates, aiming to provide a consistent pre-PR state for contributors to ensure tests and linters pass locally before submission.

**4. Community Hot Topics**
*   **Architectural Shift to MicroVMs:** [Issue #387](https://github.com/qhkm/zeptoclaw/issues/387) is the most discussed item (4 comments). It proposes a controversial but significant architectural shift: mapping core templates to Firecracker VMs.
    *   *Analysis:* The community is debating the trade-offs between complexity and security. The underlying need is to treat "Coding Agent Frameworks" (like Claude-code or Copilot-cli) as isolated apps rather than expanding the host's security surface, signaling a push towards a more secure, multi-tenant agent architecture.

**5. Bugs & Stability**
*   **Protocol Logic Error (High Severity):** [Issue #388](https://github.com/qhkm/zeptoclaw/issues/388) reports critical bugs in the ACP HTTP implementation introduced in PR #356.
    *   *Details:* The initialization flag is global rather than session-specific, allowing new clients to bypass handshakes. Additionally, HTTP notifications are incorrectly receiving response bodies intended for prompts.
    *   *Status:* No fix PR is linked yet; this requires immediate attention to prevent protocol violations in production.
*   **Rootless Container Permissions (Fixed):** The bug preventing non-root users from writing to `/usr/local/cargo` in Rust slim images (Issue #369) has been resolved.

**6. Feature Requests & Roadmap Signals**
*   **Virtualized Core Templates:** The proposal in [Issue #387](https://github.com/qhkm/zeptoclaw/issues/387) suggests a roadmap direction toward "hardened isolation." If accepted, future versions of ZeptoClaw will likely rely on Containerfiles and Firecracker VMs to execute untrusted agent code.
*   **Google Vertex AI Support:** With [PR #364](https://github.com/qhkm/zeptoclaw/pull/364) open, the roadmap explicitly includes support for enterprise Google Cloud workflows, moving beyond standard API keys to bearer token auth.

**7. User Feedback Summary**
*   **Pain Points:** Users and contributors are experiencing friction with inconsistent development environments (prompting PR #287) and security concerns regarding the ever-expanding attack surface of running multiple coding agents directly on the host or standard containers.
*   **Satisfaction:** There is positive reception to the closing of Issue #369, indicating that rootless container workflows are important to the user base.

**8. Backlog Watch**
*   **Long-Standing Dev Tools:** [PR #287](https://github.com/qhkm/zeptoclaw/pull/287) was created on March 9th but remains open. This indicates a backlog item regarding the "boring" but essential infrastructure needed to smooth out contributor onboarding and reduce CI friction.
*   **Security Architecture Debate:** [Issue #387](https://github.com/qhkm/zeptoclaw/issues/387), while newer, represents a significant backlog decision point regarding whether to adopt Firecracker VMs, which will require substantial engineering effort if approved.

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw (RivonClaw) Project Digest
**Date:** 2026-03-19
**Repo:** [gaoyangz77/easyclaw](https://github.com/gaoyangz77/easyclaw) (Target Repo: [gaoyangz77/rivonclaw](https://github.com/gaoyangz77/rivonclaw))

---

### 1. Today's Overview
The EasyClaw project (now branding primarily as **RivonClaw**) has shown aggressive release activity, shipping three minor versions (v1.6.8, v1.7.0, v1.7.1) within a short window to address platform-specific stability issues. Today's maintenance activity was high, with the team successfully closing 4 issues and 1 Pull Request, indicating a responsive "crunch" mode to resolve connectivity regressions reported by Windows users. While the macOS platform is receiving polish for system integration (Dock/Tray icons), the Windows environment is currently suffering from critical connectivity failures preventing users from utilizing the application.

### 2. Releases
**New Releases: v1.6.8, v1.7.0, v1.7.1**
*   **Branding Shift:** The release notes identify the application as **"RivonClaw"**, suggesting a formal rebrand or fork evolution from the "EasyClaw" repository name.
*   **Platform Focus:** All recent releases include specific installation instructions for macOS, addressing Gatekeeper warnings ("'RivonClaw' is damaged...") which implies the builds are currently unsigned. This suggests the project is in a rapid deployment phase where code signing may be deferred for speed.
*   **Windows Hotfixes:** The rapid progression from v1.6.8 to v1.7.1 likely corresponds to the critical Windows connection issues reported in the issues section.

### 3. Project Progress
*   **UI/System Integration (macOS):**
    *   PR #15 "fix: app icon in macos dock and system tray" was merged/closed. This resolves visual inconsistencies in the macOS interface, improving the professional feel of the desktop client.
*   **Connectivity & Stability (Windows):**
    *   Issues #18 and #19 regarding Windows connection failures have been closed. This suggests fixes were deployed in the v1.7.x series, though user confirmation in the comments was pending at the time of the last data sync.

### 4. Community Hot Topics
*   **Critical Windows Connectivity Failure ([#19](https://github.com/gaoyangz77/rivonclaw/issues/19)):**
    *   *Activity:* 3 comments.
    *   *Context:* Users upgrading to v1.7.0 on Windows 11 faced a complete blockage ("stuck on connecting").
    *   *Underlying Need:* Users require a reliable first-launch experience. The frustration was high as reconfiguring API keys and registering accounts did not resolve the issue, pointing to a deep system-level regression in the Windows build.
*   **Community Engagement ([#12](https://github.com/gaoyangz77/rivonclaw/issues/12)):**
    *   *Activity:* 3 comments.
    *   *Context:* Users requested a technical exchange group, praising the project architecture.
    *   *Underlying Need:* There is strong developer interest in the project's architecture. The maintainers should consider establishing a Discord or Telegram channel to foster community growth and allow for real-time debugging support.

### 5. Bugs & Stability
**Severity: High**
*   **Windows Connection Regression:**
    *   Multiple users reported that upgrading from v1.6.8 to v1.7.0 broke the application's ability to connect to the backend/API ([#18](https://github.com/gaoyangz77/rivonclaw/issues/18), [#19](https://github.com/gaoyangz77/rivonclaw/issues/19)).
    *   *Status:* Issues have been closed (presumably fixed in v1.7.1), but this represents a significant instability in the v1.7.0 release cycle.
*   **macOS Signing Warnings:**
    *   The binary triggers Gatekeeper warnings requiring terminal commands to bypass.
    *   *Status:* Acknowledged in documentation, but a friction point for less technical users.

### 6. Feature Requests & Roadmap Signals
*   **Windows Development Documentation:**
    *   Issue #17 requested a "Windows version startup and packaging tutorial."
    *   *Signal:* There is interest in contributing to or porting the project to Windows, but the build process is opaque. Creating a `CONTRIBUTING.md` or build guide for Windows would lower the barrier to entry for external contributors.
*   **Community Channel:**
    *   Request for a group chat ([#12](https://github.com/gaoyangz77/rivonclaw/issues/12)) suggests the user base is growing beyond what GitHub Issues can efficiently manage.

### 7. User Feedback Summary
*   **Pain Points:** The primary frustration today is **instability on Windows**. The v1.7.0 release appears to have been a "hot mess" for Windows users, rendering the app unusable (stuck on connecting screen) despite having valid credentials.
*   **Satisfaction:** Despite the bugs, user intent remains high. Users are willing to debug API keys and re-install to get it working, and one user explicitly praised the "project architecture," indicating technical appreciation for the software design.

### 8. Backlog Watch
*   **Build Transparency:** The request for a Windows packaging tutorial ([#17](https://github.com/gaoyangz77/rivonclaw/issues/17)) remains unanswered (closed without a visible solution provided in the summary). Addressing this documentation gap is recommended to prevent maintainer burnout from repeated build questions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*