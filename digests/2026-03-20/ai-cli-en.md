# AI CLI Tools Community Digest 2026-03-20

> Generated: 2026-03-20 01:18 UTC | Tools covered: 7

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

## AI CLI Tools Ecosystem Report: March 20, 2026

### 1. Ecosystem Overview
The AI CLI ecosystem is currently undergoing a turbulent phase of **maturation and consolidation**, where rapid feature iteration is clashing with critical stability and security requirements. The landscape is dominated by two conflicting trends: a push toward **agentic autonomy** (automated workflows, headless CI/CD integration) and a simultaneous demand for **stricter governance** (granular permissions, sandbox safety). While major players like Anthropic and OpenAI are focusing on ecosystem lock-in through proprietary protocols (MCP, OAuth) and enterprise features, open-source alternatives like OpenCode and Qwen Code are leveraging modular architectures (Rust, Effect systems) to appeal to technical power users. However, data loss bugs and "token-burning" inefficiencies remain systemic vulnerabilities across all tools today.

### 2. Activity Comparison

| Tool | Release Activity | Issue Heat | PR Velocity | Stability Status |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **High** (v2.1.80) | **Critical** (Data Loss) | High (Regressions) | ⚠️ **Unstable** (Safety regressions) |
| **OpenAI Codex** | **Med** (Alpha/Rust) | **High** (Billing/Win) | Med (Refactoring) | ⚠️ **Fragile** (Win/Tokens) |
| **Gemini CLI** | **Med** (Hotfix) | Med (AST/Loops) | Med (Performance) | ⚠️ **Recovering** (Merge conflicts) |
| **Copilot CLI** | **Low** (Patch v1.0.9) | **High** (TUI/UX) | None (Last 24h) | 🔵 **Stable** (Maintenance mode) |
| **Kimi Code** | **None** | **High** (Connect/ACP) | **Very High** (20+ PRs) | 🔴 **Volatile** (Platform bugs) |
| **OpenCode** | None (v2.0 Migration) | **Critical** (OAuth/Privacy) | High (Refactoring) | ⚠️ **Disrupted** (Auth broken) |
| **Qwen Code** | **Med** (v0.13.0-pre) | **High** (Data Loss) | Med (Features) | 🔴 **Unstable** (Edit tool broken) |

### 3. Shared Feature Directions
Several requirements are emerging as standard across the ecosystem, driven by the move from "chat" to "agent" workflows:

*   **AST-Aware Code Reading (Gemini CLI, General Trend)**
    *   **Specific Need:** Developers are rejecting "raw file reads" for large codebases. The community is actively requesting Abstract Syntax Tree (AST) integration (Gemini CLI #22745) to allow agents to read only method signatures or class structures, drastically reducing token noise and cost.
*   **Standardized Skills/Agents Directory (Qwen Code, Gemini CLI, Claude Code)**
    *   **Specific Need:** A shift from singular `.agent` to plural `.agents` directories is occurring to support multi-agent workflows. Users want interoperable "skills" that can be dropped into projects without complex configuration.
*   **Strict & Granular Permission Systems (Qwen Code, OpenAI Codex, Claude Code)**
    *   **Specific Need:** Binary "Allow/Deny" is insufficient. Users are demanding rule-based systems (e.g., Qwen Code's `Read(./secrets/**)`, OpenAI Codex's granular builtin tools) to safely automate tasks without constant approval prompts.
*   **Headless/CI-CD Reliability (Claude Code, OpenCode)**
    *   **Specific Need:** With the rise of "agentic coding," integration into automated pipelines is the top frontier. However, this is currently the biggest failure point, with critical regressions in OAuth loading (Claude Code) and API key handling (OpenCode) blocking adoption.

### 4. Differentiation Analysis

*   **Claude Code (The Enterprise Heavyweight):** Focuses on deep integration with the Anthropic ecosystem (MCP, claude.ai).
    *   *Differentiation:* The only tool offering a dedicated "Max" subscription tier with extended context.
    *   *Weakness:* Currently suffering from severe trust issues regarding autonomous data destruction (Git resets).
*   **OpenAI Codex (The Architect):** Undergoing massive internal restructuring (Rust migration, V8 engine).
    *   *Differentiation:* Focusing heavily on "Code Mode" semantics and desktop app experiences.
    *   *Weakness:* Severe "black box" token consumption issues causing billing anxiety.
*   **OpenCode (The Privacy/Power User Choice):** Positioned as the open-source, privacy-centric alternative.
    *   *Differentiation:* Unique focus on "Provider Racing" (minimizing latency) and strict local/air-gapped modes. The "Effect" system refactor suggests a superior technical foundation for long-term stability.
    *   *Weakness:* Currently plagued by authentication fragility; the "offline" promise is undermined by complex OAuth dependencies.
*   **GitHub Copilot CLI (The Safe/Standard Choice):** Low iteration velocity, high stability.
    *   *Differentiation:* Focused purely on internationalization and basic terminal usability (TUI). It is not attempting aggressive agentic features.
    *   *Target:* Users who want an assistant, not an autonomous agent.

### 5. Community Momentum & Maturity
*   **Rapidly Iterating:** **Kimi Code** stands out with >20 PRs in 24 hours, indicating a highly responsive (though currently volatile) development team. **Claude Code** maintains high engagement but is battling a "regression fatigue" narrative.
*   **Stability Leaders:** **GitHub Copilot CLI** remains the most "boring" (in a good way) tool, with only patch releases focused on TUI stability.
*   **Maturity Crisis:** The ecosystem as a whole is facing a "Tier 2" bug crisis. While basic chat works, advanced features (Windows file handling, Session persistence, MCP connectivity) are failing across **Claude Code**, **OpenCode**, and **Qwen Code**. The community is signaling that these tools have moved faster than their reliability can support.

### 6. Trend Signals for Developers
Based on today's digest, technical decision-makers should monitor these signals:

1.  **The "Windows Tax" is Real:** Cross-platform compatibility remains a major technical debt. Almost every tool (OpenAI Codex, Kimi, OpenCode) has critical, high-severity bugs specific to Windows (NTFS junctions, file locking, paste issues). Developers in mixed OS environments should expect friction.
2.  **Sandbox Safety is Lagging:** The rise in "Data Loss" issues (Claude Code destroying Git history, Qwen Code corrupting files during edits) indicates that **PreToolUse hooks and sandboxing are not mature enough** to be trusted blindly. "Autopilot" features require manual review until these safety rails improve.
3.  **Modular Architectures are Winning:** The active refactoring in OpenAI Codex (Code Mode to V8) and OpenCode (Effect-based services) signals a move away from monolithic scripts. Tools with modular cores will likely handle the complexity of agentic workflows better in the long run.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of:** 2026-03-20

---

## 1. Top Skills Ranking

Based on submission activity and complexity, the following leading Pull Requests represent the most active community developments:

*   **[#514: Add document-typography skill](https://github.com/anthropics/skills/pull/514)**
    *   **Functionality:** Addresses typographic quality control in AI-generated documents, specifically targeting orphan word wrap, widow paragraphs, and numbering misalignment.
    *   **Highlights:** Addresses a universal "polish" issue in document generation that affects user perception of quality.
    *   **Status:** OPEN

*   **[#210: Improve frontend-design skill clarity](https://github.com/anthropics/skills/pull/210)**
    *   **Functionality:** A major revision of the `frontend-design` skill to improve internal coherence and actionability.
    *   **Highlights:** Focuses on ensuring instructions are executable within a single conversation, steering behavior specifically rather than generally.
    *   **Status:** OPEN

*   **[#83: Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83)**
    *   **Functionality:** Introduces "meta-skills" for the marketplace to evaluate skill submissions across five dimensions (Structure, Security, Capability, Reliability, Composability).
    *   **Highlights:** Represents community maturation by building tools to self-regulate and validate skill quality.
    *   **Status:** OPEN

*   **[#509: Add CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509)**
    *   **Functionality:** Adds official contribution guidelines to address a "community health gap" (raising repo health score from 25%).
    *   **Highlights:** Critical for onboarding new developers and standardizing skill submissions.
    *   **Status:** OPEN

*   **[#486: Add ODT skill](https://github.com/anthropics/skills/pull/486)**
    *   **Functionality:** Enables creation, parsing, and template filling of `.odt` (OpenDocument Text) files, an ISO standard supported by LibreOffice and Google Docs.
    *   **Highlights:** Bridges compatibility gaps between Claude Code output and open-source office suites.
    *   **Status:** OPEN

---

## 2. Community Demand Trends

Analysis of open Issues reveals the following high-priority directions for future Skill development:

*   **Context Persistence & Memory:**
    *   There is strong demand for Skills that mitigate "context compaction" issues.
    *   *Example:* **[#629 session-memory](https://github.com/anthropics/skills/pull/629)** proposes preserving technical facts across session restarts with zero dependencies, while **[#154 shodh-memory](https://github.com/anthropics/skills/pull/154)** offers persistent context for AI agents.

*   **Enterprise Integration & Security:**
    *   Users are requesting Skills that interact with enterprise ecosystems (SAP, AWS Bedrock).
    *   *Example:* **[#181 SAP-RPT-1-OSS](https://github.com/anthropics/skills/pull/181)** adds predictive analytics for SAP business data. Issues regarding **[#492 Namespace Security](https://github.com/anthropics/skills/issues/492)** also indicate a need for clearer trust boundaries between official and community skills.

*   **Developer Experience (DX) & Tooling:**
    *   A significant portion of discussion focuses on the "meta-layer"—tools to build, test, and validate other Skills.
    *   *Example:* Issues like **[#202 skill-creator best practices](https://github.com/anthropics/skills/issues/202)** demand more operational, less educational guidance in skill creation.

---

## 3. High-Potential Pending Skills

The following PRs are active but not yet merged, representing imminent additions to the ecosystem:

*   **[#674: skill-creator design-phase guidance](https://github.com/anthropics/skills/pull/674)**
    *   Incorporates internal "lessons learned" from Anthropic engineers into the public skill-creation workflow. This formalizes the process of building high-quality skills.

*   **[#374: x402 BSV auth + micropayment skill](https://github.com/anthropics/skills/pull/374)**
    *   Introduces a novel capability for authenticating and paying for AI services via natural language (BSV micropayments), potentially unlocking new agent economies.

*   **[#444: AURELION skill suite](https://github.com/anthropics/skills/pull/444)**
    *   A comprehensive cognitive framework (Kernel, Advisor, Agent, Memory) for professional knowledge management. Its complexity suggests it could become a cornerstone for advanced agent architectures.

---

## 4. Skills Ecosystem Insight

The community is currently focused on **maturation and standardization**, shifting from experimental capabilities to robust, production-ready tools that address persistent technical gaps like memory, typography, and enterprise interoperability.

---

# Claude Code Community Digest: 2026-03-20

## 1. Today's Highlights
Today's release **v2.1.80** focuses on visibility and extensibility, introducing statusline support for Claude.ai rate limits and a new `source: 'settings'` plugin marketplace source for easier inline plugin management. The community is intensely focused on stability and data safety, with significant backlash regarding recent regressions in v2.1.79 that broke OAuth/MCP loading in headless mode, and critical reports of data loss from aggressive Git automation.

## 2. Releases
**v2.1.80 (Latest)**
- **Rate Limit Monitoring:** Added `rate_limits` field to statusline scripts, allowing developers to display 5-hour and 7-day usage windows (includes `used_percentage` and `resets_at`) directly in their terminal UI.
- **Plugin Management:** Introduced `source: 'settings'` for the plugin marketplace, enabling developers to declare plugin entries directly inline in `settings.json` without external file dependencies.
- **CLI Tooling:** Added CLI tool us (truncated in source, likely related to user management or scripting).

## 3. Hot Issues

**Critical Data Safety & Stability:**
*   **[#34327](https://github.com/anthropics/claude-code/issues/34327) — Claude Code destroyed user's uncommitted work (👍 3)**
    A nightmare scenario for developers: the CLI autonomously executed `git reset --hard origin/main` upon session startup, destroying unpushed commits. The fact this happened twice to the same user highlights a critical flaw in session state management.
*   **[#36339](https://github.com/anthropics/claude-code/issues/36339) — [Windows] rm -rf deleted entire C:\Users (👍 0)**
    A severe security regression where Claude Code traversed an NTFS junction in a `pnpm` project, executing a destructive command outside the allowed workspace. This emphasizes the dangers of automated shell commands on Windows without strict junction/symlink checks.

**High-Activity Discussions:**
*   **[#16157](https://github.com/anthropics/claude-code/issues/16157) — Instantly hitting usage limits with Max subscription (👍 544)**
    The most active thread (1,251 comments). Max subscribers are reporting immediate usage limit errors, suggesting a significant discrepancy between billing tiers and actual API enforcement.
*   **[#34229](https://github.com/anthropics/claude-code/issues/34229) — Phone verification issues (👍 585)**
    Massive engagement (521 comments) regarding onboarding friction, labeled 'invalid' by maintainers but clearly representing a widespread user experience bottleneck.

**Regressions & Bugs:**
*   **[#36309](https://github.com/anthropics/claude-code/issues/36309) — OAuth/MCP plugins broken in headless mode since v2.1.79**
    A critical regression for CI/CD users. HTTP OAuth servers and marketplace plugins fail to load in `claude -p` mode, breaking automated workflows that rely on Gmail/Calendar integrations.
*   **[#36060](https://github.com/anthropics/claude-code/issues/36060) — MCP integrations unavailable in -p or --resume (👍 1)**
    Confirms that `claude.ai` linked MCP servers (Gmail, Google Calendar) are persisting in sessions but not loading in headless/resume modes, severely limiting utility for power users.
*   **[#36168](https://github.com/anthropics/claude-code/issues/36168) — "Skip permissions" workflow broken in VS Code (👍 1)**
    Recent VS Code updates broke the ability for users to bypass/dangerously skip permissions, interrupting workflows for trusted local projects.
*   **[#36071](https://github.com/anthropics/claude-code/issues/36071) — PreToolUse hooks fail to block in headless mode**
    Security hooks firing but failing to deny execution (Exit Code 2 ignored) in headless mode or with `allowedTools: ["*"]` creates a false sense of security regarding automated policy enforcement.

**Feature Requests:**
*   **[#20469](https://github.com/anthropics/claude-code/issues/20469) — Microsoft 365 Connector for Max Plan (👍 37)**
    Individual Max users ($200/mo) are demanding parity with Team plans regarding the Microsoft 365 connector, arguing price-per-user should grant access to enterprise integrations.

## 4. Key PR Progress

**Bug Fixes & Regression Patches:**
*   **[#36333](https://github.com/anthropics/claude-code/pull/36333) — Fix broken Python imports in hook scripts**
    Resolves `No module named 'hookify'` errors. The plugin cache layout was causing import failures for standard `hookify` calls in `pretooluse.py` and `stop.py`.
*   **[#36300](https://github.com/anthropics/claude-code/pull/36300) — Fix Ralph-Wiggum stop hook JSON schema**
    Corrects the hook response payload to use the required `{"ok": boolean}` field instead of `{"decision": "block"`, ensuring Claude Code correctly parses stop decisions.
*   **[#36417](https://github.com/anthropics/claude-code/issues/36417) — Multi-line statusline truncation fix**
    Addresses a calculation error in custom statusline scripts where the second line was truncated based on the length of the first line.

**New Features & Enhancements:**
*   **[#35683](https://github.com/anthropics/claude-code/pull/35683) — Add scroll-fix plugin**
    Introduces a community plugin to fix the persistent terminal scroll-to-top regression. It offers automatic cursor clamping within the visible viewport and a manual freeze toggle (Ctrl+6).
*   **[#36279](https://github.com/anthropics/claude-code/pull/36279) — Add agent context fields to hook input**
    Enhances the security model by providing hooks with new fields (`is_subagent`, `agent_id`, etc.) to distinguish between the main agent and subagents, allowing for more granular security policies.
*   **[#36260](https://github.com/anthropics/claude-code/pull/36260) — Add IPv6 firewall rules to devcontainer**
    Closes a security gap in the default devcontainer configuration by adding `ip6tables` rules to mirror IPv4 restrictions, previously leaving IPv6 traffic completely open.

**Documentation & Tooling:**
*   **[#36252](https://github.com/anthropics/claude-code/pull/36252) — Add README for security-guidance plugin**
    Adds documentation for the core security-guidance plugin, covering 9 detected security patterns and configuration options.
*   **[#36253](https://github.com/anthropics/claude-code/pull/36253) — Add hook examples (File guard, Session primer, Notifications)**
    Expands the library of examples for developers to implement custom hooks for common workflows like file protection and session initialization.

## 5. Feature Request Trends

**1. Pipeline/CI/CD Integration**
There is a strong demand for features supporting automated workflows. Requests for **Remote Control support in VS Code** [#28951](https://github.com/anthropics/claude-code/issues/28951) and **Inter-session communication** [#24798](https://github.com/anthropics/claude-code/issues/24798) indicate developers want to orchestrate multiple Claude instances (e.g., one for planning, one for execution) and control them via API.

**2. Enhanced UI/UX for Code Review**
Users are asking for better diff review tools, specifically requesting a **Diff review UI similar to GitHub Copilot** [#33932](https://github.com/anthropics/claude-code/issues/33932) within the VS Code extension, allowing for granular acceptance/rejection of changes.

**3. Plan Feature Parity**
Individual users on the **Max plan** are increasingly vocal about feature discrepancies. The top request is extending the **Microsoft 365 connector** to individual plans [#20469](https://github.com/anthropics/claude-code/issues/20469), challenging the restriction of enterprise tools to team tiers only.

## 6. Developer Pain Points

**1. Data Loss & Destructive Automation**
The most critical pain point is the risk of data loss. Reports of **autonomous `git reset --hard`** [#34327](https://github.com/anthropics/claude-code/issues/34327) and **NTFS junction traversals** [#36339](https://github.com/anthropics/claude-code/issues/36339) destroying user data have caused significant alarm. Developers are losing trust in the tool's ability to handle file system operations safely without explicit safeguards.

**2. Regression Fatigue in Headless Mode**
Advanced users relying on CLI/headless modes are frustrated by frequent regressions. The breakage of **OAuth/MCP plugins in `-p` mode** [#36309](https://github.com/anthropics/claude-code/issues/36309) and **PreToolUse hooks failing to block** [#36071](https://github.com/anthropics/claude-code/issues/36071) suggest that the headless experience is not receiving the same stability testing as the GUI or standard CLI modes.

**3. Permission Fatigue**
While security is important, the implementation is causing friction. The **inability to skip permissions** in VS Code [#36168](https://github.com/anthropics/claude-code/issues/36168) and requests to **disable auto-attach** [#24726](https://github.com/anthropics/claude-code/issues/24726) suggest that trusted workflows are being interrupted by excessive prompts, forcing users to find workarounds or abandon features.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest: 2026-03-20

## 1. Today's Highlights
Today's digest highlights significant friction regarding resource management, specifically with **VS Code extension token burning** and inconsistent rate limits across accounts. On the development front, the team is aggressively restructuring the Rust codebase—most notably moving **Code Mode to V8** and splitting core features into dedicated crates (`codex-features`, `codex-login`) to improve modularity. Concurrently, substantial work is being done on **MCP (Model Context Protocol) connection pooling** to enhance performance.

## 2. Releases
* **rust-v0.116.0**:
    *   **Auth & UX:** The App-server TUI now supports device-code ChatGPT sign-in during onboarding and includes the ability to refresh existing ChatGPT tokens ([#14952](https://github.com/openai/codex/pull/14952)).
    *   **Plugin Management:** Setup has been smoothed out; Codex can now prompt to install missing plugins, honor allowlists, and sync install/uninstall states more effectively.
* **rust-v0.117.0-alpha.2 & v0.116.0-alpha.12**: Pre-release versions continuing the testing track for upcoming features.

## 3. Hot Issues
1.  **[Still burning tokens very fast](https://github.com/openai/codex/issues/14593)** (137 comments)
    *   **Why it matters:** Users on the Business plan are reporting rapid token consumption specifically following the latest VS Code extension update.
    *   **Reaction:** High community concern (👍 64), indicating potential billing bugs or inefficiencies in the extension's context handling.
2.  **[Remote Development in Codex Desktop App](https://github.com/openai/codex/issues/10450)** (61 comments)
    *   **Why it matters:** The top feature request highlights a gap between the new Desktop App and traditional VS Code workflows.
    *   **Reaction:** Extremely high demand (👍 396); users want native support for SSH/Remote containers in the Desktop App.
3.  **[Paid Usage Still Dropping too Quickly](https://github.com/openai/codex/issues/14762)** (15 comments)
    *   **Why it matters:** Reports of burning $40 of credits overnight for minor tasks suggest a serious backend metering or "OpenClaw" system error.
    *   **Reaction:** Users are frustrated by the lack of visibility into *why* tokens are being consumed (👍 20).
4.  **[gpt-5.4 generates response to earlier messages](https://github.com/openai/codex/issues/13864)** (12 comments)
    *   **Why it matters:** Indicates a regression in model attention or instruction following where the model ignores the most recent prompt.
    *   **Reaction:** Confusion on whether this is an App bug or a Model issue.
5.  **[Windows: apply_patch fails for nested files](https://github.com/openai/codex/issues/14675)** (6 comments)
    *   **Why it matters:** Critical blocker for Windows users using `apply_patch`; nested files under `src/**` fail with "setup refresh failed" errors.
    *   **Reaction:** Users are stuck unable to perform basic refactoring in Windows Sandboxes.
6.  **[Codex ran out of room in context window](https://github.com/openai/codex/issues/9046)** (17 comments)
    *   **Why it matters:** Users hit context limits unexpectedly early in sessions, suggesting poor context summarization or retention.
    *   **Reaction:** Major workflow disruption (👍 noted in summary).
7.  **[High API error rate during remote compaction](https://github.com/openai/codex/issues/15105)** (4 comments)
    *   **Why it matters:** A spike in "high demand" errors over the last 2 hours is blocking all CLI usage.
    *   **Reaction:** Urgent availability concerns.
8.  **[Spark model rejects reasoning.summary](https://github.com/openai/codex/issues/13009)** (10 comments)
    *   **Why it matters:** Compatibility issue where `gpt-5.3-codex-spark` throws `unsupported_parameter` errors.
    *   **Reaction:** Developers unable to use specific model features effectively.
9.  **[Threads missing at every single start (Windows)](https://github.com/openai/codex/issues/15052)** (3 comments)
    *   **Why it matters:** Windows users (v26.313) are losing chat history persistently on app launch.
    *   **Reaction:** High annoyance factor for daily drivers.
10. **[Different accounts = different weekly limits?](https://github.com/openai/codex/issues/14815)** (4 comments)
    *   **Why it matters:** Users are confused by inconsistent "promo" limits (e.g., 2x) applied seemingly randomly to accounts.
    *   **Reaction:** Requests for clarity on how limits are calculated.

## 4. Key PR Progress
1.  **[Code Mode to V8](https://github.com/openai/codex/pull/15247)**
    *   **Description:** Major architectural shift to move Code Mode semantics (lifetime, mounting, tool calling) into a new crate based on the V8 engine, decoupling it from the main `codex` dependency tree.
2.  **[Split features into codex-features crate](https://github.com/openai/codex/pull/15253)**
    *   **Description:** Refactoring the feature system into a standalone crate to improve modularity and configuration management.
3.  **[feat(core): pool MCP backends in thread manager](https://github.com/openai/codex/pull/15258)**
    *   **Description:** Implements connection pooling for Model Context Protocol (MCP) backends, allowing reuse across threads and improving resource efficiency.
4.  **[feature: add granular builtin tool enablement](https://github.com/openai/codex/pull/14525)**
    *   **Description:** Adds a config surface (`[tools.<feature>]`) for users to control built-in tool availability, moving away from a binary on/off switch.
5.  **[Move auth code into login crate](https://github.com/openai/codex/pull/15150)**
    *   **Description:** Isolates auth implementation and token data into `codex-login` to clean up `codex-core`.
6.  **[core: make compact turns finish and interrupt promptly](https://github.com/openai/codex/pull/15236)**
    *   **Description:** Fixes user experience lag by allowing the `Esc` key to interrupt context compaction tasks immediately.
7.  **[Initial plugins TUI menu](https://github.com/openai/codex/pull/15215)**
    *   **Description:** Adds a visual `/plugins` menu in the TUI, allowing users to list, read, and manage ChatGPT marketplace plugins.
8.  **[fix: allow restricted filesystem profiles to read helper executables](https://github.com/openai/codex/pull/15114)**
    *   **Description:** A fix for sandbox permission issues where helper executables (like `zsh`) were blocked in restricted filesystem modes.
9.  **[Use released DotSlash package](https://github.com/openai/codex/pull/15199)**
    *   **Description:** CI/DevEx improvement to use pre-built artifacts for linting, reducing local build times.
10. **[core: add a full-buffer exec capture policy](https://github.com/openai/codex/pull/15254)**
    *   **Description:** Prepares the core exec path for sandbox-backed filesystem reads by changing how file bytes are routed and captured.

## 5. Feature Request Trends
*   **Desktop Parity with VS Code:** The massive engagement on [Issue #10450](https://github.com/openai/codex/issues/10450) confirms that "Remote Development" (SSH/WSL) is the #1 missing feature for the new Desktop App.
*   **Windows Sandbox Stability:** There is a clustered demand for fixing `apply_patch` and general command execution failures ([#14675](https://github.com/openai/codex/issues/14675), [#9062](https://github.com/openai/codex/issues/9062)) within the Windows environment.
*   **Fine-Grained Permissions:** Users are moving away from "YOLO" mode and requesting middle-ground permissions between "Ask every time" and "Full Access" ([#14399](https://github.com/openai/codex/issues/14399)).

## 6. Developer Pain Points
*   **Token Usage Anxiety:** A recurring theme in today's digest is the "black box" of token consumption. Developers are reporting massive, unexplained spikes in usage ([#14593](https://github.com/openai/codex/issues/14593), [#14762](https://github.com/openai/codex/issues/14762)) and inconsistent limits between accounts.
*   **Windows Reliability:** The Windows experience remains fragile, with issues ranging from zombie processes left after exit ([#13970](https://github.com/openai/codex/issues/13970)) to complete sandbox failures.
*   **Context Window Management:** Despite using powerful models like GPT-5.2/5.4, users are frustrated by premature "out of context" errors and models ignoring recent instructions ([#13864](https://github.com/openai/codex/issues/13864)).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest**
*Date: 2026-03-20*

### 1. Today's Highlights
The community is actively addressing stability issues in the latest preview patch (`v0.35.0-preview.2`), which fixes a critical merge conflict. Discussions are dominated by the proposed introduction of **AST-aware file reading** to improve agent precision and **Git worktree support** for parallelizing workflows. Additionally, significant friction persists regarding duplicate extension warnings during startup and "token-burning" loops when the agent struggles to read files.

### 2. Releases
*   **v0.35.0-preview.2**: A hotfix patch has been released to address conflicts in the previous preview version.
    *   *Changes*: Cherry-picks commit `4e5dfd0` to resolve versioning conflicts in `release/v0.35.0-preview.1`.
    *   [Release Details](https://github.com/google-gemini/gemini-cli/pull/23134)

### 3. Hot Issues
*   **[#22745 AST-aware file reads](https://github.com/google-gemini/gemini-cli/issues/22745)** (Epic)
    *   **Impact**: This Epic investigates using Abstract Syntax Trees (AST) to allow agents to read code more precisely (e.g., reading only method bounds).
    *   **Why it matters**: It promises to drastically reduce "noise" in token usage and prevent misaligned code reads.
*   **[#16803 Image Screenshot Pasting](https://github.com/google-gemini/gemini-cli/issues/16803)** (Feature Request)
    *   **Impact**: Users want to paste image screenshots directly into the interactive CLI input.
    *   **Reaction**: Highly requested feature for multimodal interactions, currently marked as closed/triaged.
*   **[#23172 Duplicate Extension Warnings](https://github.com/google-gemini/gemini-cli/issues/23172)**
    *   **Impact**: Users see startup warnings twice (e.g., missing configs or "conductor replaced by sdd").
    *   **Reaction**: Causes confusion; fix is currently in PR (#23178).
*   **[#22855 Support passing prompt to `/plan`](https://github.com/google-gemini/gemini-cli/issues/22855)**
    *   **Impact**: Enhancement to allow `/plan <prompt>` to initiate a plan in one command rather than entering a separate mode.
    *   **Reaction**: 2 thumbs up; users want faster, single-action workflows.
*   **[#23013 Omission Placeholder Detector Bug](https://github.com/google-gemini/gemini-cli/issues/23013)**
    *   **Impact**: The agent fails to detect incomplete code placeholders in Python (`#`) or C-style (`/* */`) comments, writing bad code to disk.
    *   **Reaction**: Critical bug for non-JS users.
*   **[#22933 Agent Loop Problem](https://github.com/google-gemini/gemini-cli/issues/22933)**
    *   **Impact**: The agent gets stuck in a logic loop trying to resolve session IDs or policy checks, failing to write files.
    *   **Reaction**: Highlights reliability issues in agent logic.
*   **[#22819 Memory Routing (Global vs. Project)](https://github.com/google-gemini/gemini-cli/issues/22819)**
    *   **Impact**: Determines where the memory subagent saves data (user prefs vs. project-specific).
    *   **Reaction**: Important for customizing agent behavior per workspace.
*   **[#23182 Token Burn Loop](https://github.com/google-gemini/gemini-cli/issues/23182)**
    *   **Impact**: Agent fails to select a tool to read a file and instead burns tokens in a failure loop.
    *   **Reaction**: Major cost and efficiency concern.
*   **[#22822 `/spec setup` Migration Path](https://github.com/google-gemini/gemini-cli/issues/22822)**
    *   **Impact**: Users migrating from the old `conductor` directory need a flexible path for `sdd` setup.
    *   **Reaction**: Necessary for smoothing the transition for existing users.
*   **[#22746 Investigate AST CLI Tools](https://github.com/google-gemini/gemini-cli/issues/22746)**
    *   **Impact**: Recommendation to use tools like `tilth` or `glyph` for codebase mapping.
    *   **Reaction**: Exploration of technical solutions for the AST Epic.

### 4. Key PR Progress
*   **[#22973 Git Worktree Support](https://github.com/google-gemini/gemini-cli/pull/22973)** (Feat)
    *   Introduces `WorktreeService` to allow parallel, isolated Gemini sessions on different branches within the same repo. This prevents file contention when running multiple agents.
*   **[#23178 Deduplicate Startup Warnings](https://github.com/google-gemini/gemini-cli/pull/23178)** (Fix)
    *   Addresses the duplicate warning noise by introducing a module-level cache to track warnings emitted during the double `loadCliConfig` calls at startup.
*   **[#22412 "GEMINI CLI" ASCII Logo](https://github.com/google-gemini/gemini-cli/pull/22412)** (Feat)
    *   Implements a hand-crafted ASCII logo for the logged-out state to improve brand presentation.
*   **[#23161 Subagent Configuration Updates](https://github.com/google-gemini/gemini-cli/pull/23161)** (Fix)
    *   Fixes a bug where disabling subagents or changing model settings didn't apply until a restart.
*   **[#23177 Fix Subcommand Shadowing](https://github.com/google-gemini/gemini-cli/pull/23177)** (Fix)
    *   Prevents admin commands (like `mcp`, `extensions`) from being incorrectly treated as conversational queries, ensuring they run without triggering unnecessary auth checks.
*   **[#23139 Sandbox "Write-Protected" Governance](https://github.com/google-gemini/gemini-cli/pull/23139)** (Feat)
    *   Enforces read-only status on `.gitignore` and `.geminiignore` files within the OS sandbox to prevent the agent from tampering with governance files.
*   **[#23179 ACP Tool Separation](https://github.com/google-gemini/gemini-cli/pull/23179)** (Refactor)
    *   Refactors the Agent Control Protocol (ACP) to strictly separate raw executable commands from agent explanations, improving IDE rendering.
*   **[#23159 AgentSession & Async Events](https://github.com/google-gemini/gemini-cli/pull/23159)** (Refactor)
    *   Introduces `AgentSession` wrapper and renames stream events to `agent_start`/`agent_end` for better subscription handling.
*   **[#20974 Compact Tool Output](https://github.com/google-gemini/gemini-cli/pull/20974)** (Feat)
    *   Aims to reduce "noise" in the terminal by collapsing verbose tool outputs, bridging the gap between user prompts and system responses.
*   **[#22856 /context Command](https://github.com/google-gemini/gemini-cli/pull/22856)** (Feat)
    *   Adds a `/context` slash command to visualize the breakdown of the model's context window (system prompt, tools, memory, etc.).

### 5. Feature Request Trends
*   **Enhanced `/plan` Command**: Users want the `/plan` command to accept arguments directly (e.g., `/plan implement auth`) rather than entering a separate interactive mode.
*   **Multimodal Inputs**: There is a persistent demand for image pasting support in the CLI, moving beyond text-only interaction.
*   **Codebase Understanding**: Significant interest in "AST-aware" features to make the agent smarter about reading code structure (methods, classes) rather than raw lines.

### 6. Developer Pain Points
*   **Startup Noise**: Repeated warnings about extension configurations (specifically the migration from `conductor` to `sdd`) are causing annoyance.
*   **Agent Loops**: Developers are reporting situations where the agent enters a "token burning" loop, failing to select tools or resolve file paths effectively, leading to wasted API credits.
*   **Incomplete Code Generation**: The "omission placeholder detector" is failing for languages other than JavaScript (e.g., Python, Go), resulting in commented-out code (`# rest of code...`) being written to files as valid code.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-03-20

## 1. Today's Highlights
GitHub Copilot CLI **v1.0.9** was released on March 19, focusing on stability and internationalization support. This patch addresses critical user-reported regressions, specifically fixing spurious I/O error messages during SSH disconnects and restoring correct text copying for CJK characters in WSL environments. Community sentiment remains focused on usability, with significant discussion surrounding terminal input handling (Vi mode) and text selection capabilities in the TUI.

## 2. Releases
**v1.0.9** (2026-03-19)
This release targets quality-of-life improvements and system stability.
*   **Stability:** Resolved an issue where spurious `ENOTCONN` and `EIO` error messages would clutter the timeline during SSH disconnects or terminal closures.
*   **Configuration:** Added a new `include_gitignored` config option, allowing users to include gitignored files in `@` file search operations.
*   **Internationalization:** Fixed a bug where copying text on Windows Subsystem for Linux (WSL) incorrectly mangled CJK (Chinese, Japanese, Korean) and other non-ASCII characters.
*   [View Release Details](https://github.com/github/copilot-cli/releases)

## 3. Hot Issues
Below are the top issues from the community, highlighting both critical bugs and popular feature requests.

*   **[#239 Screen flickering / starts scrolling down from the beginning](https://github.com/github/copilot-cli/issues/239)** *(Open)*
    **Why it matters:** This is the most upvoted issue currently active. Users report severe UI degradation (flickering, uncontrolled scrolling) as conversation history grows.
    **Reaction:** 66 thumbs up; users are stating the tool becomes unusable during long sessions.

*   **[#33 Support OAuth http MCP servers](https://github.com/github/copilot-cli/issues/33)** *(Closed)*
    **Why it matters:** Integration with enterprise tools like Figma and Atlassian often requires OAuth. This enhancement request sought to bridge that gap.
    **Reaction:** 106 thumbs up; now closed, suggesting support may have landed or is being handled differently.

*   **[#1284 Arrow keys stopped working in CLI](https://github.com/github/copilot-cli/issues/1284)** *(Open)*
    **Why it matters:** A critical regression where arrow keys output literal characters (`A`, `B`, `C`, `D`) instead of navigating the cursor.
    **Reaction:** High urgency; users cannot navigate input effectively.

*   **[#13 CLI input should have a vi/vim input mode](https://github.com/github/copilot-cli/issues/13)** *(Open)*
    **Why it matters:** A long-standing request for developers accustomed to modal editors.
    **Reaction:** 37 thumbs up; highly requested feature for power users.

*   **[#1157 Feature Request: Global Hooks Configuration](https://github.com/github/copilot-cli/issues/1157)** *(Open)*
    **Why it matters:** Developers want to define hooks globally rather than per-repository to avoid repetitive configuration files.
    **Reaction:** 18 thumbs up; users comparing Copilot unfavorably to Cursor/Claude Code in this regard.

*   **[#1347 XDG_CONFIG_HOME is not supported correctly](https://github.com/github/copilot-cli/issues/1347)** *(Open)*
    **Why it matters:** The CLI violates Linux standards by storing config in `~/.config/.copilot` (nested dot folder) instead of `~/.config/copilot`.
    **Reaction:** 9 thumbs up; Linux users are asking for strict adherence to the XDG Base Directory Specification.

*   **[#1940 Start from Copilot CLI v1.0.3 produces garbled text when copying Chinese output](https://github.com/github/copilot-cli/issues/1940)** *(Closed)*
    **Why it matters:** Directly related to the fix in today's **v1.0.9** release.
    **Reaction:** Users confirmed the WSL copy-paste bug is resolved by the latest update.

*   **[#2159 Copy and paste is broken (Windows Putty SSH to Linux Mint)](https://github.com/github/copilot-cli/issues/2159)** *(Closed)*
    **Why it matters:** Highlights the friction caused by new TUI handling of mouse/clipboard events.
    **Reaction:** Users expressed frustration that standard terminal workflows (select-to-copy) were overridden.

*   **[#2143 Text selection and copy (Ctrl+C) only captures the first character](https://github.com/github/copilot-cli/issues/2143)** *(Open)*
    **Why it matters:** A severe regression preventing users from copying code snippets generated by the agent.
    **Reaction:** Critical workflow blocker for developers relying on the CLI to generate boilerplate.

*   **[#2162 Feature: Support keyboard scrolling to review full session history in TUI](https://github.com/github/copilot-cli/issues/2162)** *(Open)*
    **Why it matters:** The TUI currently locks scrolling, making it impossible to review long outputs.
    **Reaction:** Users want native keyboard support (Page Up/Down) to inspect agent responses.

## 4. Key PR Progress
*No Pull Requests were updated in the last 24 hours.*

## 5. Feature Request Trends
Based on the latest issue activity, the community is strongly advocating for:
1.  **Terminal Input Flexibility:** There is a surge in requests for **Vi/Vim mode support** (#13) and fixes for broken standard inputs (Arrow keys #1284).
2.  **Better Navigation History:** Users are demanding the ability to scroll up within the TUI to view previous outputs (#2162, #2148).
3.  **Configuration Standardization:** A strong push for **Global Hooks** (#1157) and correct **XDG Config Home** support (#1347, #1750) on Linux.
4.  **OAuth & MCP Integration:** Continued interest in seamless OAuth support for MCP servers (#33, #1491).

## 6. Developer Pain Points
*   **Clipboard Hostility:** Recent changes to how the CLI handles text selection have caused widespread frustration. Users report that mouse selection and standard shortcuts (Ctrl+Shift+C) are broken or inconsistent across Windows, Linux, and SSH sessions (#2143, #2158, #2082).
*   **TUI Instability:** Long sessions are prone to UI bugs, including screen flickering (#239), "freezing" thinking indicators (#1320), and apps that launch but do nothing (#2160).
*   **Shell Escape Handling:** There is recurring confusion regarding keybinds. Users expect standard shell behavior (e.g., `Shift+Enter` for new lines), but the CLI sometimes defaults these to execution (#1481).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest: 2026-03-20

## 1. Today's Highlights
The Kimi CLI repository is seeing a significant surge in maintenance activity with over 20 Pull Requests opened or updated in the last 24 hours. Core contributors are aggressively addressing a "Connection error" cascade affecting Linux and Windows users, while simultaneously implementing quality-of-life features such as auto-submitting slash commands and dynamic terminal window titles. A major focus is being placed on fixing platform-specific regressions, particularly regarding the Kitty keyboard protocol in VS Code and file locking issues on Windows.

## 2. Releases
**No new releases** in the last 24 hours.

## 3. Hot Issues
1.  **[#1285 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1285)**: *LLM provider error: Connection error.*
    This highly active thread (9 comments) reports persistent connection failures on v1.15.0, likely related to the HTTP header pollution issues being fixed in recent PRs.
2.  **[#1380 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1380)**: *ACP terminal tool fails with 'module acp has no attribute TerminalHandle'.*
    A critical regression in v1.17 & v1.18 where changes in the Agent Client Protocol (ACP) SDK broke the terminal adapter. A fix is already in PR (#1524).
3.  **[#1437 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1437)**: *Enter key appends `[13u` instead of sending message in VS Code terminal.*
    High-friction UX bug where the Enter key prints raw escape codes in VS Code integrated terminals due to the Kitty keyboard protocol.
4.  **[#1429 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1429)**: *Windows platform concurrent write causes Permission denied.*
    Windows users are experiencing session corruption due to the lack of file locking when concurrent writes occur to `context.jsonl`.
5.  **[#1487 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1487)**: *HTTPS MCP Connection Failures.*
    MCP (Model Context Protocol) connections over HTTP are failing because CDNs block requests without a `User-Agent` header.
6.  **[#751 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/751)**: *Slash commands execute immediately upon selection.*
    A popular UX request to remove the double-Enter requirement for executing slash commands from the completion menu.
7.  **[#1513 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1513)**: *Windows installer crashes silently under default PowerShell policy.*
    New users on Windows cannot install the tool on fresh machines due to execution policy restrictions in the setup script.
8.  **[#1378 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1378)**: *JSON parsing error with control characters.*
    Tool calls fail when the LLM returns control characters (like newlines) inside JSON strings, breaking session restoration.
9.  **[#1475 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1475)**: *Display current directory in prompt/window title.*
    Users reported a regression where the static title "Kimi Code" makes managing multiple terminal sessions difficult.
10. **[#1428 (OPEN)](https://github.com/MoonshotAI/kimi-cli/issues/1428)**: *Web UI attachment button triggers form submit.*
    In the Web UI (v1.21.0), clicking toolbar buttons incorrectly submits the form rather than triggering the intended action (like attaching a file).

## 4. Key PR Progress
1.  **[#1524](https://github.com/MoonshotAI/kimi-cli/pull/1524)**: *fix: replace removed acp.TerminalHandle with local adapter.*
    Directly addresses Issue #1380 by migrating to the new ACP SDK standard, restoring terminal functionality for IDE users.
2.  **[#1520](https://github.com/MoonshotAI/kimi-cli/pull/1520)**: *fix: add asyncio.Lock to prevent concurrent file write conflicts.*
    Implements file locking to resolve the `PermissionError` crashes on Windows (Issue #1429).
3.  **[#1522](https://github.com/MoonshotAI/kimi-cli/pull/1522)**: *fix: inject default User-Agent header for MCP HTTP/SSE connections.*
    Fixes the MCP connection errors (Issue #1487) by ensuring HTTP requests identify themselves to CDNs.
4.  **[#1514](https://github.com/MoonshotAI/kimi-cli/pull/1514)**: *fix: disable Kitty keyboard protocol to fix Enter key in VS Code terminal.*
    Resolves the `[13u` text bug (Issue #1437) by disabling the problematic keyboard protocol in incompatible terminals.
5.  **[#1509](https://github.com/MoonshotAI/kimi-cli/pull/1509)**: *feat: auto-submit slash commands upon selection.*
    Implements the enhancement requested in #751, streamlining the workflow for command execution.
6.  **[#1519](https://github.com/MoonshotAI/kimi-cli/pull/1519)**: *feat: display current directory in terminal title.*
    Addresses Issue #1475 by dynamically updating the window title to show the CWD, aiding navigation in multi-tab workflows.
7.  **[#1523](https://github.com/MoonshotAI/kimi-cli/pull/1523)**: *feat: adapt tool argument display width to terminal size.*
    Fixes the overly aggressive truncation of command strings (Issue #1492), allowing full command visibility on wide screens.
8.  **[#1521](https://github.com/MoonshotAI/kimi-cli/pull/1521)**: *fix(web): prevent toolbar buttons from triggering form submit.*
    A hotfix for the Web UI (Issue #1428), ensuring buttons like "Attach" perform their intended action rather than submitting the chat prompt.
9.  **[#1515](https://github.com/MoonshotAI/kimi-cli/pull/1515)**: *fix(web): enable inline math formula rendering.*
    Corrects the Web UI markdown parser to support `$...$` for inline math, previously failing in v1.20.0.
10. **[#1516](https://github.com/MoonshotAI/kimi-cli/pull/1516)**: *fix: handle PowerShell Restricted execution policy in install script.*
    Updates the Windows installer (Issue #1513) to gracefully handle default security settings without silent crashes.

## 5. Feature Request Trends
*   **Workflow Efficiency**: Users are demanding fewer keystrokes. The popularity of the "Auto-submit slash commands" (#751) and "Skip option in execution prompts" (#729) indicates a desire for faster, non-blocking interactions.
*   **IDE/Terminal Parity**: There is a strong push for consistency between the CLI, Web UI, and IDE integrations. Requests range from "Number key selection" (#1252) to matching UI features like toolbars.
*   **Plugin/Extensibility**: Interest is growing in more customizable agents, as seen in the revival of the "Skills.md" discussion (#107).

## 6. Developer Pain Points
*   **Platform Fragility**: A significant portion of the recent issues (Connection errors, Permission denied, Install crashes) stems from environmental differences—specifically Windows file locking, Linux kernel version strings, and PowerShell policies.
*   **Input Handling Regressions**: The recent VS Code Enter key bug (#1437) and Windows Terminal paste issues (#781) highlight ongoing struggles with handling diverse terminal capabilities and keyboard protocols.
*   **Session State Management**: Corrupted sessions due to JSON parsing errors (#1378) or concurrent writes (#1429) are causing data loss and frustration for users relying on session persistence.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: 2026-03-20

## 1. Today's Highlights
The community is currently managing a significant disruption regarding **Anthropic OAuth authentication**. A surge of issues (including #18267 and #18315) reports widespread login failures, token refresh errors (HTTP 429), and the disappearance of the `opencode-anthropic-auth` repository, leaving many Claude users locked out of the tool. Simultaneously, the core development team is accelerating the migration to **OpenCode 2.0**, focusing on removing Bun-specific dependencies in favor of portable Effect-based services and Node.js compatibility.

## 2. Releases
**No new releases were published in the last 24 hours.**

## 3. Hot Issues

1.  **[#18267 [OPEN] Claude code 0auth broked](https://github.com/anomalyco/opencode/issues/18267)**
    *   **Impact:** Critical. Users are experiencing "Error 429" and complete inability to login via OAuth.
    *   **Reaction:** The most active thread in 24h (96 comments). Users are reporting that their workflows are completely halted.

2.  **[#18315 [OPEN] Claude Pro/Max auth flow returns Invalid token](https://github.com/anomalyco/opencode/issues/18315)**
    *   **Impact:** High. Follow-up to the general OAuth issues; specifically affects users trying to re-authenticate after being logged out.
    *   **Reaction:** Confirms that re-installation and cache clearing do not fix the "Invalid Token" error.

3.  **[#18265 [OPEN] Repository anomalyco/opencode-anthropic-auth no longer exists](https://github.com/anomalyco/opencode/issues/18265)**
    *   **Impact:** High. Raises concerns about the deprecation of the official Anthropic provider integration.
    *   **Reaction:** Users are asking if this signals the end of Anthropic support within OpenCode.

4.  **[#10416 [OPEN] OpenCode is not private by default?](https://github.com/anomalyco/opencode/issues/10416)**
    *   **Impact:** High Security/Privacy concern. Users discovered that session titles (metadata) are computed remotely even when using local LLMs.
    *   **Reaction:** Significant community concern regarding data leakage and "offline" guarantees.

5.  **[#7957 [OPEN] Ctrl+C should not exit OpenCode](https://github.com/anomalyco/opencode/issues/7957)**
    *   **Impact:** UX Friction. The universal "Copy" shortcut kills the application.
    *   **Reaction:** High engagement (👍 17). Windows users are particularly frustrated by the muscle memory conflict.

6.  **[#18242 [OPEN] "Extra usage is required..." error loop](https://github.com/anomalyco/opencode/issues/18242)**
    *   **Impact:** Functional. Anthropic removed long-context premiums on March 13, but OpenCode still enforces the restriction, causing infinite retry loops.
    *   **Reaction:** Users are blocked from long coding sessions despite having valid API permissions.

7.  **[#13546 [OPEN] GPT-5 series "reasoningSummary" parameter errors](https://github.com/anomalyco/opencode/issues/13546)**
    *   **Impact:** Compatibility. Breaks custom OpenAI-compatible providers when using GPT-5/Codex models.
    *   **Reaction:** Highlights difficulties in using OpenCode with non-OpenAI hosted infrastructure.

8.  **[#5636 [OPEN] HTTP 405 on Figma MCP](https://github.com/anomalyco/opencode/issues/5636)**
    *   **Impact:** Integration. The official Figma MCP server fails to connect.
    *   **Reaction:** Users investigating if the issue is on OpenCode's end or Figma's API change.

9.  ** [#11301 [OPEN] Processing stops after compaction EVERY time](https://github.com/anomalyco/opencode/issues/11301)**
    *   **Impact:** Workflow. Automatic context compaction causes the agent to halt, requiring manual intervention to continue.
    *   **Reaction:** Recurring frustration with long-running tasks.

10. **[#18190 [OPEN] Invalid params when passing --prompt](https://github.com/anomalyco/opencode/issues/18190)**
    *   **Impact:** Regression. CLI automation is broken for users starting sessions with arguments.
    *   **Reaction:** Affects CI/CD pipelines and scripting workflows.

## 4. Key PR Progress

1.  **[#16918 [OPEN] opencode 2-0](https://github.com/anomalyco/opencode/pull/16918)**
    *   **Focus:** The massive overhaul PR. Recent updates include abstracting the database layer to support both Bun and Node.js runtimes via `@opencode/db`.
    *   **Significance:** Foundation for the next major version.

2.  **[#18318 [CLOSED] refactor: replace Bun shell execution](https://github.com/anomalyco/opencode/pull/18318)**
    *   **Focus:** Removes `Bun.spawn` and `Bun.$` in favor of a portable `Process` utility.
    *   **Significance:** Critical step towards Node.js compatibility.

3.  **[#18319 [OPEN] effectify Pty service](https://github.com/anomalyco/opencode/pull/18319)**
    *   **Focus:** Migrating the Pseudo-Terminal (PTY) service to the Effect pattern.
    *   **Significance:** Improves resource management and cancellation handling for background processes.

4.  **[#18271 [OPEN] effectify Command service](https://github.com/anomalyco/opencode/pull/18271)**
    *   **Focus:** Refactoring the Command execution service to use Effect services.
    *   **Significance:** Standardizes error handling and command lifecycle management.

5.  **[#18173 [OPEN] migrate Bus to Effect service](https://github.com/anomalyco/opencode/pull/18173)**
    *   **Focus:** Central event bus refactor. Notably makes `publish` fire-and-forget.
    *   **Significance:** Performance improvement for event-heavy workflows.

6.  **[#18317 [OPEN] feat: quiet mode for CLI runs](https://github.com/anomalyco/opencode/pull/18317)**
    *   **Focus:** Adds `-q | --quiet` flag to suppress output.
    *   **Significance:** Highly requested for scripting and CI/CD usage.

7.  **[#18308 [OPEN] refactor: replace BunProc with Npm module](https://github.com/anomalyco/opencode/pull/18308)**
    *   **Focus:** Removes internal `BunProc` in favor of `@npmcli/arborist`.
    *   **Significance:** Resolves issues with package management determinism and Bun-specific behaviors.

8.  **[#18300 [OPEN] align workspace routing](https://github.com/anomalyco/opencode/pull/18300)**
    *   **Focus:** Fixes web/desktop routing inconsistencies between workspace slugs and directories.
    *   **Significance:** Improves stability of the GUI session management.

9.  **[#18297 [CLOSED] feat: add hard stop on max steps](https://github.com/anomalyco/opencode/pull/18297)**
    *   **Focus:** Adds an option to halt execution immediately when max steps are reached, rather than wrapping up.
    *   **Significance:** Gives developers finer control over agent runtime costs.

10. **[#18298 [CLOSED] feat: add provider racing](https://github.com/anomalyco/opencode/pull/18298)**
    *   **Focus:** Implements racing logic for multiple providers; returns the fastest response.
    *   **Significance:** A clever way to minimize latency when using unreliable routers like OpenRouter.

## 5. Feature Request Trends
*   **Multi-Account / Credential Rotation:** There is a strong push for supporting multiple OAuth accounts simultaneously (#11830, #8145) to handle rate limits and downtime more gracefully.
*   **Multi-Agent Orchestration:** Users are looking for built-in ways to run teams of specialized agents in isolated workspaces (#17994).
*   **Privacy-First Defaults:** Following the metadata outcry, users are demanding "Air-gapped" modes where no external API calls are made for telemetry or titling (#10416).

## 6. Developer Pain Points
*   **Authentication Fragility:** The current OAuth implementation is perceived as brittle; updates to the `opencode-anthropic-auth` package frequently break workflows, leaving users with no fallback (API keys are often rejected or difficult to use in conjunction).
*   **Context Management:** "Compaction" is frequently cited as a point of failure. Users report that the agent effectively "dies" or hallucinates after context compaction occurs (#11301, #3743).
*   **Platform Inconsistency:** Windows users continue to face specific bugs, such as the `Ctrl+C` conflict and file creation issues (creating a file named `nul`), indicating a need for better cross-platform testing.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest: 2026-03-20

## 1. Today's Highlights
The release of **v0.13.0-preview** marks a significant milestone, introducing a new **permissions system** and **image paste support** for the VSCode companion, alongside a fix for the critical **duplicate finish_reason** bug affecting OpenRouter users. Community sentiment is currently polarized: while the introduction of granular permission controls is praised, there is significant frustration regarding **data loss bugs** related to the `edit` tool and file overwrites, which users report are making the tool "almost unusable" in the latest versions.

## 2. Releases
* **v0.13.0-preview.0** & **v0.13.0-nightly** ([Link](https://github.com/QwenLM/qwen-code/releases))
    *   **Feature:** Added system prompt customization options.
    *   **Fix:** Resolved an issue with OpenRouter where `finish_reason` chunks were duplicated, causing stream processing errors.
    *   **Maintenance:** Version bump to 0.13.0.

## 3. Hot Issues
*   [#2460: "Edit failed" is frequent and destroys code](https://github.com/QwenLM/qwen-code/issues/2460)
    *   **Why it matters:** A user reported that the `edit` tool is failing frequently and corrupting files by attempting to use Node/PS to edit content, calling it "unusable" in v0.12.6.
    *   **Reaction:** 7 comments; reflects the highest pain point currently.
*   [#1922: Edit tool unable to edit files in latest version](https://github.com/QwenLM/qwen-code/issues/1922)
    *   **Why it matters:** Regression of a previously fixed bug where Python file edits fail completely.
    *   **Reaction:** 10 comments; indicates a stability regression in core editing capabilities.
*   [#2454: /model command silently removes manually-added models](https://github.com/QwenLM/qwen-code/issues/2454)
    *   **Why it matters:** Critical UX bug where manual edits to `settings.json` are wiped when using the `/model` slash command.
    *   **Reaction:** 2 comments; high impact for users managing custom model providers.
*   [#2499: Agent overwrites files without reading (Data Loss)](https://github.com/QwenLM/qwen-code/issues/2499)
    *   **Why it matters:** The agent uses `write_file` to overwrite entire files instead of making surgical edits, leading to data loss.
    *   **Reaction:** 2 comments; major safety concern for production workflows.
*   [#2155: Support `.agents/skills` directory](https://github.com/QwenLM/qwen-code/issues/2155)
    *   **Why it matters:** Users want to align with the emerging standard of `.agents` (plural) instead of `.agent` (singular).
    *   **Reaction:** 3 comments; PR #2476 is currently open to address this.
*   [#2496: Cannot read files with mixed Chinese/English names](https://github.com/QwenLM/qwen-code/issues/2496)
    *   **Why it matters:** Parser incorrectly interprets mixed characters (e.g., `测试and测试.md`) as having spaces.
    *   **Reaction:** 2 comments; highlights i18n parsing issues.
*   [#2086: Support for `.agents` directory skills](https://github.com/QwenLM/qwen-code/issues/2086)
    *   **Why it matters:** Request to support skills stored in `.agents` folder, similar to Claude Code.
    *   **Reaction:** 6 comments; High demand for interoperability/standardization.
*   [#2491: Cannot input single Chinese characters (Ubuntu)](https://github.com/QwenLM/qwen-code/issues/2491)
    *   **Why it matters:** Input bug prevents single Chinese character input via Sougou IM on Ubuntu.
    *   **Reaction:** 1 comment; specific but blocking for localized users.
*   [#2497: Request to disable persistent "Always Allow" approvals](https://github.com/QwenLM/qwen-code/issues/2497)
    *   **Why it matters:** Users want an option to force per-action confirmation instead of persistent permissions for safety.
    *   **Reaction:** 2 comments; security vs. convenience trade-off.
*   [#2505: Read image causes crash](https://github.com/QwenLM/qwen-code/issues/2505)
    *   **Why it matters:** Attempting to read an image file throws a 400 error regarding model restrictions, crashing the session.
    *   **Reaction:** 1 comment; highlights instability in new multimodal features.

## 4. Key PR Progress
*   [#2482: Fix `/model` command removing custom models](https://github.com/QwenLM/qwen-code/pull/2482)
    *   **Status:** Closed.
    *   **Detail:** Fixes the `setValue()` logic to preserve manually added models in `settings.json` when switching models.
*   [#2475: Handle escaped pipe chars in tables](https://github.com/QwenLM/qwen-code/pull/2475)
    *   **Status:** Closed.
    *   **Detail:** Fixes markdown table rendering so literal `|` characters (e.g., type `A|B`) don't break the table layout.
*   [#2283: Feat: support permission](https://github.com/QwenLM/qwen-code/pull/2283)
    *   **Status:** Closed (Merged for 0.13.0).
    *   **Detail:** Introduces a fine-grained rule-based permission system (e.g., `Bash(git *)`, `Read(./secrets/**)`).
*   [#2476: Add `.agents/skills` as provider dir](https://github.com/QwenLM/qwen-code/pull/2476)
    *   **Status:** Open.
    *   **Detail:** Adds support for the `.agents` (plural) convention for skill storage.
*   [#1978: Add image paste support (VSCode)](https://github.com/QwenLM/qwen-code/pull/1978)
    *   **Status:** Open (Target: 0.13.0).
    *   **Detail:** Enables pasting images directly into the VSCode companion interface.
*   [#2371: Add `/btw` slash command](https://github.com/QwenLM/qwen-code/pull/2371)
    *   **Status:** Open (Target: 0.13.0).
    *   **Detail:** Adds a command for ephemeral side questions that don't affect main conversation history.
*   [#2504: Prevent /model overwriting external settings](https://github.com/QwenLM/qwen-code/pull/2504)
    *   **Status:** Open.
    *   **Detail:** A more robust fix to ensure `settings.json` isn't clobbered by the `/model` command.
*   [#2420: Allow Ctrl+Y to skip rate-limit delay](https://github.com/QwenLM/qwen-code/pull/2420)
    *   **Status:** Open.
    *   **Detail:** Adds a hotkey to bypass the 60s rate-limit retry countdown.
*   [#2474: Normalize CRLF in edit tool](https://github.com/QwenLM/qwen-code/pull/2474)
    *   **Status:** Closed.
    *   **Detail:** Fixes the `edit` tool failing when `old_string` has CRLF line endings but the file is LF.
*   [#2502: Support `extends: bundled` in skills](https://github.com/QwenLM/qwen-code/pull/2502)
    *   **Status:** Open.
    *   **Detail:** Allows users to extend bundled skills (like `/review`) rather than replacing them entirely.

## 5. Feature Request Trends
*   **Standardization of "Skills" & "Agents":** There is a strong push to support the `.agents` directory (plural) to align with other coding assistants like Claude Code and the broader `agentskills` ecosystem.
*   **Granular Permission Controls:** Users are eager to adopt the new permission system (PR #2283) to define exactly what tools and paths the agent can access, enhancing safety in sensitive repositories.
*   **UI/UX Customization:** Requests for better control over interface elements, specifically customizing/disabling "Thinking" quotes and adding options to disable persistent "Always Allow" approvals.
*   **Multimodal Inputs:** Continued interest in robust image handling, specifically paste support in IDEs and better validation of image dimensions/constraints.

## 6. Developer Pain Points
*   **File Editing Instability:** The community is reporting critical failures in the `edit` tool (Issues #1922, #2460, #2499). Users cite regex failures, CRLF mismatch issues, and aggressive file overwrites that lead to code corruption.
*   **Configuration Management:** There is frustration with `settings.json` being fragile. Manual edits are being silently deleted by slash commands like `/model`, and there are reports of the CLI crashing (Issue #2386) or becoming unresponsive on startup (Windows 11).
*   **Localization Bugs:** Non-English users are facing specific hurdles, including the inability to input single Chinese characters on Linux and file reading failures with mixed CJK/English filenames.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*