# OpenClaw Ecosystem Digest 2026-03-19

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-03-19 01:23 UTC

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
OpenClaw is experiencing an exceptionally high surge in development activity, with **500 issues and 500 pull requests updated in the last 24 hours**. Despite this massive volume, project velocity appears healthy; there are ~5x more active issues than closed ones, but the Pull Request merge rate is robust (~19% of updated PRs were merged/closed). The project is in a feature-heavy phase, with significant contributions focused on multi-agent memory, external tool integrations, and platform-specific client fixes.

## 2. Latest Releases
No new releases were published today.

## 3. Project Progress
*Major Features Advancing:*
*   **Cortex Memory Integration:** PR #44421 remains active, aiming to integrate Cortex as a local memory substrate. This is a major architectural shift, moving from simple session history to persistent, structured memory.
*   **Native MCP Support:** Discussion continued in Issue #29053 regarding native Model Context Protocol (MCP) support, indicating strong community demand for standardized external tool connectivity.
*   **Multi-Agent Framework:** PR #48838 is actively developing agent-scoped skill policies and cron agent semantics, essential for complex multi-agent deployments.

*Infrastructure & Tooling:*
*   **Configuration Management:** PR #49841 introduces Nacos as a configuration source, facilitating centralized config for Kubernetes environments.
*   **Search Providers:** PR #50033 adds "Parallel" as a new search/fetch provider, offering LLM-optimized search results.

## 4. Community Hot Topics
*   **Internationalization (i18n):**
    *   [Issue #3460](https://github.com/openclaw/openclaw/issues/3460) (103 comments): The most discussed item is the lack of internationalization support. The core team cites bandwidth constraints as the blocker, but community demand is massive.
*   **Desktop Apps Expansion:**
    *   [Issue #75](https://github.com/openclaw/openclaw/issues/75) (63 reactions): There is a strong push for official Linux and Windows GUI apps ("Clawdbot"), similar to the existing macOS/iOS/Android offerings.
*   **Phishing Security Alert:**
    *   [Issue #49836](https://github.com/openclaw/openclaw/issues/49836) (28 comments): A critical warning about a fake repository targeting OpenClaw users with wallet-draining phishing scams.
*   **DingTalk Integration:**
    *   [Issue #26534](https://github.com/openclaw/openclaw/issues/26534) (74 comments): Users want DingTalk available as a first-install option during setup, rather than requiring manual configuration later.

## 5. Bugs & Stability
*Critical Instability (High Severity):*
*   **Gateway Restarts:** [Issue #48205](https://github.com/openclaw/openclaw/issues/48205) (20 comments) reports gateways restarting every ~50 minutes for unknown reasons, causing service interruptions.
*   **WhatsApp Desync:** [Issue #34741](https://github.com/openclaw/openclaw/issues/34741) (18 comments) highlights a regression where WhatsApp reports "No active listener" despite status being connected, breaking messaging mid-session.
*   **Heartbeat Failures:** [Issue #45772](https://github.com/openclaw/openclaw/issues/45772) (18 comments) notes that the gateway heartbeat timer stops after 1-2 triggers, causing permanent failures.
    *   *Fix Status:* PR #47433 and #44984 are addressing the root cause (singleton/map duplication in WhatsApp listeners) and should resolve these stability issues.

*Regressions:*
*   **CLI Handshake:** [Issue #45560](https://github.com/openclaw/openclaw/issues/45560) and [Issue #48167](https://github.com/openclaw/openclaw/issues/48167) describe frequent "gateway closed (1000)" errors even when the gateway is running, linked to aggressive 3-second timeouts.
*   **Tool Execution:** [Issue #36994](https://github.com/openclaw/openclaw/issues/36994) (17 comments) reports that exec tools and browser control break repeatedly after the first run.

## 6. Feature Requests & Roadmap Signals
*   **External Memory API:** [Issue #49233](https://github.com/openclaw/openclaw/issues/49233) proposes an "External Memory Provider API" to allow zero-downtime context compaction, solving the current 30-60s agent blackout during memory management.
*   **ClawAPI Provider:** PR #47809 proposes adding "ClawAPI" as a built-in provider, offering a crypto-native multi-model gateway to simplify provider configuration.
*   **Search Fallbacks:** [Issue #16629](https://github.com/openclaw/openclaw/issues/16629) notes that Brave Search API is no longer free, requiring the project to integrate alternatives like DuckDuckGo or Tavily.

## 7. User Feedback Summary
*   **Pain Point - Cost Visibility:** Users are frustrated by inaccurate token cost reporting. Issues #49917 and #50083 highlight that cached tokens are either showing 0% usage or $0.00 cost, leading to surprise bills.
*   **Pain Point - Setup/Onboarding:** New users are stumbling on the "Gateway never becomes ready" step on macOS [Issue #6156](https://github.com/openclaw/openclaw/issues/6156) and installation failures on Ubuntu [Issue #39447](https://github.com/openclaw/openclaw/issues/39447).
*   **UX Issue - "Thought" Leakage:** [Issue #25592](https://github.com/openclaw/openclaw/issues/25592) describes internal agent "thinking" text leaking into public channels (Slack/iMessage) during tool use, which is considered a significant UX failure.

## 8. Backlog Watch
*   **Binding Issues:** [Issue #4947](https://github.com/openclaw/openclaw/issues/4947) (Stale) — The `gateway.bind` setting fails to bind to LAN IPs on macOS, sticking to localhost only.
*   **SSRF False Positives:** [Issue #25215](https://github.com/openclaw/openclaw/issues/25215) reports that stricter SSRF checks block legitimate traffic from proxy tools like Clash/mihomo (fake-ip ranges).
*   **Windows Reliability:** [Issue #19819](https://github.com/openclaw/openclaw/issues/19819) (Stale) — SIGUSR1 restarts crash on Windows due to bad file descriptors.

---

## Cross-Ecosystem Comparison

# Open-Source AI Agent Ecosystem Analysis: March 19, 2026

## 1. Ecosystem Overview
The open-source AI agent ecosystem is currently undergoing a phase of rapid maturation, characterized by a bifurcation between heavy-duty orchestration frameworks and lightweight "personal assistant" clients. Across the board, projects are shifting focus from pure feature addition to operational stability, specifically targeting memory persistence, multi-agent management, and integration with the **Model Context Protocol (MCP)**. While OpenClaw remains the de facto standard for complex infrastructure, a surge of "Claw" derivatives (NanoClaw, PicoClaw, NullClaw) highlights a community desire for simpler, more opinionated deployments. The ecosystem faces shared growing pains regarding authentication security (secrets management), the complexity of Docker-based deployments, and the user experience friction caused by frequent breaking updates.

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Releases (24h) | Health Signal |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** (Core) | 500 | 500 | None | **Surge** (High load, healthy merge rate) |
| **CoPaw** | ~40 | ~60 | **v0.1.0-beta.3** | **Unstable** (Regressions in local models) |
| **IronClaw** | 50 | 50 | None | **Recovering** (Post-v0.19.0 debt cleanup) |
| **PicoClaw** | 32 | 89 | Nightly | **Refactoring** (Agent identity overhaul) |
| **NanoClaw** | 25 | 50 | None | **Stressed** (Security audit, sync bugs) |
| **NanoBot** | 36 | 62 | None | **Active** (High engagement, regression fixes) |
| **ZeroClaw** | 37 | 50 | **v0.5.0** | **Stabilizing** (Installation polish) |
| **NullClaw** | 15 | 25 | **v2026.3.17** | **Robust** (High velocity, rapid patching) |
| **TinyClaw** | 0 | 16 (Merged) | **v0.0.15** | **Pivoting** (Rebrand to TinyAGI) |
| **LobsterAI** | 13 | 11 | None | **Volatile** (Gateway migration friction) |
| **Moltis** | 2 | 1 | None | **Maintenance** (Critical bugs only) |
| **ZeptoClaw** | 3 | 2 | None | **Quiet** (Architectural planning) |
| **EasyClaw** | 0 (Closed 3) | 2 | **v1.7.1** | **Reactive** (Hotfixing connectivity) |

## 3. OpenClaw's Position
OpenClaw stands as the undisputed market leader in terms of raw community scale and development velocity (1000+ combined daily updates).
*   **Advantages:** It possesses the most comprehensive plugin ecosystem and a proven track record of handling enterprise-grade complexity (Nacos integration, multi-agent frameworks).
*   **Differentiation:** Unlike derivatives that struggle with basic stability (e.g., WhatsApp desyncs in PicoClaw, duplicate messages in NanoBot), OpenClaw is tackling architectural shifts like **Cortex Memory Integration** and **Native MCP support**, positioning it for the next generation of agent capabilities rather than just fixing basic messaging bugs.
*   **Community Size:** Its community is double or triple the size of the nearest competitor, allowing it to sustain a massive backlog of issues while still shipping features at a high pace.

## 4. Shared Technical Focus Areas
The following requirements are emerging as de facto standards across the ecosystem:
*   **Observability & Tracing:**
    *   **NanoBot** and **IronClaw** are seeing heavy demand for Langfuse/OpenTelemetry integration. Users are losing the ability to debug complex agent chains without external tracing.
    *   **NanoClaw** is implementing explicit API usage tracking (cost estimation) due to user frustration with "surprise bills."
*   **Security & Secrets Management:**
    *   **ZeroClaw** is debating "God Mode" vs. "Safe by Default," while **NanoClaw** and **NullClaw** are rushing to encrypt plaintext API keys in config files.
    *   **IronClaw** and **Moltis** are actively patching SSRF (Server-Side Request Forgery) vulnerabilities as agents connect to more internal tools.
*   **Memory & Context:**
    *   **OpenClaw** is moving toward persistent memory substrates (Cortex).
    *   **PicoClaw** and **TinyClaw** are refining file-based memory (`SOUL.md`/`AGENT.md` and hierarchical markdown memory) to solve context bloat.
    *   **LobsterAI** and **NanoClaw** users are demanding visibility into token usage/compression to prevent "silent failures."

## 5. Differentiation Analysis
Projects are diverging into three distinct tiers:
*   **Infrastructure / Enterprise (OpenClaw, IronClaw):** Focus on scalability, multiple providers, and complex workflows. OpenClaw targets K8s/Nacos users; IronClaw focuses on Routines/Automation.
*   **Desktop / Personal UI (LobsterAI, CoPaw, EasyClaw):**
    *   **LobsterAI** prioritizes a polished UI ("Clone accusations" suggest its UX is a market leader) but suffers from update instability.
    *   **CoPaw** is betting heavily on multimodal input (Voice/Image) and local model support (llama.cpp).
*   **Lightweight / Developer-Centric (PicoClaw, NullClaw, NanoBot, Moltis):**
    *   **NullClaw** focuses on "pure" Rust performance and A2A protocols.
    *   **NanoBot** and **PicoClaw** are competing for the "lightweight CLI agent" niche, though both are struggling with the "bloat" of maintaining Node.js and Python dependencies simultaneously.

## 6. Community Momentum & Maturity
*   **Rapidly Iterating:** **ZeroClaw** (shipping betas daily), **TinyClaw** (aggressive rebrand/release cycles), and **NullClaw** (high velocity post-release) show the most aggressive shipping cadences.
*   **Stabilizing/Mature:** **OpenClaw** and **IronClaw** are in "clean-up" phases, addressing technical debt rather than adding volatile new features.
*   **Stressed/Regressing:** **CoPaw** and **LobsterAI** are facing user backlash due to regressions in their latest releases (Local model loading errors, Gateway crashes).
*   **Niche:** **Moltis** and **ZeptoClaw** have quiet communities, focusing on low-level architecture (Rust, Firecracker VMs) rather than mass adoption.

## 7. Trend Signals
*   **The "Standardization" of MCP:** Model Context Protocol support is the #1 requested feature across OpenClaw, CoPaw, and PicoClaw. Agents that do not support MCP native tooling are considered legacy.
*   **Authentication Crisis:** Almost every project (NanoClaw, NullClaw, CoPaw) has active critical issues regarding plaintext secrets or missing authentication for web UIs. The ecosystem is moving quickly to encrypt-at-rest and add OAuth2.
*   **Platform Fatigue:** There is a clear signal from **OpenClaw**, **NanoClaw**, and **NullClaw** users requesting non-Docker / native installs. Docker complexity is becoming a barrier to entry for personal users.
*   **Multimodal is Mandatory:** **CoPaw**'s push for image upload and **PicoClaw**'s work on voice (TTS/ASR) indicates that text-only agents are entering the end-of-life phase for personal assistants.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest: 2026-03-19

## 1. Today's Overview
NanoBot is experiencing a period of **intense development and high community engagement**. In the last 24 hours, the project processed 62 Pull Requests and 36 Issues, indicating a very active iteration cycle. The current focus appears to be split between stabilizing recent regressions introduced in `v0.1.4post5` and advancing new architectural features for security and observability. While the volume of merged PRs (23) is healthy, the 25 open active issues suggest a growing backlog that needs triage.

## 2. Releases
**No new releases published in the last 24 hours.**
*Note: The project is currently on `v0.1.4post5`. Users are reporting several regressions stemming from this version, suggesting a `post6` or `v0.1.5` may be imminent to address stability.*

## 3. Project Progress
**Features Advanced (Merged/Closed PRs):**
*   **Test Infrastructure Restoration:** PR #396 (closed) removed the broad `tests/` ignore rule from `.gitignore`, ensuring new test files are tracked correctly.
*   **Configuration & Headers:** PR #424 (closed) fixed a bug where `extraHeaders` casing was not preserved during config key normalization, crucial for providers with strict header requirements.
*   **Documentation:** PR #418 (closed) added guidance for "best-effort" OpenAI-compatible endpoints.
*   **Tool Execution Stability:** PR #2192 (closed) addressed graceful error handling in the agent loop to prevent crashes during tool failures.

**Active Development (Open PRs):**
*   **Security:** PR #2225 aims to set strict `0o600` permissions on config files to protect API keys.
*   **i18n:** PR #2232 is implementing a comprehensive multilingual documentation suite (English/Chinese).
*   **Config UX:** PR #2227 attempts to automatically fill in new config options when schema changes occur.

## 4. Community Hot Topics
*   **[Observability Demand](https://github.com/HKUDS/nanobot/issues/2189)** & **[LLM Tracing](https://github.com/HKUDS/nanobot/issues/2154)**
    *   **Discussion:** Users are explicitly requesting integration with **Langfuse** or general trace/observability features.
    *   **Signal:** As users deploy NanoBot in production, debugging complex agent chains has become a major pain point.
*   **[Security: Plaintext Secrets](https://github.com/HKUDS/nanobot/issues/2172)**
    *   **Discussion:** High demand for removing secrets from `config.json` and supporting references to env vars or secret managers (1Password).
    *   **Signal:** "Ultra-lightweight" implies security by default; storing keys in plaintext is a blocker for enterprise adoption.
*   **[Architecture: "Ultra-lightweight" Definition](https://github.com/HKUDS/nanobot/issues/660)**
    *   **Discussion:** A spirited debate regarding the requirement of Node.js alongside Python.
    *   **Signal:** The community is strict about resource usage and architectural purity.

## 5. Bugs & Stability
**High Severity / Regressions:**
*   **[v0.1.4post5 Voice Transcription Failure](https://github.com/HKUDS/nanobot/issues/2141)**
    *   **Status:** Open
    *   **Impact:** Users lost the ability to transcribe voice notes on Telegram immediately after upgrading.
*   **[Duplicate Messages on Telegram/WhatsApp](https://github.com/HKUDS/nanobot/issues/1692) & [Android specifically](https://github.com/HKUDS/nanobot/issues/2208)**
    *   **Status:** Open (Partially addressed in PR #2177)
    *   **Impact:** Bots respond twice or rendering fails, degrading UX significantly.
*   **[Gemini-3-Flash Compatibility Broken](https://github.com/HKUDS/nanobot/issues/2185)**
    *   **Status:** Open
    *   **Impact:** Regression affecting Google model users.
*   **[MCP Tools TypeError](https://github.com/HKUDS/nanobot/pull/2230)**
    *   **Status:** Fix Proposed (Open PR)
    *   **Impact:** MCP tools with nullable parameters crash the agent.

**Medium Severity:**
*   **[Infinite Loop Response (llama3.3)](https://github.com/HKUDS/nanobot/issues/1240)**: Closed, but highlights issues with specific model parameter handling.
*   **[LiteLLM Timeout in Air-Gapped Networks](https://github.com/HKUDS/nanobot/issues/2145)**: Dependency attempts to phone home to GitHub, causing startup failures in isolated environments.

## 6. Feature Requests & Roadmap Signals
*   **Plugin/Extensibility System:** There are competing requests for a **Plugin System** [#2231](https://github.com/HKUDS/nanobot/issues/2231) and a **Hooks System** (like Claude Code) [#2182](https://github.com/HKUDS/nanobot/issues/2182). Both aim to allow user-defined logic at lifecycle events (SessionStart, PreToolUse).
*   **Multi-Tenancy:** Request for **data isolation** between users/workspaces [#2102](https://github.com/HKUDS/nanobot/issues/2102).
*   **QQ Channel File Support:** Users want to send/receive files via QQ, currently only text is supported [#2226](https://github.com/HKUDS/nanobot/issues/2226).
*   **Interactive Wizard:** Issue [#2018](https://github.com/HKUDS/nanobot/issues/2018) suggests an onboarding wizard to avoid manual JSON editing.

## 7. User Feedback Summary
*   **Configuration Friction:** Users struggle with the manual `config.json` editing. Requests for "wizards" and complaints about breaking changes in config schema (#2227) indicate the developer experience (DX) for setup needs improvement.
*   **Platform Specifics:** Telegram users are the most vocal regarding bugs (duplicates, markdown rendering, voice notes), likely due to it being the primary platform.
*   **Satisfaction vs. Bloat:** There is a distinct divide between users who want *more* features (Langfuse, Plugins) and users who want *fewer* dependencies (No Node.js). Maintaining the "lightweight" promise while adding features is the core tension.

## 8. Backlog Watch
*   **[Good First Issue: Node.js Bloat](https://github.com/HKUDS/nanobot/issues/660)** (Open since Feb 14): Labeled `to-nightly` but unresolved.
*   **[Model Switching](https://github.com/HKUDS/nanobot/issues/1991)**: Request to support multiple "custom" model profiles for easy switching.
*   **[Status Command](https://github.com/HKUDS/nanobot/issues/2131)**: Users want a `/status` command to see if the bot is busy/locked without accessing the terminal.
*   **[Boot Notifications](https://github.com/HKUDS/nanobot/issues/2160)**: A user implemented a feature to notify when the bot comes online; awaiting official integration.

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Project Digest: ZeroClaw
**Date:** 2026-03-19
**Analyst:** AI Agent Researcher

---

### 1. Today's Overview
ZeroClaw is experiencing a **high-velocity release cycle**, having shipped 8 releases (ranging from beta.347 to v0.5.0) within a short window. The project shows robust development health with 50 updated PRs (over 50% open/active) and high community engagement (37 updated issues). The primary focus has shifted towards **operational polish**—improving the installation process, adding internationalization support, and refining agent behavior—while simultaneously expanding channel integrations to Reddit and Bluesky. While the pace of new features is high, stability concerns around Docker builds and credential handling in routing remain active areas of friction.

### 2. Releases
**v0.5.0 (Stable) & v0.5.0-beta series (347–365)**
This release cycle marks a significant maturation of the ZeroClaw agent framework.

*   **Agent Capabilities:**
    *   **Runtime Model Switching:** A new `model_switch` tool allows changing models mid-conversation without restarting the agent (merged in #3854).
    *   **Autonomous Skill Creation:** The agent can now automatically generate reusable skills from successful multi-step tasks (`[skills.skill_creation]` config).
*   **Platform & Integrations:**
    *   **New Channels:** Added native support for Reddit, Bluesky, and generic Webhooks.
    *   **Provider Support:** Enhanced support for Alibaba Cloud "Coding Plan" and `claude-code` provider upgrades.
*   **Operations (CLI/CI):**
    *   **Installer Improvements:** Added a robust self-test command (`quick`/`full` modes) and a dedicated `status --format=exit-code` for Docker healthchecks.
    *   **Update Mechanism:** Implemented a new 6-phase update pipeline with rollback capabilities.
*   **Configuration:**
    *   **Delegate Timeouts:** Sub-agent timeouts are now configurable via `config.toml` instead of being hardcoded.
    *   **i18n:** Tool descriptions have been externalized to facilitate translation.

### 3. Project Progress
**Merged & Closed Advancements:**
*   **Agent Logic:**
    *   **[PR #3916](https://github.com/zeroclaw-labs/zeroclaw/pull/3916):** Implemented autonomous skill creation, allowing the agent to learn from past successful tasks.
    *   **[PR #3910](https://github.com/zeroclaw-labs/zeroclaw/pull/3910):** Fixed a critical "vicious circle" bug where the agent would get stuck in a self-correction loop by resetting the tool call dedup cache.
    *   **[PR #3912](https://github.com/zeroclaw-labs/zeroclaw/pull/3912):** Externalized tool descriptions to enable translations (Addressing #3901).
*   **System Reliability:**
    *   **[PR #3906](https://github.com/zeroclaw-labs/zeroclaw/pull/3906):** Fixed the `install.sh` script to ensure `config.toml` is created even when using `--skip-build` or `--prefer-prebuilt` flags.
    *   **[PR #3915](https://github.com/zeroclaw-labs/zeroclaw/pull/3915):** Ensured `SOUL.md` and `IDENTITY.md` are scaffolded in non-TTY sessions (e.g., cron or daemon mode), preventing the agent from starting without an identity.
*   **Channel Features:**
    *   **[PR #3923](https://github.com/zeroclaw-labs/zeroclaw/pull/3923):** Added `mention_only` gating for WhatsApp groups.

### 4. Community Hot Topics
**The Security vs. Usability Debate:**
*   **[#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478): "Besides security, there are no functions"**
    *   **Summary:** A user expressed extreme frustration that aggressive security defaults prevent the agent from performing basic tasks (like installing ffmpeg), effectively rendering it a "chatbot only."
    *   **Sentiment:** High dissatisfaction (41 comments, 5+ upvotes).
    *   **Underlying Need:** Users desire a "God Mode" or "sudo" configuration that bypasses safety checks for personal, trusted environments. The complexity of OpenClaw was the driver for choosing ZeroClaw, but the restrictions are too tight.

**Integration Gaps:**
*   **[#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503): "Where is Napcat/Onebot channel?"**
    *   **Summary:** Users are looking for OneBot11/Napcat support to bridge with QQ/Facebook, finding it missing in the configuration options.

### 5. Bugs & Stability
*   **[S1 - Workflow Blocked] Docker Build Failure:**
    *   **[#3925](https://github.com/zeroclaw-labs/zeroclaw/issues/3925):** Docker builds crash on `linux/amd64` with `unused manifest key: lib.include` during the Cargo build phase.
*   **[S1 - Workflow Blocked] Configuration Schema:**
    *   **[#3919](https://github.com/zeroclaw-labs/zeroclaw/issues/3919):** The `config schema` command fails due to a parsing error on `challenge_max_attempts`. Fix is in progress via **[PR #3921](https://github.com/zeroclaw-labs/zeroclaw/pull/3921)**.
*   **[S1 - Workflow Blocked] Local Provider Connectivity:**
    *   **[#3894](https://github.com/zeroclaw-labs/zeroclaw/issues/3894):** Users utilizing custom local providers (like llamafile) are encountering "Non-retryable errors" causing immediate failures without fallback.
*   **[S2 - Degraded] Tool Calling/Security Handshake:**
    *   **[#3922](https://github.com/zeroclaw-labs/zeroclaw/issues/3922):** Ollama tool-calling handshake failures are preventing the agent from executing security prompts and tools.

### 6. Feature Requests & Roadmap Signals
*   **Stop/Interruption Control:** Multiple active PRs (**[PR #3891](https://github.com/zeroclaw-labs/zeroclaw/pull/3891)**, **[PR #3895](https://github.com/zeroclaw-labs/zeroclaw/pull/3895)**, **[PR #3918](https://github.com/zeroclaw-labs/zeroclaw/pull/3918)**) indicate a push to add `/stop` command and `interrupt_on_new_message` support across Matrix, Discord, and Mattermost channels.
*   **Alibaba Cloud Support:** Explicit request and active development (**[PR #3889](https://github.com/zeroclaw-labs/zeroclaw/pull/3889)**) for Alibaba Coding Plan support.
*   **Cross-Channel TOTP:** Request for expanded 2FA/OTP gating for critical tools across all channels (**[#3767](https://github.com/zeroclaw-labs/zeroclaw/issues/3767)**).

### 7. User Feedback Summary
**Pain Points:**
*   **Over-Restrictive Safety:** Users feel the "safe by default" philosophy renders the agent unusable for autonomous tasks (e.g., [#1478](https://github.com/zeroclaw-labs/zeroclaw/issues/1478)). They need clearer ways to disable these rails for personal projects.
*   **Installation Complexity:** Despite the "zero" in the name, installation on small devices (Orange Pi) or via Podman is still brittle (missing configs, build cache issues).
*   **Context/Token Efficiency:** Users are requesting better token management to prevent "bloat" when running on local hardware with limited context windows (**[#3892](https://github.com/zeroclaw-labs/zeroclaw/issues/3892)**).

### 8. Backlog Watch
*   **[#3818](https://github.com/zeroclaw-labs/zeroclaw/issues/3818) - Restore Legacy Features:**
    *   Critical security parameters and the `Copilot` onboarding provider were lost during a branch migration (`main` -> `master`). Restoring these is essential for parity.
*   **[#3845](https://github.com/zeroclaw-labs/zeroclaw/issues/3845) - Dynamic Skill Loading:**
    *   Long-running channels do not refresh available skills or cached system prompts. Users must restart the daemon to use new skills.
*   **[#3838](https://github.com/zeroclaw-labs/zeroclaw/issues/3838) - Credential Wiring Gap:**
    *   Route-specific API keys are dropped in Channel/Agent mode, falling back to global keys unintentionally.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# Project Digest: PicoClaw (2026-03-19)

## 1. Today's Overview
PicoClaw is experiencing a period of intense development and high community engagement. The project saw 89 PRs and 32 issues updated in the last 24 hours, signaling that the "Agent Refactor" (Track #1216) is in full swing. While development velocity is high, stability remains a concern; user reports frequently cite configuration complexity, provider-specific bugs (GLM, OpenRouter, Anthropic), and "silent failures" in channels (Feishu, Telegram). The project is actively advancing toward v0.2.3/0.3.0, with major shifts in agent architecture (`SOUL.md`, `AGENT.md`) and a strong focus on hardening security and provider compatibility.

## 2. Releases
* **v0.2.3-nightly.20260319** ([Release](https://github.com/sipeed/picoclaw/releases/tag/v0.2.3-nightly.20260319.e73d9d95))
    *   **Type:** Nightly Build (Unstable)
    *   **Highlights:** This automated build bridges the gap between v0.2.3 and the main branch. It likely includes the latest fixes for provider errors and tool enhancements discussed below, but users are advised to exercise caution due to the ongoing heavy refactoring in the agent core.

## 3. Project Progress
*   **Agent Refactor (Architecture):** Significant progress on defining Agent Identity.
    *   **PRs:** Merged/Closed logic regarding `SOUL.md` and `AGENT.md` structures (Issues #1218, #1756). The codebase is moving towards a model where personality (`SOUL.md`) is distinct from instruction (`AGENT.md`).
    *   **Sub-Agents:** PR #1636 (SubTurn) is actively being developed to enable hierarchical agent execution with proper lifecycle management.
*   **Provider Compatibility:**
    *   **Alibaba Cloud:** PR #1748 adds support for Alibaba Coding Plan and international Qwen endpoints.
    *   **OpenAI Compatibility:** PR #1768 introduces configurable streaming for custom APIs.
*   **Tooling & Sandbox:**
    *   **Security:** PR #1760 introduces "Sandbox" Docker Compose files to enhance host isolation using read-only filesystems and capability dropping.
    *   **Usability:** PR #1761 adds an `overwrite` flag to `write_file` to prevent accidental data loss, and PR #1332 aims to provide real-time feedback for tool usage via channels.
*   **Documentation:**
    *   PR #1747 clarifies that workspace configuration files (`AGENTS.md`, etc.) are now **hot-reloaded**, removing the need for gateway restarts during config updates.

## 4. Community Hot Topics
*   **[Issue #1218] "What an Agent is" (27 comments)**
    *   **Link:** [sipeed/picoclaw#1218](https://github.com/sipeed/picoclaw/issues/1218)
    *   **Topic:** The definition of the new `SOUL.md` vs `AGENT.md` paradigm.
    *   **Analysis:** This is the core philosophical debate of the refactor. The community is actively discussing how much structure to impose on an agent's "soul" (personality) versus keeping it freeform. High engagement indicates users care deeply about customizability.
*   **[Issue #1648] Adding TTS and ASR Support (10 comments)**
    *   **Link:** [sipeed/picoclaw#1648](https://github.com/sipeed/picoclaw/issues/1648)
    *   **Topic:** Voice interaction architecture.
    *   **Analysis:** There is strong demand for voice capabilities. Users are pushing for a standardized architecture for Text-to-Speech and Speech-to-Text to be integrated into the gateway, moving away from disparate scripts.
*   **[Issue #1216] Meta: Agent refactor (8 comments)**
    *   **Link:** [sipeed/picoclaw#1216](https://github.com/sipeed/picoclaw/issues/1216)
    *   **Topic:** Roadmap for the agent refactor.
    *   **Analysis:** The tracking issue for all breaking changes. Users are monitoring this to understand when the "instability" period will end and what migration steps will be required.

## 5. Bugs & Stability
*   **Severity: High - Channel Failures**
    *   **Issue #1757:** Users report that scheduled tasks (cron) run successfully but produce **no output** in the channel (Telegram). ([#1757](https://github.com/sipeed/picoclaw/issues/1757))
        *   *Status:* Fix proposed in PR #1766.
    *   **Issue #1767:** Feishu (Lark) bot frequently stops replying, suspected network disconnect with no auto-reconnect. ([#1767](https://github.com/sipeed/picoclaw/issues/1767))
*   **Severity: Medium - Provider Errors**
    *   **Issue #1652:** GLM Coding Plan returns "Insufficient balance" errors even when balance exists. ([#1652](https://github.com/sipeed/picoclaw/issues/1652))
    *   **Issue #1658:** Claude API returns "tool use.name string should contain at least 1 character," breaking the tool calling loop. ([#1658](https://github.com/sipeed/picoclaw/issues/1658))
    *   **Issue #1746:** `reasoning_channel_id` not functioning with OpenAI-compatible providers (e.g., LiteLLM/Venice AI). ([#1746](https://github.com/sipeed/picoclaw/issues/1746))
*   **Severity: Low - UX/Edge Cases**
    *   **Issue #1042:** `exec` tool safety guard blocks harmless commands (e.g., `curl wttr.in`) due to aggressive regex path matching. ([#1042](https://github.com/sipeed/picoclaw/issues/1042))
    *   **Issue #1734:** Launcher crashes silently if it cannot open the log file. ([#1734](https://github.com/sipeed/picoclaw/issues/1734))

## 6. Feature Requests & Roadmap Signals
*   **RFC: PTY + Background Support (Issue #1733):** Users want the `exec` tool to support long-running interactive tasks (like `docker build`) and background processes, which it currently cannot handle. ([#1733](https://github.com/sipeed/picoclaw/issues/1733))
*   **Enterprise Observability (Issue #1731):** Request for OpenTelemetry (OTel) GenAI standard support for enterprise monitoring. ([#1731](https://github.com/sipeed/picoclaw/issues/1731))
*   **OpenAI API Channel (Issue #1738):** Users want to expose PicoClaw *as* an OpenAI-compatible endpoint to easily integrate it into existing ecosystems. ([#1738](https://github.com/sipeed/picoclaw/issues/1738))
*   **WebUI (Issue #806):** A Web UI is under active refactoring to lower the barrier to entry for non-technical users. ([#806](https://github.com/sipeed/picoclaw/issues/806))

## 7. User Feedback Summary
*   **Configuration Fatigue:** Users are struggling with "magic values" and scattered environment variables, leading to a request for centralized management (Issue #1638).
*   **Provider Trust:** There is noticeable frustration with specific providers (GLM, OpenRouter) either not working or consuming balance without returning results.
*   **Safety vs. Usability:** The `exec` tool's safety guards are viewed as too simplistic, blocking valid commands while trying to protect the system.
*   **Silent Failures:** The most critical pain point is the agent "thinking" (LLM inference completing) but failing to deliver the message to the user (Channel/Provider disconnect), leaving the user in the dark.

## 8. Backlog Watch
*   **Issue #547:** Improve `AGENT.md` with task-solving patterns. Open since Feb 20, this highlights the need for better "System Prompts" out of the box. ([#547](https://github.com/sipeed/picoclaw/issues/547))
*   **Issue #1209:** "Timeout error with context deadline exceeded." Open since March 7, affecting one-shot agents. ([#1209](https://github.com/sipeed/picoclaw/issues/1209))
*   **PR #1332:** Tool Feedback feature. Still open. Implementing this would significantly improve the "waiting" experience for users. ([#1332](https://github.com/sipeed/picoclaw/pull/1332))

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

**Project Digest: NanoClaw**
**Date:** 2026-03-19
**Analyst:** AI Agent Research

---

### 1. Today's Overview
NanoClaw is experiencing an intense phase of development and maintenance, with high community engagement across 25 issues and 50 pull requests updated in the last 24 hours. The project is currently in a "security and stability" sprint, addressing critical vulnerabilities regarding user data logging and container trust models. Despite this high activity, development velocity appears slightly bottlenecked; numerous critical bugs regarding session management and code synchronization remain open, and the CI/CD pipeline is reporting repeated merge conflicts in skill branches. The community is actively pushing for broader platform support (beyond Claude) and better operational hygiene (Dockerless installs, update safety).

### 2. Latest Releases
*No new releases published in the last 24 hours.*

### 3. Project Progress
While no PRs were marked *merged* in the immediate data window, significant advancements are under review:
*   **Security Hardening:** PR #1191 (Fixes #1150) addresses the critical issue of user prompts being logged to disk in plaintext during container errors.
*   **Platform Resilience:** PR #1253 fixes credential binding issues on WSL with native Docker Engine, improving cross-platform compatibility.
*   **Feature Expansion:**
    *   PR #1111 introduces comprehensive API usage tracking (SQLite tables, cost estimation).
    *   PR #1255 adds MiniMax OAuth as an alternative model provider, reducing reliance on a single LLM vendor.
    *   PR #1250 and #1251 are expanding capabilities with local voice transcription (via whisper.cpp) and an OpenMail email channel.

### 4. Community Hot Topics
*   **Security Disclosure & Trust** [Critical]
    *   **Issue #1149:** A private request for a security disclosure channel suggests a responsible vulnerability finding.
    *   **Issue #865 (Closed):** Discussion on "Container trust" highlights architectural concerns about assuming containers are secure by default.
    *   **Underlying Need:** The community prioritizes security auditing and is demanding safer defaults for credential handling and data logging.

*   **Claude SDK Terms of Service** [High Interest]
    *   **Issue #1224:** Revisiting TOS compliance regarding the use of the Claude Agent SDK via subscription credentials, citing changes in the risk landscape.
    *   **Underlying Need:** Users and developers are anxious about the legality and longevity of NanoClaw's dependency on Anthropic's specific terms, seeking a migration path to standard API keys or alternative CLIs.

*   **Multi-Model Support** [Enhancement]
    *   **Issue #1163:** Request to support OpenCode (JS SDK) in parallel with Claude Code to allow usage with other AI providers.
    *   **Underlying Need:** Vendor lock-in is a major concern; users want flexibility to use internal or different AI providers.

### 5. Bugs & Stability
*   **CRITICAL - Session Management:**
    *   **Issue #1216:** Stale Claude Code session IDs cause permanent resume failures with no auto-recovery mechanism.
    *   **Issue #1236:** Updates to `agent-runner` source code do not sync to existing groups, leaving production environments running stale code.
*   **CRITICAL - Pipeline Reliability:**
    *   **Issue #1242:** Pipeline stage timeouts are defined in constants but not enforced at runtime, leading to stuck pipeline runs.
*   **HIGH - Security/Data:**
    *   **Issue #1150:** (Fix in PR #1191) Container error logs include full user prompt content.
*   **MEDIUM - Functionality:**
    *   **Issue #1210:** API incompatibility with Alibaba DashScope proxying Claude models (model mapping issues).
    *   **Issue #1141:** Per-group trigger patterns saved to DB are ignored by the runtime logic.
    *   **Issue #1135:** The `update-nanoclaw` script silently drops customized code during auto-merge without conflict markers.
    *   **Issue #1184:** Deployment challenges in restricted Kubernetes environments (Sealos).

### 6. Feature Requests & Roadmap Signals
*   **Session Management:** Issue #1211 requests a `/new` command to reset session context to prevent token waste and history accumulation.
*   **Non-Docker Workflows:** Issue #1225 asks for native Windows/Linux support without requiring Docker.
*   **E2E Testing:** Several issues by user `azorel` (#1244, #1243, #1249, #1248) indicate a roadmap focus is being placed on test coverage, specifically auditing missing tests and fixing regex/IPC bugs in the testing suite.
*   **Interactive CLI:** PR #1247 proposes storing bot responses and adding an interactive REPL to the CLI.

### 7. User Feedback Summary
*   **Pain Points:**
    *   **Update Anxiety:** Users are frustrated that updating the framework (Issue #1135) or the agent source (Issue #1236) can silently break existing setups or lose customizations.
    *   **Documentation Confusion:** Issue #1075 highlights a mismatch between GitHub Readme (Linux "coming soon") and the official website (Linux "supported"), causing onboarding friction.
    *   **Docker Dependency:** A subset of users (Issue #1225) feels alienated by the strict Docker requirement.
*   **Positive Sentiment:**
    *   Users appreciate the "minimalist approach" compared to bloated agent frameworks (Issue #1184).
    *   The community is actively contributing complex features (OAuth integration, Voice channels) indicating strong engagement.

### 8. Backlog Watch
*   **Merge Conflicts:** Automated maintenance issues (#1226, #1227, #1228) indicate that skill branches `skill/apple-container` and `skill/compact` have failed to merge with `main` for at least three consecutive commits (aa4f7a2, 9200612, fe0a309). These branches require manual intervention to rejoin the mainline.
*   **Long-Standing/Unanswered:**
    *   **Issue #1163:** Discussion on supporting other AI providers (OpenCode) remains open with high interest (👍 2) but no labeled status.
    *   **Issue #418:** A fix for the `/setup` mounts step (changing allowlist format) remains "Blocked" and open since February.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest: 2026-03-19

## 1. Today's Overview
The NullClaw project is demonstrating high velocity and stability, resolving a cluster of post-release regressions quickly following the `v2026.3.17` release. With 25 PRs and 15 Issues updated in the last 24 hours, the team is actively prioritizing bug fixes and developer experience improvements over new feature experimentation. The core focus remains on solidifying the Agent-to-Agent (A2A) protocol, correcting configuration parsing (specifically regarding AIEOS identity), and ensuring compatibility across diverse environments like Nix, Podman, and Android. The project health appears robust, with maintainer `manelsen` leading a significant cleanup effort to address recent user-reported friction points.

## 2. Releases
**v2026.3.17** (Released 2026-03-18)
*   **Key Changes**:
    *   **OTLP Support**: Added runtime observability wiring and OpenTelemetry Protocol (OTLP) support (PR #600).
    *   **Hardened Channels**: Introduced hardened external channel plugins (PR #582).
*   **Migration Notes**: Users utilizing the `nullclaw` container image should note that the configuration schema has recently shifted away from `default_provider` to `agents.defaults.model.primary`. Several PRs (e.g., #636) are addressing documentation and starter config mismatches caused by this transition.

## 3. Project Progress
**Merged & Closed PRs**
*   **Release Engineering**: `v2026.3.17` was successfully cut and pushed ([#614](https://github.com/nullclaw/nullclaw/pull/614)).
*   **Crypto & Security**: API keys in `config.json` are now encrypted at rest ([#609](https://github.com/nullclaw/nullclaw/pull/609)), and a security fix preventing the leakage of pairing code secrets in logs was merged ([#535](https://github.com/nullclaw/nullclaw/pull/535)).
*   **Service Management**: Added OpenRC support for Linux service management ([#605](https://github.com/nullclaw/nullclaw/pull/605)), broadening the project's system compatibility.
*   **Configuration Logic**: Clarified the interaction between `workspace_path` and `system_prompt` via documentation and regression tests ([#620](https://github.com/nullclaw/nullclaw/pull/620)).
*   **Regression Fixes**: A session fix resolving dangling provider pointers in named-agent sessions was closed ([#500](https://github.com/nullclaw/nullclaw/pull/500)), alongside a batch fix for regressions in prompt injection, Matrix, and Telegram ([#632](https://github.com/nullclaw/nullclaw/pull/632)).

**Active Development**
*   **A2A Protocol Upgrade**: A major update is in progress ([#630](https://github.com/nullclaw/nullclaw/pull/630)) to upgrade the A2A implementation to v0.3.0, adding new task states (rejected, auth-required) and enhanced history support.

## 4. Community Hot Topics
*   **Installation & Config Friction (Docker/Nix)**:
    *   PR [#636](https://github.com/nullclaw/nullclaw/pull/636): Discussion on fixing the OCI container starter config to match the new schema.
    *   PR [#637](https://github.com/nullclaw/nullclaw/pull/637): Pinning the Nix flake dev shell to Zig 0.15.2 to match repo requirements.
    *   *Signal*: The community is rapidly adopting the tool across various Linux environments, and the recent schema changes caused temporary friction in containerized and Nix-based setups.

*   **Platform-Specific Bugs**:
    *   Issue [#626](https://github.com/nullclaw/nullclaw/issues/626): Users reporting `TEXTDRAFT_PEER_INVALID` errors in Telegram. Addressed in PR [#635](https://github.com/nullclaw/nullclaw/pull/635).
    *   Issue [#616](https://github.com/nullclaw/nullclaw/issues/616): Matrix private room detection logic failing for quiet rooms. Fix pending in PR [#634](https://github.com/nullclaw/nullclaw/pull/634).
    *   *Signal*: Cross-platform compatibility (Telegram, Matrix, Android/Podman) is a major daily pain point for users, requiring rapid patch cycles.

*   **Configuration Complexity**:
    *   Issue [#613](https://github.com/nullclaw/nullclaw/issues/613): Users requesting better descriptions for `config.json` options to ease onboarding.

## 5. Bugs & Stability
**High Severity**
*   **AIEOS Identity Injection Bug** ([Issue #625](https://github.com/nullclaw/nullclaw/issues/625)): Configured AIEOS identity was parsed but never injected into the system prompt.
    *   *Fix*: Available in PR [#633](https://github.com/nullclaw/nullclaw/pull/633).
*   **HTTP Timeout Configuration Ignored** ([Issue #519](https://github.com/nullclaw/nullclaw/issues/519)): `HttpRequestTool` hardcoded curl timeout to 60s, ignoring `http_timeout_secs`.
    *   *Status*: Closed/Fixed.

**Medium Severity**
*   **Podman Gateway Failure** ([Issue #629](https://github.com/nullclaw/nullclaw/issues/629)): Starter config in containers fails due to deprecated schema fields.
*   **Matrix Room Logic** ([Issue #616](https://github.com/nullclaw/nullclaw/issues/616)): Private room detection fails if members haven't spoken.
*   **Telegram Draft Errors** ([Issue #626](https://github.com/nullclaw/nullclaw/issues/626)): API errors for invalid peers causing log spam.

## 6. Feature Requests & Roadmap Signals
*   **Vision Pipeline (Multimodal)**: ([Issue #624](https://github.com/nullclaw/nullclaw/issues/624)) Users want automatic base64 encoding to send images/files directly to multimodal LLMs.
*   **Wife-Safe Messaging**: ([Issue #618](https://github.com/nullclaw/nullclaw/issues/618)) Request for a buffering mechanism to wait for a stream of messages before the bot responds, improving UX for users who send multiple short messages.
*   **HTTP Status Endpoint**: ([Issue #631](https://github.com/nullclaw/nullclaw/issues/631)) Request for a `GET /status` endpoint for monitoring active/idle agents without using the CLI.
*   **Search Enhancement**: ([Issue #623](https://github.com/nullclaw/nullclaw/issues/623)) Request to add DuckDuckGo (`ddgs`) metasearch support.
*   **Gemini CLI Local Provider**: ([PR #628](https://github.com/nullclaw/nullclaw/pull/628)) Active work to support Gemini CLI as a keyless local provider.

## 7. User Feedback Summary
*   **Pain Points**: The primary source of dissatisfaction today stems from **migration friction**. Users running the latest container images or cloning the repo are facing "Config error" messages due to the shift from `default_provider` to `agents.defaults.model.primary`.
*   **Error Visibility**: Users expressed frustration with generic error messages like "error.ApiError" ([Issue #619](https://github.com/nullclaw/nullclaw/issues/619)), requesting more detailed feedback to debug configuration issues.
*   **Onboarding**: Newcomers are struggling with the lack of documentation for configuration options ([Issue #613](https://github.com/nullclaw/nullclaw/issues/613)).

## 8. Backlog Watch
*   **Android Installation** ([Issue #339](https://github.com/nullclaw/nullclaw/issues/339)): Open since March 6, regarding build errors in Termux. No PR is linked yet.
*   **Custom Provider Guide** ([Issue #117](https://github.com/nullclaw/nullclaw/issues/117)): Users asking how to add custom models (e.g., Claude) to the transfer station. This remains a top-requested documentation/code example task.
*   **MAX Messenger Support** ([Issue #607](https://github.com/nullclaw/nullclaw/issues/607)): Discussion regarding the ethics/feasibility of supporting the state-promoted MAX messenger. Closed, but highlights geopolitical considerations in the roadmap.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest: 2026-03-19

## 1. Today's Overview
IronClaw is demonstrating exceptionally high development velocity with **50 Issues and 50 PRs updated in the last 24 hours**, split nearly evenly between active/closed items. The project is in a "clean-up and polish" phase following the recent `v0.19.0` release, with a strong focus on addressing **CRITICAL and HIGH severity technical debt** identified by the Staging CI Review bot. While no new releases were published today, the `main` branch is undergoing active promotion via automated staging batches. Development is broadly distributed across core agent improvements, authentication/OAuth refactoring, and new LLM provider integrations.

## 2. Releases
**No new releases** published in the last 24 hours.
*Note: Users upgrading from v0.18.0 to v0.19.0 should be aware of ongoing reports regarding migration checksum mismatches (see Issue #1328).*

## 3. Project Progress
**Significant advancements were made in internal architecture and bug fixing:**

*   **OAuth & Auth Refactoring:** [PR #1375](https://github.com/nearai/ironclaw/pull/1375) (Open) by `henrypark133` aims to unify hosted OAuth and MCP authentication flows, moving toward generic, versioned callback states.
*   **Agent "Self-Repair":** [PR #1234](https://github.com/nearai/ironclaw/pull/1234) (Open) introduces `stuck_threshold` logic to detect jobs stuck in `InProgress` state, a crucial stability improvement for long-running agent tasks.
*   **Reliability Fixes:** [PR #1380](https://github.com/nearai/ironclaw/pull/1380) (Merged) and [PR #1374](https://github.com/nearai/ironclaw/pull/1374) (Merged) addressed performance issues (schema caching) and logic bugs (`full_job` lifecycle management) respectively.
*   **Testing Framework:** [PR #1233](https://github.com/nearai/ironclaw/pull/1233) (Open) adds a sophisticated `FaultInjector` to the `StubLlm`, allowing developers to simulate specific network failures to test retry logic.

## 4. Community Hot Topics
*   **Upgrade Path Broken:** [Issue #1328](https://github.com/nearai/ironclaw/issues/1328) (👍 2) is the most significant user-facing issue. Users report that upgrading to `v0.19.0` fails due to a checksum mismatch in the `V6__routines` SQL migration. This suggests a release process gap where migration scripts were modified post-release.
*   **SSRF Security Fix:** [PR #1221](https://github.com/nearai/ironclaw/pull/1221) addresses a critical SSRF vulnerability (#1103) by validating embedding base URLs, preventing attackers from forcing the agent to contact internal network resources.
*   **Tool Installation Failures:** [Issue #1205](https://github.com/nearai/ironclaw/issues/1205) and [Issue #1384](https://github.com/nearai/ironclaw/issues/1384) highlight friction in the tool ecosystem, specifically incorrect release asset paths for Slack tools and capability file lookups for Telegram channels.

## 5. Bugs & Stability
**Critical & High Severity Issues (Staging CI Review):**
The CI bot identified several severe code quality issues in the Routines engine, most of which were immediately closed (likely fixed):
*   **CRITICAL - Logic Inversions:** [Issue #1281](https://github.com/nearai/ironclaw/issues/1281) found a Telegram auto-verification check was inverted, and [Issue #1178](https://github.com/nearai/ironclaw/issues/1178) found a workflow linting bypass.
*   **CRITICAL - Performance/DoS:** [Issue #1361](https://github.com/nearai/ironclaw/issues/1361) highlighted "N+1 schema generation on every LLM call," and [Issue #1287](https://github.com/nearai/ironclaw/issues/1287) found an "Unbounded Retry-After duration DoS vulnerability."
*   **CRITICAL - Reliability:** [Issue #908](https://github.com/nearai/ironclaw/issues/908) noted that `consecutive_failures` counters were not reset on successful reconnection, potentially breaking stream recovery logic.

**User Reported Regressions:**
*   **PostgreSQL Migration Failure:** [Issue #1328](https://github.com/nearai/ironclaw/issues/1328) remains open and blocks upgrades for existing database users.

## 6. Feature Requests & Roadmap Signals
*   **MCP Approval Modes:** [PR #1383](https://github.com/nearai/ironclaw/pull/1383) introduces granular control over MCP (Model Context Protocol) server approvals, allowing users to set `auto`, `always`, or `never` modes per server.
*   **Custom LLM UI:** [PR #1340](https://github.com/nearai/ironclaw/pull/1340) allows defining custom LLM providers via the Web UI, removing the need to edit config files manually.
*   **Aliyun Integration:** [PR #1299](https://github.com/nearai/ironclaw/pull/1299) adds support for Aliyun BaiLian Coding Plan, signaling continued expansion of provider support beyond the standard US-based APIs.

## 7. User Feedback Summary
*   **Pain Point - Discovery/Installation:** Users are struggling with the `ironclaw registry install` command failing due to 404 errors ([#1205](https://github.com/nearai/ironclaw/issues/1205)) and incorrect paths for auth files ([#1384](https://github.com/nearai/ironclaw/issues/1384)). The "plug-and-play" promise of tools feels brittle.
*   **Pain Point - Upgrades:** The migration error in [#1328](https://github.com/nearai/ironclaw/issues/1328) indicates that while the `v0.19.0` feature set is desired, the deployment process is risky for production users with persistent data.

## 8. Backlog Watch
*   **Routine Concurrency:** While [Issue #1317](https://github.com/nearai/ironclaw/issues/1317) (full_job lifecycle) and [Issue #1318](https://github.com/nearai/ironclaw/issues/1318) (concurrency limits) were closed by PR #1374, [Issue #1320](https://github.com/nearai/ironclaw/issues/1320) (Bounded self-recovery for transient failures) remains **Open**. This is a key feature for making the "Routines" system robust enough for production reliance.
*   **Test Reliability:** [Issue #1280](https://github.com/nearai/ironclaw/issues/1280) regarding "Flaky OAuth wildcard callback tests" remains open, indicating ongoing CI instability that slows down development velocity.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest: 2026-03-19

## 1. Today's Overview
LobsterAI is experiencing a high-intensity development cycle with significant architectural refactoring occurring concurrently with widespread stability reports. The project has processed 11 Pull Requests in the last 24 hours (9 merged), focusing heavily on migrating the NetEase IM (NIM) gateway to the OpenClaw plugin architecture and fixing critical UI streaming states. However, this rapid iteration has introduced friction; the Issues board is saturated with 13 new or updated reports, primarily stemming from the v0.2.x update cycle, ranging from configuration migrations to "OpenClaw" runtime crashes. The user sentiment is mixed, with appreciation for new features but frustration regarding data persistence and update frequency.

## 2. Releases
No new releases were published in the last 24 hours. The project remains on the recent v0.2.4 / v2026.03.16 baseline, which is currently the subject of multiple bug reports regarding migration and stability.

## 3. Project Progress
*   **NIM Gateway Migration (PR #473 - Merged):** Successfully migrated the NetEase IM channel from a direct SDK implementation to the standardized OpenClaw runtime plugin architecture (`openclaw-nim`). This aligns NIM with other gateways like DingTalk and Feishu, improving consistency.
*   **Gateway Stability Fixes (PR #484, #486, #487 - Merged):** Multiple PRs were merged to address gateway restart logic and configuration synchronization.
    *   PR #484 adds functionality to restart the OpenClaw gateway automatically upon startup failure.
    *   PR #487 fixed a critical UI freeze bug where modifying IM configurations during an active session would cause the interface to hang indefinitely in a "streaming" state.
    *   PR #486 ensures configuration changes only trigger a gateway restart upon explicitly clicking "Save."
*   **Scheduled Task Migration (PR #477 - Merged):** Fixed timezone drift issues (8-hour offset) in legacy scheduled tasks and improved error handling for tasks scheduled in the past.
*   **Documentation Update (PR #483 - Merged):** Updated `AGENTS.md` to reflect the new routing architecture (`coworkEngineRouter`, `openclawRuntimeAdapter`) and added development environment variable documentation.

## 4. Community Hot Topics
*   **Plagiarism Accusations ([#435](https://github.com/netease-youdao/LobsterAI/issues/435)) - 5 Comments:**
    *   *Summary:* Users are accusing other "Claw" branded tools (Wind Claw, Zeelin Claw) of being "skins" (clones) of LobsterAI without proper attribution.
    *   *Analysis:* This indicates LobsterAI has achieved a market-leading UI/UX standard that competitors are imitating. It highlights a need for brand protection or clear licensing statements from the maintainers.
*   **Update Friction ([#382](https://github.com/netease-youdao/LobsterAI/issues/382)) - 2 Comments:**
    *   *Summary:* User complains that "all settings need to be refilled" after updates and calls the frequency "poor."
    *   *Analysis:* A critical UX pain point. Frequent updates are breaking local configuration persistence, suggesting the upgrade path between versions (e.g., v0.1.x to v0.2.x) is not automatically migrating user settings.
*   **Context Management ([#485](https://github.com/netease-youdao/LobsterAI/issues/485)) - 1 Comment:**
    *   *Summary:* Request for visibility into context usage (e.g., "140k/200k used"), manual context compression controls, and better loading indicators during compression.
    *   *Analysis:* Power users are hitting token limits and lack visibility. The "black box" nature of context management is causing anxiety about token costs and model performance.

## 5. Bugs & Stability
*   **[CRITICAL] OpenClaw Runtime Instability ([#490](https://github.com/netease-youdao/LobsterAI/issues/490)):** Users report OpenClaw repeatedly crashing and restarting during task execution, halting workflows mid-process.
*   **[HIGH] Scheduled Tasks Vanishing ([#474](https://github.com/netease-youdao/LobsterAI/issues/474)):** Update v2026.3.16 caused existing scheduled tasks to disappear. (Fix likely in PR #477, but user confusion remains).
*   **[HIGH] Sandbox Settings Missing ([#474](https://github.com/netease-youdao/LobsterAI/issues/474)):** Settings UI no longer shows sandbox/local options in the latest version.
*   **[MEDIUM] Ubuntu/AppImage Errors ([#481](https://github.com/netease-youdao/LobsterAI/issues/481)):** Permissions errors accessing `/tmp` and shared memory regions on Linux.
*   **[MEDIUM] Linux Build Breakage ([#476](https://github.com/netease-youdao/LobsterAI/issues/476)):** `npm install` fails on Ubuntu 22.04 with Node v24 due to dependency errors.

## 6. Feature Requests & Roadmap Signals
*   **Telegram Bot Support ([#478](https://github.com/netease-youdao/LobsterAI/issues/478)):** Explicit request to add Telegram integration. *Signal: High.* Given the merged PR #473 which unifies gateway plugins, adding Telegram is likely easier now if the community contributes the `openclaw-telegram` plugin.
*   **Context Transparency ([#485](https://github.com/netease-youdao/LobsterAI/issues/485)):* Requests for a visual context usage bar and manual compression trigger.
*   **Thinking Process Visibility ([#485](https://github.com/netease-youdao/LobsterAI/issues/485)):** Users want to see the model's chain-of-thought, not just the final output, to verify reasoning.

## 7. User Feedback Summary
*   **Pain Points:** The "update experience" is currently negative. Users cite lost settings, lost scheduled tasks, and frequent crashes as major detractors. The phrase "差劲" (poor/bad) was used in [#382](https://github.com/netease-youdao/LobsterAI/issues/382).
*   **Positive Sentiment:** Despite bugs, users acknowledge the software is "getting much better" (Issue #485) and are actively engaging in deep technical discussions about the OpenClaw runtime.
*   **Safety Concerns:** Issue [#489](https://github.com/netease-youdao/LobsterAI/issues/489) reports the AI attempting to execute "dangerous commands," indicating a need for better sandboxing or confirmation prompts before destructive actions.

## 8. Backlog Watch
*   **Node.js Compatibility ([#476](https://github.com/netease-youdao/LobsterAI/issues/476)):** The project mandates Node v24, but `npm install` fails on this version. This is a blocker for new developers trying to build the project.
*   **Local vs. Sandbox Auth ([#124](https://github.com/netease-youdao/LobsterAI/issues/124)):** An issue from February regarding a "401 Invalid Token" error in local mode (while Sandbox works) was bumped today but remains unresolved.
*   **Custom Model Support ([#492](https://github.com/netease-youdao/LobsterAI/issues/492)):** Questions remain about compatibility with non-standard API formats (e.g., `openai-responses`).

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

# TinyClaw Project Digest: 2026-03-19

## 1. Today's Overview
TinyClaw (transitioning to TinyAGI) is in a phase of **heavy architectural refactoring and rebranding**. The project has seen significant activity with **16 Pull Requests updated in the last 24 hours**, all of which have been merged or closed, indicating a high velocity of development. The release of **v0.0.15** marks a major shift in the installation methodology, moving from source-based installation to a binary distribution model via a curl one-liner. While no new issues were reported in the last 24 hours, the volume of merged PRs suggests the team is aggressively stabilizing the codebase and finalizing the rebrand from "TinyClaw" to "TinyAGI."

## 2. Releases
### **v0.0.15 (Latest)**
This release represents a significant maturation of the project's distribution strategy.
*   **New Feature: One-line Installation**: The default install method is now `curl -fsSL https://raw.githubusercontent.com/TinyAGI/tinyagi/main/scripts/install.sh | bash`. This simplifies the onboarding process significantly compared to previous `npx` or clone-based methods.
*   **Data Migration**: The release includes **automatic migration logic** to handle the transition from the old project name (`~/.tinyclaw`) to the new name (`~/.tinyagi`), ensuring existing users do not lose their data during the upgrade.
*   **Installer Robustness**: The installation script now handles native module rebuilding (e.g., `better-sqlite3`) automatically to support cross-platform environments (Linux builds running on macOS).
*   **Release Notes**: [TinyAGI v0.0.15 Release Details](https://github.com/TinyAGI/tinyagi/releases/tag/v0.0.15)

## 3. Project Progress
The project advanced significantly today with the closure of 13 Pull Requests, focused primarily on infrastructure, installation fixes, and rebranding.
*   **Rebranding Finalization**: PRs #191, #234, #237, and #238 successfully completed the transition from "TinyClaw" to "TinyAGI." This included renaming package scopes (`@tinyclaw/*` → `@tinyagi/*`), moving directories, and updating the primary CLI entrypoint to Node.js from shell scripts.
*   **Installation & Onboarding**: PRs #235, #237, and #240 solidified the new installation experience. The team removed redundant scripts (like `migrate.sh` and `remote-install.sh`) in favor of a unified, robust `install.sh`.
*   **Memory & Intelligence**: PR #209 added a **hierarchical memory system** for agents, allowing them to store and recall knowledge using markdown files with YAML frontmatter.
*   **Communication Refactoring**: PR #213 simplified the agent communication schema by removing conversation state tracking, opting for direct flat DMs with immediate streaming to reduce complexity.
*   **Chat Interface**: PR #241 fixed a UX bug where chat messages were displayed in reverse chronological order.

## 4. Community Hot Topics
While the issue tracker is quiet, specific open Pull Requests indicate active community and maintainer debate regarding architectural stability.
*   **Fixing Agent Feedback Loops** ([PR #220](https://github.com/TinyAGI/tinyagi/pull/220))
    *   **Topic**: A critical architectural flaw was identified where `[#team: ...]` messages triggered a "fan-out" to all agents, creating an exponential feedback loop.
    *   **Analysis**: This highlights a core need for better control loops in multi-agent systems. The community is prioritizing stability and resource management over raw autonomy.
*   **Office Workspace Redesign** ([PR #212](https://github.com/TinyAGI/tinyagi/pull/212))
    *   **Topic**: A complete redesign of the `/office` experience.
    *   **Analysis**: There is a strong focus on improving the user interface for the "TinyOffice" component, likely to make the agent's workspace more observable and manageable for humans.
*   **Memory Maintenance** ([PR #233](https://github.com/TinyAGI/tinyagi/pull/233))
    *   **Topic**: Implementing periodic memory maintenance via the heartbeat system.
    *   **Analysis**: As the memory system (added in #209) grows, the team recognizes the need for automated cleanup to prevent "bloat" or hallucination from outdated context.

## 5. Bugs & Stability
*   **Critical (Fix Merged)**: **Chat Message Ordering** ([PR #241](https://github.com/TinyAGI/tinyagi/pull/241))
    *   *Description*: Messages were fetched correctly from the DB (`ORDER BY created_at DESC`) but displayed in reverse order, breaking the conversation flow.
    *   *Status*: **Fixed** in v0.0.15 via a simple array reverse.
*   **High (Fix in Progress)**: **Agent Feedback Loops** ([PR #220](https://github.com/TinyAGI/tinyagi/pull/220))
    *   *Description*: Team messages were triggering recursive agent invocations, potentially causing infinite loops or API rate limiting.
    *   *Status*: **Open**. A fix exists but is not yet merged.
*   **Medium (Fix Merged)**: **Native Module Compatibility** ([PR #240](https://github.com/TinyAGI/tinyagi/pull/240))
    *   *Description*: Pre-built native modules (Linux) were failing on other OSs (macOS).
    *   *Status*: **Fixed**. The installer now rebuilds modules locally.

## 6. Feature Requests & Roadmap Signals
Based on the merged PRs, the project is evolving from a simple CLI tool to a robust autonomous agent platform:
*   **Hierarchical Memory (Implemented)**: Users wanted agents to have long-term memory. This was delivered in PR #209, suggesting future features will focus on knowledge retention.
*   **Web-based Configuration (Implemented)**: PR #214 added web-based setup and custom API URL configuration, indicating a desire to decouple the agent logic from the LLM provider, making it easier for users to plug in local models or custom endpoints.
*   **Heartbeat/Maintenance (In Progress)**: PR #233 suggests a roadmap towards "self-healing" agents that can manage their own storage and memory hygiene.

## 7. User Feedback Summary
*   **Pain Points**:
    *   **Installation Friction**: The sheer number of PRs dedicated to `install.sh` (PRs #235, #237, #240, #239) implies that previous installation methods were brittle or confusing for users.
    *   **Observability**: The push to "redesign the live office workspace" (PR #212) suggests users struggled to understand what their agents were doing or how to interact with them effectively.
*   **Positive Signals**:
    *   The rapid closure of PRs suggests high user engagement and a responsive core team.

## 8. Backlog Watch
*   **[PR #220: Fix Agent Feedback Loops](https://github.com/TinyAGI/tinyagi/pull/220)**
    *   *Priority*: **High**. This PR addresses a stability issue that could degrade user experience (infinite agent loops). It was opened on Mar 16 and remains open.
*   **[PR #212: Redesign Office Workspace](https://github.com/TinyAGI/tinyagi/pull/212)**
    *   *Priority*: **Medium**. It represents a significant UX overhaul. Opened on Mar 13, it is still active as of Mar 18. Completion of this will likely define the "v0.1" experience.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Project Digest: Moltis (2026-03-19)

**Author:** AI Analyst
**Date:** 2026-03-19
**Source:** [github.com/moltis-org/moltis](https://github.com/moltis-org/moltis)

---

### 1. Today's Overview
The Moltis project is currently in a maintenance and stabilization phase, with moderate activity levels reflecting active troubleshooting by the community. In the last 24 hours, there has been no release activity; however, the community is actively identifying instability issues, evidenced by 2 new bug reports and 1 open pull request addressing a tooling panic. The development focus appears to be shifting toward fixing regressions in external integrations (Copilot) and network reliability (web search), indicating a push to improve the robustness of the agent's interface with the web and IDEs.

### 2. Releases
*No new releases published in the last 24 hours.*

### 3. Project Progress
No pull requests were merged in the last 24 hours. However, progress is being made on the stability front:
*   **PR #450** ([fix(tools): prevent web_fetch panic on non-UTF8 pages](https://github.com/moltis-org/moltis/pull/450)) was opened by `koatora20`. This PR addresses a critical panic in the `web_fetch` tool caused by legacy text encodings (GBK, GB18030, Big5), aiming to allow the agent to read web content without crashing.

### 4. Community Hot Topics
The most active discussion revolves around integration stability:
*   **[#261: Github Copilot provider errors](https://github.com/moltis-org/moltis/issues/261)**
    *   **Status:** Open (Updated 2026-03-18)
    *   **Engagement:** 5 comments, 2 👍 reactions
    *   **Analysis:** This is the highest-voted issue recently updated. Users are experiencing failures when trying to use Moltis as a provider for GitHub Copilot. The high comment count suggests users are actively troubleshooting or providing logs, indicating this is a high-priority workflow blockage for developers integrating Moltis into their IDEs.

### 5. Bugs & Stability
Two stability issues were updated yesterday, highlighting current fragility in network operations and third-party integrations:
1.  **[High Severity] Network-filter Proxy / Web Search Failure**
    *   **Issue:** [#407](https://github.com/moltis-org/moltis/issues/407)
    *   **Report:** The `web_search` tool fails immediately after the agent starts.
    *   **Impact:** This represents a critical regression in core agent capabilities (accessing real-time information).
2.  **[Medium Severity] GitHub Copilot Integration Errors**
    *   **Issue:** [#261](https://github.com/moltis-org/moltis/issues/261)
    *   **Report:** Errors occurring when Moltis interacts with the GitHub Copilot API.
    *   **Fix Status:** No fix PR linked yet; remains under investigation.

### 6. Feature Requests & Roadmap Signals
*No new feature requests were explicitly opened in the last 24 hours.* However, **PR #450** signals a roadmap focus on **internationalization and web resilience**. By fixing handling for non-UTF8 pages (common in Asian regions), the project is implicitly prioritizing global usage robustness.

### 7. User Feedback Summary
User sentiment is currently focused on **reliability**. The feedback from Issues #261 and #407 points to frustration with breaking changes in the "latest" version. Specifically, users expect:
*   **Consistent Web Access:** The `web_search` functionality is a core promise of an AI agent; its immediate failure (Issue #407) is a significant pain point.
*   **Seamless IDE Integration:** Developers relying on Moltis via Copilot (Issue #261) are facing friction, suggesting that recent updates may have broken API compatibility.

### 8. Backlog Watch
*   **#420 (Referenced in PR #450):** The underlying issue for `web_fetch` panicking on non-UTF8 pages has been open and is now receiving a fix, suggesting good responsiveness to specific technical bugs.
*   **Maintenance Required:** With no releases pushed despite active bug reports, the backlog appears to be in a "holding pattern" awaiting a patch release (e.g., v0.x.x) to bundle the upcoming `web_fetch` fix and address the Copilot proxy issues.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# Project Digest: CoPaw (agentscope-ai/CoPaw)
**Date:** 2026-03-19
**Analyst:** AI Agent Analyst

## 1. Today's Overview
CoPaw is currently exhibiting **very high development velocity**, with **100 combined updates** (Issues + PRs) in the last 24 hours. The project has released the **v0.1.0-beta.3** update, focusing on console optimization and localization. However, the rapid release cycle appears to have introduced **regressions**, particularly regarding local model loading (llama.cpp) and MCP client stability, resulting in a spike of critical bug reports. Community engagement is intense, with significant focus on expanding multimodal capabilities (file/image upload) and hardening security (authentication).

## 2. Releases
**v0.1.0-beta.3**
*   **Status:** Released.
*   **Key Changes:**
    *   Version bump to `0.1.0b3`.
    *   Console updates: Enhanced multi-language support and optimized document navigation anchors.
*   **Migration Notes:** Users upgrading to this version immediately reported issues with local model loading (ImportErrors), suggesting potential breaking changes in the backend dependencies or path handling.

## 3. Project Progress
**Features Advanced:**
*   **Multimodal Support (Major Milestone):** PR [#1772](https://github.com/agentscope-ai/CoPaw/pull/1772) merged, adding image and file upload support to the Web UI. This resolves a long-standing user request (#675, #1045).
*   **Channel Routing:** PR [#1792](https://github.com/agentscope-ai/CoPaw/pull/1792) (Open) introduces routing logic for multi-agent setups, allowing specific agents to handle messages from channels like Feishu.
*   **Local Embedding:** PR [#1789](https://github.com/agentscope-ai/CoPaw/pull/1789) (Open) adds support for local embedding models (BGE, Qwen3-VL) for long-term memory, enhancing offline capabilities.

**Bug Fixes Merged:**
*   **Chat Model Selection:** PR [#1788](https://github.com/agentscope-ai/CoPaw/pull/1788) fixed issues where model providers/dropdowns were empty or switching models failed post-upgrade.
*   **Local Model Import:** PR [#1784](https://github.com/agentscope-ai/CoPaw/pull/1784) attempted to fix the `ImportError: cannot import name 'create_local_chat_model'` issue affecting Desktop users.

## 4. Community Hot Topics
*   **[Critical] Local Model Load Failure:** Multiple Issues ([#1794](https://github.com/agentscope-ai/CoPaw/issues/1794), [#1795](https://github.com/agentscope-ai/CoPaw/issues/1795), [#1803](https://github.com/agentscope-ai/CoPaw/issues/1803)) report that `llama.cpp` integration is broken in the Desktop v0.10b3 update due to a missing import `create_local_chat_model`.
    *   *Analysis:* High urgency; a regression in the latest release blocking core local LLM functionality.
*   **[Feature] Authentication for Web UI:** Issue [#492](https://github.com/agentscope-ai/CoPaw/issues/492) and [#1046](https://github.com/agentscope-ai/CoPaw/issues/1046) are gaining traction. Users demand password protection for the Console before deploying on public servers.
    *   *Analysis:* Critical security gap for users wanting to expose CoPaw remotely.
*   **[Bug] CPU Usage Spikes:** Issue [#1385](https://github.com/agentscope-ai/CoPaw/issues/1385) reports CPU hitting 100% on Ubuntu 25.10, suspected to be related to MCP `read_file` operations.
    *   *Analysis:* Performance regression requiring immediate optimization.

## 5. Bugs & Stability
*   **Critical (Regression):** `ImportError: cannot import name 'create_local_chat_model'`
    *   *Impact:* Users of Windows Desktop and Linux local models cannot load models.
    *   *Fix Attempt:* PR [#1784](https://github.com/agentscope-ai/CoPaw/pull/1784) was merged, but new reports (#1803) suggest it may not be fully resolved or deployed to all users yet.
*   **High (Data Loss):** Issue [#1805](https://github.com/agentscope-ai/CoPaw/issues/1805) reports "Memory Loss" and system freezing when querying databases created the previous day.
*   **High (UI/UX):** Issue [#1563](https://github.com/agentscope-ai/CoPaw/issues/1563) - `write_file` tool truncates large content (writes only 19% of a 33KB file).
*   **Medium (MCP):** Issue [#1767](https://github.com/agentscope-ai/CoPaw/issues/1767) - Errors during MCP client cleanup when disabling skills.
*   **Medium (Compatibility):** Issue [#823](https://github.com/agentscope-ai/CoPaw/issues/823) - `llama.cpp` fails to load specific GGUF variants (Qwen3.5), resulting in `Failed to load model`.

## 6. Feature Requests & Roadmap Signals
*   **Authentication:** Highly requested (Issues #492, #333, #1046). Expect to see basic auth/password login for the Web UI in upcoming releases to enable safe public deployment.
*   **Execution Tracing:** Issue [#1474](https://github.com/agentscope-ai/CoPaw/issues/1474) requests execution chain logs to debug agent behavior. Related PR [#1781](https://github.com/agentscope-ai/CoPaw/pull/1781) is adding tracing configuration support.
*   **Avatar Customization:** PR [#1791](https://github.com/agentscope-ai/CoPaw/pull/1791) is adding the ability to upload avatars for agents, improving visual distinction in multi-agent setups.
*   **Copy User Messages:** PR [#1802](https://github.com/agentscope-ai/CoPaw/pull/1802) addresses a small but frequent UX annoyance (copying user input).

## 7. User Feedback Summary
*   **Pain Points:**
    *   **Upgrade Friction:** The latest update (`v0.1.0-beta.3` / `v0.10b3`) caused significant disruption for local model users (ImportErrors).
    *   **Model Configuration:** Users struggle with configuring custom providers (Ollama, private models) via the UI, often facing "400 Bad Request" or "Unknown Agent" errors (#1782, #1727).
    *   **File Handling:** While new file upload features are landing, the underlying `write_file` tool is currently unreliable for larger files (#1563).
*   **Positive Sentiment:**
    *   Strong enthusiasm for the new **multimodal/image upload** features.
    *   Active community contributions (many "first-time-contributor" PRs) indicate a healthy, growing ecosystem.

## 8. Backlog Watch
*   **Open Tasks:** Issue [#430](https://github.com/agentscope-ai/CoPaw/issues/430) lists open contribution tasks. Maintainers need to update status for claimed items.
*   **HTTP MCP Support:** Issue [#676](https://github.com/agentscope-ai/CoPaw/issues/676) requests support for HTTP-based MCP servers (currently mostly stdio). PR [#1783](https://github.com/agentscope-ai/CoPaw/pull/1783) recently added 'streamable-http' support, which may resolve this.
*   **File Permissions:** Issue [#973](https://github.com/agentscope-ai/CoPaw/issues/973) requests granular file access controls (read-only vs. read-write) for security. No active PR exists yet.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest: 2026-03-19

## 1. Today's Overview
ZeptoClaw is currently experiencing a phase of active architectural refinement and infrastructure expansion. The project maintains a high velocity with 3 new issues and 2 updated pull requests in the last 24 hours, indicating a responsive maintenance schedule despite a lack of recent releases. The development focus is split between fundamental infrastructure improvements—specifically regarding developer tooling and standardization—and expanding the platform's integration capabilities with major cloud providers. While no features were merged today, the activity suggests a robust effort to stabilize internal libraries and secure external connections before the next deployment cycle.

## 2. Releases
**No new releases** have been published in the last 24 hours. The project appears to be in a development build cycle.

## 3. Project Progress
No pull requests were merged or closed today. Development effort is concentrated on two significant open initiatives:
*   **Provider Expansion:** Work continues on PR #364 to add first-class support for Google Vertex AI, which would enhance enterprise integration capabilities.
*   **Developer Experience:** PR #287 is being updated to establish consistent pre-PR testing environments, aimed at reducing friction for contributors.

## 4. Community Hot Topics
The most discussed topic involves a controversial architectural shift toward sandboxed execution environments.
*   **[#387: Core templates based on Containerfiles... Firecracker VM's](https://github.com/qhkm/zeptoclaw/issues/387)** (4 comments)
    *   **Analysis:** This issue has sparked debate regarding the "feature creep" of coding agent frameworks. The community is actively discussing whether specialized coding agents should be abstracted as standard applications running within lightweight, isolated Firecracker VMs. This reflects a desire within the user base for improved security isolation and a modular approach to AI agent management.

## 5. Bugs & Stability
One protocol-level bug affecting the HTTP channel implementation was identified and requires immediate attention:
*   **[#388: ACP HTTP initialize and notification semantics](https://github.com/qhkm/zeptoclaw/issues/388)** (Severity: Medium/High)
    *   **Details:** A logic error in the ACP HTTP protocol allows subsequent clients to bypass the handshake initialization if a global flag is already set. Furthermore, HTTP notifications are incorrectly receiving response bodies.
    *   **Status:** Reported by the maintainer; no fix PR is open yet. This affects session integrity and requires correction before the next release.

## 6. Feature Requests & Roadmap Signals
Recent issues indicate a strategic pivot toward code modularity and enterprise compliance:
*   **Rig Framework Evaluation:** Issue #389 proposes building core utilities on top of the `0xPlaygrounds/rig` crate. This suggests the team is looking to reduce code duplication and leverage external libraries for generic functions.
*   **Google Vertex AI Support:** PR #364 signals strong intent to release official support for Google Gemini models via `VERTEX_ACCESS_TOKEN` auth, catering to enterprise security requirements.

## 7. User Feedback Summary
The feedback highlights a tension between feature expansion and architectural complexity.
*   **Security Concerns:** Users and contributors are expressing worry over the "security surface expansion" (Issue #387), advocating for the isolation provided by Firecracker VMs.
*   **Maintainability:** There is an explicit request to ease the burden of maintaining generic code by integrating established libraries like `rig`.

## 8. Backlog Watch
Items requiring maintainer attention to prevent drift:
*   **PR #287 (Open for ~10 days):** While important for developer tooling, this PR has been open since early March without being merged. It needs review to ensure local testing standards are adopted.
*   **PR #364 (Open for ~4 days):** The Google Vertex AI provider implementation is pending. Given the complexity of provider integrations, this requires testing to ensure zero-dependency goals are met.

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

# EasyClaw Project Digest
**Date:** 2026-03-19 | **Status:** Active Development

## 1. Today's Overview
EasyClaw (referenced in issues as RivonClaw) exhibits active development with significant focus on internationalization and UI refactoring. The project released version **v1.7.1**, likely a hotfix addressing immediate installation or connectivity barriers observed in v1.7.0. While the issue tracker was cleared of 3 recent items (indicating high responsiveness), 2 new Pull Requests regarding UI architecture and multi-language support are pending review. Community sentiment leans towards technical curiosity, though recent reports indicate potential stability regressions in the latest Windows release.

## 2. Releases
**v1.7.1 (RivonClaw)**
*   **Status:** Released.
*   **Key Note:** The release notes specifically address a "Gatekeeper" issue on macOS where the unsigned app is blocked by security settings. This suggests v1.7.1 primarily focuses on ensuring usability on macOS systems where the application might be flagged as damaged.
*   **Context:** This release follows user reports of connectivity issues in v1.7.0, though the patch notes visible here focus on the macOS workaround.

## 3. Project Progress
*   **Pending UI Migration:** PR #20 is currently open, aiming to modernize the interface by extracting `<BottomActions>` components, consolidating SVGs into a base `Icon` class, and separating theme logic.
*   **Internationalization (i18n):** PR #21 has been submitted to add 5 new languages (Traditional Chinese, Japanese, Korean, Vietnamese, Hindi), covering 1,333 translation keys. This signals a strong push for global accessibility.

## 4. Community Hot Topics
*   **Connectivity Failures in v1.7.0 (Windows):**
    *   **[Issue #18](https://github.com/gaoyangz77/rivonclaw/issues/18)** (Closed) & **[Issue #19](https://github.com/gaoyangz77/rivonclaw/issues/19)** (Closed): Multiple users reported being "stuck connecting" after upgrading from v1.6.8 to v1.7.0 on Windows 11.
    *   **Analysis:** The recurrence of this issue suggests a regression in the network handling or API configuration logic within the v1.7.0 update cycle.
*   **Community Engagement:**
    *   **[Issue #12](https://github.com/gaoyangz77/rivonclaw/issues/12)** (Closed): Users requested a technical discussion group, praising the project's architecture. The closure suggests a channel may have been established or the request was acknowledged.

## 5. Bugs & Stability
*   **Severity: High - Connection/Login Regression (Windows)**
    *   **Description:** Users upgrading to v1.7.0 faced a complete inability to connect or register, even with valid API configurations.
    *   **Status:** Issues #18 and #19 were closed on March 18. While no specific fix PR is listed in today's data, the closure coupled with the release of v1.7.1 suggests these connectivity bugs were likely addressed in the latest patch.
*   **Severity: Medium - macOS "Damaged" File Warning**
    *   **Description:** macOS blocks the application due to lack of code signing.
    *   **Mitigation:** The project provided explicit terminal instructions to bypass Gatekeeper, acknowledging the limitation of the current build process.

## 6. Feature Requests & Roadmap Signals
*   **Multi-language Support:** The submission of PR #21 indicates that localization is a high-priority roadmap item for the next developmental iteration.
*   **UI/UX Refinement:** PR #20 highlights a move towards a more modular component architecture, likely improving maintainability and enabling the new "Skills Page" feature mentioned in the PR summary.

## 7. User Feedback Summary
*   **Pain Points:** The update experience from v1.6.8 to v1.7.0 was turbulent for Windows users, resulting in "stuck" interfaces and non-functional connections. The rapid closure of these issues (within 1-2 days) suggests the maintainers are reacting quickly to instability.
*   **Positive Feedback:** A user explicitly noted that the "EasyClaw project architecture fits my expectations very well," indicating strong approval from the developer community regarding the codebase structure.

## 8. Backlog Watch
*   **Review Pending:** PRs #20 and #21 require maintainer review to merge the UI refactor and new languages. These represent significant structural changes that should be prioritized to prevent merge conflicts later.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*