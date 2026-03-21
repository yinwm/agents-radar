# AI CLI Tools Community Digest 2026-03-21

> Generated: 2026-03-21 01:14 UTC | Tools covered: 7

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

# AI CLI Tools Ecosystem Report: 2026-03-21

## 1. Ecosystem Overview
The AI CLI landscape is currently defined by a bifurcation between **automation readiness** and **user experience stability**. As of March 2026, leading tools are aggressively optimizing for headless CI/CD workflows (evidenced by Claude Code's `--bare` flag and OpenCode's server fixes), yet they simultaneously struggle with platform-specific regressions, particularly on Windows. A significant industry-wide focus has emerged on **Agent Safety**—specifically preventing data loss from "hallucinated" file overwrites—while **Model Context Protocol (MCP)** integration has become the standard for extensibility across all major players.

## 2. Activity Comparison

| Tool | Version Status | Issues (Last 24h) | PRs (Last 24h) | Release Velocity | Primary Focus |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | v2.1.81 | 10 Hot Issues | 10 Merged | **High** (Stable) | Automation (`--bare`), Permissions, MCP |
| **OpenAI Codex** | v0.117.0-alpha | 7 Hot Issues | 8 Merged | **Med** (Alpha) | Sandbox Stability, V8 Refactoring |
| **Gemini CLI** | No Release | 10 Hot Issues | 11 Merged | **High** (Active Dev) | Task Tracking (SDD), AST Integration |
| **GitHub Copilot** | v1.0.10 | 10 Hot Issues | 0 Merged | **Low** (Patch) | Clipboard/Clipboard Fixes, Plan Mode |
| **Kimi Code** | v1.16-v1.24 | 11 New Issues | 20 Closed | **High** (Sprint) | Windows Compatibility, MCP Resilience |
| **OpenCode** | No Release | 10 Hot Issues | 10 Active | **Med** (Maint) | OAuth/Memory Leaks, AI SDK v6 |
| **Qwen Code** | v0.13.0-preview | 9 Hot Issues | 8 Active | **High** (Iterating) | File Safety (Read-Before-Write), Parity |

## 3. Shared Feature Directions
*   **Headless & CI/CD Support:** There is a unanimous push to reduce interactive friction.
    *   *Claude Code* introduced `--bare` mode.
    *   *OpenCode* users are demanding server-side stability.
    *   *Kimi Code* is adding timeout extensions and pseudo-cwd for scripting.
*   **Agent Safety & File Integrity:** Following a wave of "destructive agent" reports, multiple communities are implementing strict guardrails.
    *   *Qwen Code* is enforcing "Read-Before-Write" logic to prevent truncation.
    *   *Claude Code* merged "destructive-command-guard" plugins.
    *   *GitHub Copilot* users are demanding stricter "Plan Mode" adherence to prevent premature execution.
*   **MCP (Model Context Protocol) Resilience:** While MCP is the standard, its implementation is currently fragile across the board.
    *   *Kimi Code* and *GitHub Copilot* users are reporting that single-server failures crash the entire session (Issue #769, #2178).
    *   *OpenCode* and *Gemini CLI* are actively working on connection pooling and isolation.

## 4. Differentiation Analysis

| Feature Focus | Tools | Notes |
| :--- | :--- | :--- |
| **Platform Fragility** | **Windows** is the primary pain point for *Kimi Code* (encoding), *OpenAI Codex* (sandbox), and *Claude Code* (filesystem). | *Gemini CLI* appears to be avoiding some deep-shell issues by focusing on "Agent" capabilities and SDD. |
| **Memory Management** | *OpenCode* is battling critical memory leaks (60GB+ OOM). | *Gemini CLI* successfully patched a ~1.7GB V8 leak. |
| **Extensibility** | *Claude Code* leads with **Plugins & Hooks** (PreToolUse, agent-wallet). | *GitHub Copilot* is playing catch-up with SDK hooks. |
| **Technical Approach** | *OpenAI Codex* is rewriting core logic in Rust/V8 ("Code mode on v8"). | *Qwen Code* focuses on Agentic UI (Plan mode, Insight) and cross-client parity. |
| **Architecture** | *Gemini CLI* is moving from Markdown plans to **Native DAGs (SDD)**. | Others rely on LLM-generated text plans. |

## 5. Community Momentum & Maturity
*   **High Velocity:** **Claude Code** and **Qwen Code** show the highest momentum. Claude Code is rapidly releasing stable versions with advanced automation features. Qwen Code is iterating aggressively on "Safety" and "Parity" (CLI to VSCode).
*   **Stability Concerns:** **OpenAI Codex** and **OpenCode** are currently facing "Regression Anxiety." Codex's sandbox issues (Bubblewrap) and OpenCode's OAuth failures are blocking core workflows for enterprise users.
*   **Maturation:** **GitHub Copilot CLI** is the most stable but least innovative; the lack of PR updates suggests a maintenance mode, focusing purely on integrating with the broader VS Code ecosystem rather than CLI-first innovation.

## 6. Trend Signals for Developers
1.  **Expect "Hallucination" Guarantees:** The era of trusting LLMs to write files directly is ending. Successful tools are implementing "Read-Before-Write" or "Diff-Only" workflows by default. **Signal:** Prioritize tools with granular pre-commit hooks.
2.  **The "Headless" Imperative:** Interactive chat is becoming a secondary use case to scripted automation (`-p`, `--bare`). Tools that cannot run reliably in CI/CD pipelines without TUI overhead are being re-architected.
3.  **MCP is the New JSON:** Integration complexity has shifted from API keys to configuring MCP servers. However, robust error handling for MCP connection failures is currently missing in most tools.
4.  **Windows is the Canary:** If an AI CLI tool supports Windows (file systems, terminals, encodings) correctly, it usually implies a high-quality, robust codebase. Currently, most are failing this test.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Analysis Period:** Data as of March 21, 2026

## 1. Top Skills Ranking
*Based on community engagement via Pull Requests*

*   **[document-typography](https://github.com/anthropics/skills/pull/514)** (PGTBoos)
    Addresses a universal pain point in AI generation: preventing typographic errors like "widows" and "orphans" in documents. The discussion highlights that while code generation is strong, visual formatting artifacts remain a common issue in all generated documentation.
*   **[skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** (eovidiu)
    Meta-tools for the ecosystem. These skills propose a 5-dimensional quality framework (Structure, Documentation, etc.) and security vetting for other community skills, reflecting the ecosystem's maturation beyond simple scripts into formal engineering.
*   **[frontend-design (Improvement)](https://github.com/anthropics/skills/pull/210)** (justinwetch)
    A significant refactor to make the frontend-design skill more "actionable" and less theoretical. The author focuses on ensuring every instruction is executable by Claude within a single context window, signaling a trend toward "token-efficient" prompting.
*   **[SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181)** (amitlals)
    Bridges the gap between Claude Code and enterprise SAP data using the open-source SAP-RPT-1-OSS foundation model. This represents a high-value entry for technical users in legacy enterprise environments.
*   **[codebase-inventory-audit](https://github.com/anthropics/skills/pull/147)** (p19dixon)
    A "cleanup" utility for identifying orphaned code and documentation debt. It generates a standardized `CODEBASE-STATUS.md`, suggesting a community desire for better maintenance of large, existing projects rather than just greenfield development.
*   **[session-memory](https://github.com/anthropics/skills/pull/629)** (Lordanakun)
    Tackles the "context compaction" problem by preserving technical facts across session restarts without external dependencies. This is critical for long-running workflows where context limits are hit frequently.

## 2. Community Demand Trends
*Derived from top Issues and proposals*

*   **Ecosystem Integrity & Security:**
    *   **Trust Boundaries:** [Issue #492](https://github.com/anthropics/skills/issues/492) highlights a critical vulnerability where community skills can impersonate official Anthropic ones (`anthropic/` namespace), creating security risks.
    *   **Quality Control:** Users are demanding standardization. The call for `CONTRIBUTING.md` (via [PR #509](https://github.com/anthropics/skills/pull/509)) and better documentation (Issue #202) indicates the "Wild West" phase is ending and governance is needed.

*   **Reliability & Compatibility:**
    *   **UTF-8 & Encoding:** A surprising amount of attention ([PR #362](https://github.com/anthropics/skills/pull/362), [PR #284](https://github.com/anthropics/skills/pull/284)) is focused on fixing character encoding bugs (non-Latin characters causing panics), suggesting rapid globalization of the user base.
    *   **Platform Integration:** Users are actively asking for better integration with AWS Bedrock ([Issue #29](https://github.com/anthropics/skills/issues/29)) and MCP protocols ([Issue #16](https://github.com/anthropics/skills/issues/16)).

*   **Meta-Skills & Tooling:**
    *   There is a strong push for "skills about skills" ([Issue #83](https://github.com/anthropics/skills/pull/83)), such as analyzers that audit other skills for quality and security, or agent governance patterns ([Issue #412](https://github.com/anthropics/skills/issues/412)).

## 3. High-Potential Pending Skills
*Active PRs likely to impact the ecosystem soon*

*   **[ODT (OpenDocument Text) Skill](https://github.com/anthropics/skills/pull/486)** (GitHubNewbie0)
    Adds support for LibreOffice/OpenOffice formats (`.odt`), filling a gap for users in open-source ecosystems who cannot rely on proprietary DOCX formats.
*   **[shodh-memory](https://github.com/anthropics/skills/pull/154)** (varun29ankuS)
    Introduces a "persistent memory" system using a `proactive_context` tool to surface relevant memories from past conversations. This moves toward a stateful AI agent model.
*   **[management-consulting](https://github.com/anthropics/skills/pull/384)** (anotb)
    Brings structured business frameworks (market entry, competitive positioning) to Claude Code, expanding its utility from pure coding to high-level strategic business analysis.
*   **[x402 BSV Auth + Micropayment](https://github.com/anthropics/skills/pull/374)** (Calgooon)
    A novel skill enabling natural-language-triggered micropayments for AI services. If merged, this introduces a monetization layer to agent interactions.

## 4. Skills Ecosystem Insight
The community is moving beyond basic coding utilities to demand **robustness, interoperability, and "pro-level" features** (like persistent memory, enterprise integrations, and typography control); the highest concentration of demand is currently for **Meta-Skills**—tools that validate, secure, and manage the growing repository of capabilities itself.

---

# Claude Code Community Digest — 2026-03-21

## Today's Highlights
Version **2.1.81** has been released, introducing a `--bare` flag designed for high-performance scripted automation by stripping out hooks, LSP, and plugin overhead. Simultaneously, the community is actively troubleshooting cross-platform regressions, specifically persistent bugs on Windows involving external directory access and a critical issue where session settings are inadvertently shared globally across active instances.

## Releases
**v2.1.81**
This release targets CI/CD and advanced automation workflows. The new `--bare` flag allows Claude Code to run with zero overhead (skipping hooks, LSP, and skill walks) but requires an explicit `ANTHROPICS_API_KEY`. Additionally, a new `--channels` permission relay has been added to facilitate channel-based integrations.
[View Release](https://github.com/anthropics/claude-code/releases)

## Hot Issues

1.  **[Console Scrolling History Jump (macOS)](#826)**
    *   **Status:** Open | 625 👍
    *   **Impact:** High-votes indicate this is a major UX nuisance. When Claude appends text to the console, the view jumps to the top of the history, forcing users to manually scroll back down.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/826)

2.  **[Cowork: External Drive Access Blocked (Windows)](#29583)**
    *   **Status:** Open | 71 👍
    *   **Impact:** Critical blocker for enterprise users. The `cowork` feature fails on Windows when attempting to access folders outside the home directory (e.g., secondary drives), limiting multi-drive workflows.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/29583)

3.  **[MCP Servers Ignored by VS Code Extension](#19054)**
    *   **Status:** Open | 17 👍
    *   **Impact:** Breaks the integration ecosystem. The VS Code extension reportedly fails to connect to any MCP servers defined in the environment, effectively disabling custom tools for editor users.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/19054)

4.  **[Global Session Setting Leak (Regression)](#20745)**
    *   **Status:** Open | 29 👍
    *   **Impact:** Privacy and workflow regression. Changing the model in one session now overrides the model setting for all other active sessions in different directories.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/20745)

5.  **[spinnerVerbs Setting Ignored (Linux)](#23347)**
    *   **Status:** Open | 19 👍
    *   **Impact:** Customization settings in `~/.claude/settings.json` are not being respected, with default spinner verbs overriding user preferences.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/23347)

6.  **[Feature: CLI Commands for MCP Server Automation](#10447)**
    *   **Status:** Open | 43 👍
    *   **Impact:** High-demand feature. Users want CLI flags to programmatically enable/disable MCP servers to support hook-based automation, rather than relying on the interactive `@` menu.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/10447)

7.  **[Permissions Bypass Failure](#36887)**
    *   **Status:** Open
    *   **Impact:** Security/Annoyance. Despite "bypass permissions" being enabled, users are repeatedly prompted for approval.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/36887)

8.  **[VS Code Extension Ignores Edit/Write Permission Rules](#36884)**
    *   **Status:** Open
    *   **Impact:** The extension prompts for Edit/Write permissions even when `allow` rules are explicitly set in `.claude/settings.json`.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/36884)

9.  **[Grep Tool Silently Returns No Matches](#36875)**
    *   **Status:** Open
    *   **Impact:** Trust issue. The built-in `Grep` tool (ripgrep) fails to find existing strings, while Bash `grep` succeeds, suggesting a configuration or escaping issue in the tool wrapper.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/36875)

10. **[Global Skills Not Surfaced (.md files)](#36888)**
    *   **Status:** Open
    *   **Impact:** Flat `.md` files in `~/.claude/skills/` are not discovered; only folder-based structures are recognized, limiting how users can organize skills.
    *   [Discussion](https://github.com/anthropics/claude-code/issues/36888)

## Key PR Progress

1.  **[fix(plugins): bash-guard — Block Compound Commands](#36645)**
    *   Addresses a critical security bypass where chained bash commands (e.g., `cmd1 && cmd2`) could evade permission allowlists if the second segment matched a deny rule.
    *   [PR #36645](https://github.com/anthropics/claude-code/pull/36645)

2.  **[fix(critical): tool-mutex to Prevent Windows BSOD](#35710)**
    *   Introduces a mutex system to prevent parallel filesystem enumeration, which currently triggers `Wof.sys` BSOD crashes on Windows.
    *   [PR #35710](https://github.com/anthropics/claude-code/pull/35710)

3.  **[feat(plugins): agent-wallet for AI Payments](#36433)**
    *   Adds a plugin providing non-custodial wallet capabilities, enabling agents to handle payments for API access.
    *   [PR #36433](https://github.com/anthropics/claude-code/pull/36433)

4.  **[Add CLAUDE_CODE_GIT_BASH_PATH Environment Variable](#36562)**
    *   Enables Windows users to specify non-standard Git Bash installation paths, improving compatibility.
    *   [PR #36562](https://github.com/anthropics/claude-code/pull/36562)

5.  **[feat: add git-branch-info plugin](#36614)**
    *   Injects git branch context (dirty state, upstream status) into sessions via hooks.
    *   [PR #36614](https://github.com/anthropics/claude-code/pull/36614)

6.  **[Fix Pre/PostToolUse Message Visibility](#36625)**
    *   Corrects the hook output field so that block messages from hooks are actually visible to Claude, not just the user.
    *   [PR #36625](https://github.com/anthropics/claude-code/pull/36625)

7.  **[feat(plugin): destructive-command-guard](#23946)**
    *   A safety plugin that PreToolUse hooks to block dangerous bash commands (mass deletion, Docker nukes) and warns about edits to policy files.
    *   [PR #23946](https://github.com/anthropics/claude-code/pull/23946)

8.  **[Add Mobile Apps Plugin for Project Structure](#36445)**
    *   Provides a guided workflow to audit and reorganize mobile project structures (React Native, Flutter, etc.).
    *   [PR #36445](https://github.com/anthropics/claude-code/pull/36445)

9.  **[docs(plugin-dev): Reduce Skill Context Size](#13204)**
    *   Optimizes documentation for plugin-dev skills to reduce token usage (60% reduction in word count).
    *   [PR #13204](https://github.com/anthropics/claude-code/pull/13204)

10. **[fix(ralph-wiggum): Isolate Loop State per Session](#26077)**
    *   Fixes a bug where running a loop in one session would hijack unrelated sessions in the same project due to shared state files.
    *   [PR #26077](https://github.com/anthropics/claude-code/pull/26077)

## Feature Request Trends
*   **Headless & Automation Support:** There is a strong signal for features that support non-interactive workflows. This includes requests for CLI flags to toggle MCP servers ([#10447](https://github.com/anthropics/claude-code/issues/10447)) and the new `--bare` release flag.
*   **Granular Session Control:** Users are frustrated by shared state. Requests for `/clear --keep-session` ([#31220](https://github.com/anthropics/claude-code/issues/31220)) and fixes for global setting leakage ([#20745](https://github.com/anthropics/claude-code/issues/20745)) highlight a desire for isolation between tasks.
*   **Notification Signals:** Users are asking for terminal bells (`\a`) when Claude is waiting for approval ([#36850](https://github.com/anthropics/claude-code/issues/36850)) to better manage attention in buried sessions.

## Developer Pain Points
*   **Platform Instability:** Windows users are facing significant friction. From the "secondary drive" access bug ([#29583](https://github.com/anthropics/claude-code/issues/29583)) to critical filesystem BSODs requiring manual mutex plugins ([#35710](https://github.com/anthropics/claude-code/pull/35710)), the Windows experience is currently fragile.
*   **Configuration Complexity vs. Reliability:** Developers are struggling with settings not being applied. Issues range from `spinnerVerbs` being ignored to permissions files being bypassed, and even the VS Code extension ignoring standard MCP configurations. The "It works on my machine" problem is exacerbated by the CLI working while the VS Code extension fails.
*   **Permission Fatigue:** While "Bypass Permissions" exists, multiple reports suggest it is unreliable ([#36887](https://github.com/anthropics/claude-code/issues/36887)), leading to repeated prompts that break flow.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest: 2026-03-21

## 1. Today's Highlights
The Codex ecosystem is currently navigating significant instability regarding sandbox environments, particularly with the introduction of CLI v0.115.0/0.116.0. A regression in `bubblewrap` arguments (`--argv0`) has broken agent execution for Linux users, while Windows users are reporting failures with `apply_patch` in nested directories. Concurrently, the team is pushing foundational updates for "Code Mode" on V8 and enhancements to the guardian approval logic.

## 2. Releases
*Note: The latest 24h releases are primarily dependency updates (rusty-v8) and alpha pre-releases (v0.117.0-alpha). No stable release notes detailing breaking changes were provided in the data source for this specific day.*

*   **rusty-v8-v146.4.0**: Underlying V8 engine update.
*   **rust-v0.117.0-alpha series**: Includes Alpha 3, 5, and 6.

## 3. Hot Issues

**Critical Sandbox Regressions (Linux)**
*   [#14919](https://github.com/openai/codex/issues/14919) **[Linux Sandbox Bubblewrap] `bwrap: loopback: Failed RTM_NEWADDR`**
    *   **Why it matters:** Users updating to v0.115.0 are experiencing total sandbox failure on Ubuntu.
    *   **Reaction:** 25 upvotes; comments confirm subagents cannot execute commands.
*   [#15283](https://github.com/openai/codex/issues/15283) **[Sandbox] Unknown option `--argv0` on Ubuntu 20.04**
    *   **Why it matters:** A flag incompatibility with Bubblewrap v0.4.0 breaks v0.116.0 entirely.
    *   **Reaction:** 10 upvotes; users report "Observed in CLI agent environment."

**Windows Ecosystem Instability**
*   [#14744](https://github.com/openai/codex/issues/14744) **[VS Code] `apply_patch` is failing**
    *   **Why it matters:** Core functionality (patch application) is broken in the VS Code extension.
    *   **Reaction:** 11 comments; linked to previous unresolved issues regarding nested files.
*   [#14675](https://github.com/openai/codex/issues/14675) **[Desktop] `apply_patch` fails for nested files under `src/**`**
    *   **Why it matters:** Specific failure mode for Windows Desktop app users working in standard project structures.
    *   **Reaction:** Users report it works at root but fails in subdirectories.

**CLI & UX Friction**
*   [#14936](https://github.com/openai/codex/issues/14936) **[CLI 0.115.0] "Don't ask again" ignored for approvals**
    *   **Why it matters:** A significant UX regression where approval prompts appear for every command despite user preferences.
    *   **Reaction:** 11 upvotes; severely impacts workflow efficiency.
*   [#13476](https://github.com/openai/codex/issues/13476) **[MCP] Excessive approval prompts for Playwright**
    *   **Why it matters:** High friction in using Playwright MCP due to repeated approvals.
    *   **Reaction:** 16 upvotes; request for session-based approval memory.

**Platform Features & Requests**
*   [#10450](https://github.com/openai/codex/issues/10450) **[Desktop App] Remote Development Support**
    *   **Why it matters:** The most requested feature (404 upvotes) for the Desktop App to match VS Code remote capabilities.
*   [#12564](https://github.com/openai/codex/issues/12564) **[VS Code] Allow renaming task/thread titles**
    *   **Why it matters:** Navigation difficulty in history without custom naming.
*   [#14593](https://github.com/openai/codex/issues/14593) **[VS Code] Burning tokens very fast**
    *   **Why it matters:** High cost concern; users suspect the extension is over-processing context.
    *   **Reaction:** 70 upvotes; 162 comments, indicating high anxiety regarding token usage.

## 4. Key PR Progress

**Sandbox & Core Infrastructure**
*   [#15036](https://github.com/openai/codex/pull/15036) **fix(core): disable `command_might_be_dangerous` when unsandboxed**
    *   Addresses a logic error where `ApprovalPolicy::Never` was blocking commands even in explicitly unsandboxed modes.
*   [#15226](https://github.com/openai/codex/pull/15226) **core: eagerly initialize guardian sessions**
    *   Improves the approval pipeline by initializing guardian sessions earlier, preventing "stale trunk" issues during the first approval request.
*   [#15362](https://github.com/openai/codex/pull/15362) **Route shell commands through exec environments**
    *   Adds support for routing shell execution via an `exec-server` when configured, a step towards remote execution capabilities.

**Refactoring & Architecture**
*   [#15276](https://github.com/openai/codex/pull/15276) **Code mode on v8**
    *   Major internal move: Porting Code Mode to a new crate with no dependencies on `codex`, isolating lifetime and tool calling semantics.
*   [#15360](https://github.com/openai/codex/pull/15360) & [#15363](https://github.com/openai/codex/pull/15363) **Fix: `PATH` env var using `OsString`**
    *   Critical fix for non-UTF-8 paths. Codex was failing to prepend aliases to `PATH` if the environment variable contained invalid UTF-8 bytes.

**Plugin & MCP Ecosystem**
*   [#15342](https://github.com/openai/codex/pull/15342) **Plugins TUI install/uninstall**
    *   Adds UI actions for installing/uninstalling plugins directly from the TUI, handling config refreshes and post-install auth flows automatically.
*   [#15258](https://github.com/openai/codex/pull/15258) **[MCP] Pool MCP backends in thread manager**
    *   Implements pooling for Stdio MCP servers, allowing backend reuse across threads to improve resource efficiency.
*   [#15211](https://github.com/openai/codex/pull/15211) **[Hooks] Add `PreToolUse` support**
    *   Introduces shell-only `PreToolUse` hooks, allowing developers to block specific shell commands before execution.

## 5. Feature Request Trends
*   **Enhanced Remote Development:** A massive push for the **Desktop App** to support SSH/Remote development containers (#10450), currently a major gap compared to VS Code.
*   **Workflow Customization:** Users want to manage their AI history better, specifically requesting the ability to **rename task/thread titles** (#12564) and set different reasoning levels for different "collab modes" (#10033).
*   **Lifecycle Hooks:** Developers are building complex integrations and requesting **PreToolUse/PostToolUse** hooks (#14882) to validate or block tool execution programmatically.

## 6. Developer Pain Points
*   **Sandbox Fragility:** The `bubblewrap` implementation is currently the single largest source of bugs. Recent updates (v0.115+) have introduced regressions regarding loopback devices (#14919) and argument parsing (#15283), rendering the tool unusable for many Linux users.
*   **Windows `apply_patch` Flakiness:** Windows users are consistently reporting that `apply_patch` fails on nested files or requires sandbox refreshes (#14675, #15277).
*   **Approval Fatigue:** Recent updates have caused "Don't ask again" settings to be ignored (#14936) or removed "Approve for session" options in the macOS app (#15169), leading to a disruptive number of prompts.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

**Gemini CLI Community Digest**
*Date: 2026-03-21*

### 1. Today's Highlights
The repository is currently in a high-velocity development phase focused on **Agent Capabilities** and **Platform Stability**. Key themes include the integration of the new **Persistent Task Tracker (SDD)** to replace Markdown-based planning, significant **security hardening** for browser agents and prompt injections, and a major refactor to support **compact tool output**. While no official releases were shipped in the last 24 hours, the merge queue indicates an imminent update focusing on security and memory management.

### 2. Releases
*No new releases published in the last 24 hours.*

### 3. Hot Issues
*These issues represent the active focus of the maintainers and significant community concerns.*

*   **[#23318 Feature Request: User-Configurable Daily Quota Reset Times](https://github.com/google-gemini/gemini-cli/issues/23318)**
    *   **Why it matters:** Users are frustrated with the "Rolling 24-Hour Window" quota logic, which penalizes users who trigger the reset at inconsistent times. They demand a fixed daily reset (e.g., midnight local time) to manage usage predictably.
*   **[#23230 exiting plan mode does not switch model](https://github.com/google-gemini/gemini-cli/issues/23230)**
    *   **Why it matters:** A regression where the CLI fails to switch from the planning model to the execution model (`gemini-3-flash-preview`) after plan confirmation, forcing users to manually interrupt to regain expected behavior.
*   **[#22855 Support passing prompt to `/plan`](https://github.com/google-gemini/gemini-cli/issues/22855)**
    *   **Why it matters:** Currently, `/plan` opens a separate interface. Users want to kick off planning in a single command action (e.g., `/plan implement the auth flow`), streamlining the workflow.
*   **[#22933 Fix the loop problem](https://github.com/google-gemini/gemini-cli/issues/22933)**
    *   **Why it matters:** Users are experiencing infinite loops where the agent gets stuck checking non-existent directories and failing policy checks, indicating a flaw in the agent's state recovery logic.
*   **[#22745 Assess the impact of AST-aware file reads](https://github.com/google-gemini/gemini-cli/issues/22745)**
    *   **Why it matters:** An internal Epic investigating Abstract Syntax Tree (AST) integration. This could drastically improve codebase understanding by allowing precise method extraction rather than noisy full-file reads.
*   **[#23175 SDD: deduplicate startup extension warnings](https://github.com/google-gemini/gemini-cli/issues/23175)**
    *   **Why it matters:** As the new `SDD` system rolls out, users are seeing duplicate warnings (e.g., missing configs, deprecated `conductor`) on startup, cluttering the UI.
*   **[#22819 Implement memory routing: global vs. project](https://github.com/google-gemini/gemini-cli/issues/22819)**
    *   **Why it matters:** A critical architectural improvement to ensure the memory subagent distinguishes between user-specific preferences (global) and codebase-specific context (project), preventing context contamination.
*   **[#23320 SDD Phase 3: Tasks Integration](https://github.com/google-gemini/gemini-cli/issues/23320)**
    *   **Why it matters:** Tracking the migration from `plan.md` checklists to a native Directed Acyclic Graph (DAG) task tracker, signaling a move toward more robust, complex task management.
*   **[#22816 Multiple indents for second level dependencies](https://github.com/google-gemini/gemini-cli/issues/22816)**
    *   **Why it matters:** A UI/UX request to improve the readability of the dependency tree, which currently flattens complex relationships into a confusing two-level structure.
*   **[#23323 Task aware compression and memories](https://github.com/google-gemini/gemini-cli/issues/23323)**
    *   **Why it matters:** A request to make the context compression logic "task-aware," ensuring that the current active task isn't compressed away while older tasks are summarized.

### 4. Key PR Progress
*Active development affecting security, core architecture, and UI.*

*   **[#23216 feat(browser): add maxActionsPerTask for browser agent setting](https://github.com/google-gemini/gemini-cli/pull/23216)**
    *   **Change:** Introduces a `maxActionsPerTask` setting (default: 100) for the browser agent.
    *   **Impact:** Prevents the browser agent from running indefinitely or consuming excessive resources during a single task loop.
*   **[#23221 fix(security): strengthen prompt-injection nd backtick defenses](https://github.com/google-gemini/gemini-cli/pull/23221)**
    *   **Change:** Patches vulnerabilities related to command injection via backtick substitution and prompt injection.
    *   **Impact:** Critical security update to sanitize inputs more effectively, closing gaps identified in recent security audits.
*   **[#23286 refactor(cli,core): foundational layout, identity management, and type safety](https://github.com/google-gemini/gemini-cli/pull/23286)**
    *   **Change:** A large refactor establishing infrastructure for upcoming "compact tool output" changes, including `useHistoryManager` and layout fixes.
    *   **Impact:** Foundation for future UI improvements; cleans up technical debt.
*   **[#23281 fix(telemetry): patch memory leak and enforce logPrompts privacy](https://github.com/google-gemini/gemini-cli/pull/23281)**
    *   **Change:** Fixes a ~1.7GB memory leak caused by V8 closure retention in telemetry and ensures `logPrompts` respects privacy settings.
    *   **Impact:** Solves potential Out-Of-Memory (OOM) crashes and improves user privacy compliance.
*   **[#23295 fix(core): enable global session and persistent approval for web_fetch](https://github.com/google-gemini/gemini-cli/pull/23295)**
    *   **Change:** Fixes a regression where "Allow for this session" was ignored for the `web_fetch` tool.
    *   **Impact:** Restores expected approval workflow for web fetching tools.
*   **[#23321 feat(core): add recursive prompter module with dynamic sections](https://github.com/google-gemini/gemini-cli/pull/23321)**
    *   **Change:** Adds a new module to `@google/gemini-cli-core` for building complex, composable system prompts.
    *   **Impact:** Enhances the flexibility of the core prompting engine, allowing for more dynamic context assembly.
*   **[#22412 feat(cli): implement full "GEMINI CLI" logo for logged-out state](https://github.com/google-gemini/gemini-cli/pull/22412)**
    *   **Change:** Adds a new ASCII art banner for the logged-out startup screen.
    *   **Impact:** Polishes the initial user experience and branding.
*   **[#23150 feat(core): implement tool-based topic grouping (Chapters)](https://github.com/google-gemini/gemini-cli/pull/23150)**
    *   **Change:** Implements semantic topic grouping ("Chapters") to replace prompt-only narration, gated behind an experimental flag.
    *   **Impact:** Aims to make long conversation histories more navigable by grouping events into logical chapters rather than relying on unreliable text summaries.
*   **[#23317 fix(extensions): revert broken extension removal behavior](https://github.com/google-gemini/gemini-cli/pull/23317)**
    *   **Change:** Reverts an automatic deletion behavior for broken extensions.
    *   **Impact:** Prevents the CLI from deleting extensions that fail to load; instead, it logs an error, which is safer for developers debugging extension code.
*   **[#23164 Evals: PR Guidance adding workflow](https://github.com/google-gemini/gemini-cli/pull/23164)**
    *   **Change:** Adds a GitHub Action to provide guidance on PRs that modify steering/prompts.
    *   **Impact:** Improves internal quality control by automatically flagging changes that might affect model behavior.

### 5. Feature Request Trends
Based on the latest issues, the community is pushing for:
1.  **Robust Task Management (SDD):** Users want the new "Tracker" system to be deeply integrated, visualizing progress in the terminal UI (Issue #23133) and replacing manual Markdown checklists (Issue #23320).
2.  **Refined Quota Control:** There is a strong desire to move from rolling usage windows to fixed daily quotas (Issue #23318).
3.  **AST Integration:** Developers are asking for the CLI to understand code structure (AST) rather than just treating files as text blobs (Issue #22745), to enable smarter refactors and searches.

### 6. Developer Pain Points
*   **Switching Regressions:** Users are reporting that model switching (e.g., post-plan) and approval persistence (specifically for `web_fetch`) are buggy in recent builds (Issue #23230).
*   **Startup Noise:** The transition to the new SDD system has introduced duplicate warnings and extension errors during startup, degrading the initial CLI experience (Issue #23175).
*   **Browser Agent Safety:** While browser automation is powerful, developers are concerned about cost and safety, requesting strict limits on actions per task (PR #23216) and better read-only noise reduction.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-03-21 | **Source:** github.com/github/copilot-cli

### 1. Today's Highlights
The Copilot CLI team released **v1.0.10** today, focusing on stability and integration fixes. This update addresses critical regressions in clipboard functionality on Windows and Linux, while also resolving working directory detection issues in remote server modes. Concurrently, the community is actively troubleshooting significant issues regarding remote MCP server connectivity in non-interactive modes and model availability warnings for specific agents.

### 2. Releases
**v1.0.10 (2026-03-20)**
*   **Bug Fixes:** Reduced memory footprint when viewing large files; fixed arrow key navigation in `app` terminals; corrected working directory detection for `--server` mode.
*   **Integrations:** The `/login` device flow now operates correctly in Codespaces and remote environments.
*   **v1.0.10-1 (Pre-release):** Added HTML formatting to `/copy` clipboard output for seamless pasting into Microsoft Word, Outlook, and Teams on Windows.
*   **v1.0.10-0 (Pre-release):** Introduced SDK support for custom slash commands, elicitation dialogs, and experimental concurrent sessions.

### 3. Hot Issues
**Top 10 Community Issues (Last 24h)**

1.  **[#2099 "Claude Sonnet 4.5" is not available](https://github.com/github/copilot-cli/issues/2099)**
    *   **Impact:** Users with Copilot Pro are seeing warnings that specific models (Sonnet 4.5) are unavailable in agent definitions, causing the CLI to fall back to default models unexpectedly.
2.  **[#2178 Remote MCP servers broken in `-p` mode (Windows)](https://github.com/github/copilot-cli/issues/2178)**
    *   **Impact:** A regression in v1.0.9 prevents third-party remote MCP servers from loading in non-interactive (prompt) mode, breaking automation workflows.
3.  **[#2143 Text selection/Ctrl+C only captures first character](https://github.com/github/copilot-cli/issues/2143)**
    *   **Impact:** A critical UX bug where copying code snippets from the terminal output results in only the first character being placed in the clipboard.
4.  **[#2082 Linux Clipboard Conflict](https://github.com/github/copilot-cli/issues/2082)**
    *   **Impact:** The standard Linux shortcut `Ctrl+Shift+C` no longer works to copy text, disrupting the workflow for users on Ubuntu 24.04.
5.  **[#1730 `sessionStart` hooks failing](https://github.com/github/copilot-cli/issues/1730)**
    *   **Impact:** Hooks defined in `.github/hooks/` are not firing on session start, preventing users from automating initialization tasks.
6.  **[#1663 Agent implements changes during Plan Mode](https://github.com/github/copilot-cli/issues/1663)**
    *   **Impact:** Agents are ignoring the `[[PLAN]]` prefix and executing code changes immediately rather than just generating a plan, posing a risk to codebase integrity.
7.  **[#252 Global Instructions File Support](https://github.com/github/copilot-cli/issues/252)**
    *   **Impact:** Users are requesting a global configuration file to avoid repeating instructions for every repository, a highly upvoted quality-of-life feature.
8.  **[#2017 Plan Mode ignores "Exit" selection](https://github.com/github/copilot-cli/issues/2017)**
    *   **Impact:** Even when users explicitly select "Exit plan mode," the agent proceeds with implementation, removing user control over the session flow.
9.  **[#2183 Unable to upgrade or downgrade CLI](https://github.com/github/copilot-cli/issues/2183)**
    *   **Impact:** Users attempting to roll back from v1.0.9 due to bugs are facing errors, leaving them stuck on a broken version.
10. **[#2142 `onSessionStart` hook `additionalContext` ignored](https://github.com/github/copilot-cli/issues/2142)**
    *   **Impact:** The documented SDK feature for adding context via hooks is not functioning, limiting extensibility.

### 4. Key PR Progress
*   **Status:** No Pull Requests were updated or merged in the last 24 hours. Development focus appears to be on issue triage and patch releases following the v1.0.9/v1.0.10 rollout.

### 5. Feature Request Trends
Based on recent issue activity:
*   **Enhanced Plan Mode Control:** Users are demanding stricter adherence to "Planning" logic. There is a clear trend of requests to prevent agents from executing code during plan mode unless explicitly authorized.
*   **Global & Modular Configuration:** Developers are looking for ways to centralize instructions (Global Instructions Files) and manage hooks more effectively, specifically composing hooks from extensions with local `hooks.json`.
*   **Clipboard & Terminal UX:** A surge in requests for native clipboard integration (restoring `Ctrl+Shift+C` on Linux and fixing `Ctrl+C` capture) indicates that the TUI is interfering with standard terminal behaviors.

### 6. Developer Pain Points
*   **Model Availability Confusion:** discrepancy between defined agent models (e.g., Claude Sonnet 4.5) and actual availability is causing friction, with users unsure why "Pro" subscriptions aren't granting access to specific models.
*   **Regression Anxiety:** The v1.0.9 release introduced several regressions (MCP connectivity, clipboard failures, theme detection) that are making users hesitant to upgrade.
*   **Non-Interactive Mode Limitations:** Automation workflows relying on `copilot -p` are currently fragile, particularly regarding the loading of remote MCP servers, which negates the benefits of scripted CLI usage.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest: 2026-03-21

## 1. Today's Highlights
The **Kimi Code CLI** repository is undergoing a massive maintenance sprint despite no new version release in the last 24 hours. The core team has closed **20 Pull Requests** addressing a wide array of stability bugs, platform-specific crashes (especially on Windows), and quality-of-life improvements for the terminal interface. Community activity remains high with 11 new issues reported, focusing largely on installation failures, terminal rendering glitches, and MCP integration robustness.

## 2. Releases
*No new releases detected in the last 24 hours.*
*Current stable version context: Issues cite versions ranging from v1.16 to v1.24.*

## 3. Hot Issues

### Critical Bugs & Crashes
*   **[#1380 ACP terminal tool fails with `module acp has no attribute TerminalHandle`](https://github.com/MoonshotAI/kimi-cli/issues/1380)**
    *   **Impact:** Users on v1.17/v1.18 are experiencing failures in the ACP terminal tool, likely due to an API change in the `acp` module.
*   **[#1513 Windows installation script crashes under default PowerShell execution policy](https://github.com/MoonshotAI/kimi-cli/issues/1513)**
    *   **Impact:** New users on Windows 10/11 cannot install the tool on fresh environments as the script exits silently due to execution policy restrictions.
*   **[#1332 & #1321 Service failure on Ubuntu 22.04 / Linux](https://github.com/MoonshotAI/kimi-cli/issues/1332) / [(#1321)](https://github.com/MoonshotAI/kimi-cli/issues/1321)**
    *   **Impact:** Upgrading to v1.17.0 causes the CLI to fail entirely on Linux. One issue traces to uncleaned kernel variables causing the whole service to fail, highlighting a need for defensive input cleaning.
*   **[#1531 Terminal output causes jamming during task execution](https://github.com/MoonshotAI/kimi-cli/issues/1531)**
    *   **Impact:** Real-time terminal output during long-running tasks (like HTTPS setups) causes the CLI to freeze or hang.

### Experience & Feature Requests
*   **[#769 MCP: Should not exit automatically on connection failure](https://github.com/MoonshotAI/kimi-cli/issues/769)**
    *   **Impact:** (👍 5) High-priority request. The CLI currently crashes if *any* MCP server fails to connect. Users demand resilience similar to Claude Code, allowing the session to continue with remaining tools.
*   **[#766 Shell mode: Add pseudo-cwd so `cd` affects subsequent commands](https://github.com/MoonshotAI/kimi-cli/issues/766)**
    *   **Impact:** The current stateless shell mode ignores directory changes (`cd`), making multi-step operations cumbersome.
*   **[#1476 Plan Mode Logic Confusion](https://github.com/MoonshotAI/kimi-cli/issues/1476)**
    *   **Impact:** The tool incorrectly reports "no longer in plan mode" even when it is active, confusing users trying to preview changes.
*   **[#1289 HTTP header illegal character due to trailing space in uname](https://github.com/MoonshotAI/kimi-cli/issues/1289)**
    *   **Impact:** A formatting bug in specific kernel versions sends malformed headers, breaking API calls.
*   **[#1414 Request: Add 'Switch to YOLO Mode' option in approval prompts](https://github.com/MoonshotAI/kimi-cli/issues/1414)**
    *   **Impact:** Users want a quick toggle to auto-approve subsequent actions without restarting the session.
*   **[#1534 Terminal interface disorder and auto-repetition](https://github.com/MoonshotAI/kimi-cli/issues/1534)**
    *   **Impact:** Resizing the terminal causes the UI to break and repeat output indefinitely.

## 4. Key PR Progress
*The repository has seen a significant cleanup effort with 20+ PRs closed recently. Key fixes include:*

*   **[PR #1497: Enforce UTF-8 on Windows](https://github.com/MoonshotAI/kimi-cli/pull/1497)** - Fixes crashes caused by Emoji/Unicode characters in legacy console encodings (cp1252/ascii).
*   **[PR #1498: Configurable default shell for Windows](https://github.com/MoonshotAI/kimi-cli/pull/1498)** - Allows users to switch from `powershell.exe` to `pwsh`, `cmd`, or WSL, resolving hardcoding limitations.
*   **[PR #1460: Relax JSON parsing for Tool Calls](https://github.com/MoonshotAI/kimi-cli/pull/1460)** - Uses `strict=False` to prevent tool execution failures when LLMs inject control characters (newlines/tabs) in JSON arguments.
*   **[PR #1501: Suppress verbose MCP debug messages](https://github.com/MoonshotAI/kimi-cli/pull/1501)** - Cleans up console noise during MCP startup.
*   **[PR #1505: Add Alt+V paste shortcut for Windows](https://github.com/MoonshotAI/kimi-cli/pull/1505)** - Bypasses Windows Terminal's hijacking of Ctrl+V, aligning with Claude Code behavior.
*   **[PR #1506: Add 'Skip' option for tool approval](https://github.com/MoonshotAI/kimi-cli/pull/1506)** - Users can now skip a specific tool call without aborting the entire task execution.
*   **[PR #1507: Add `/timeout` command](https://github.com/MoonshotAI/kimi-cli/pull/1507)** - Allows extending the default 60s timeout for shell commands (vital for large npm/pip installs).
*   **[PR #1472: Restore Codeblock Copy in Web UI](https://github.com/MoonshotAI/kimi-cli/pull/1472)** - Fixes the clipboard API which failed on non-HTTPS (HTTP/localhost) contexts.
*   **[PR #1463: OSC Terminal Notifications](https://github.com/MoonshotAI/kimi-cli/pull/1463)** - Adds desktop notifications when agent tasks complete.
*   **[PR #1462: Escape Rich Markup in error content](https://github.com/MoonshotAI/kimi-cli/pull/1462)** - Prevents CLI crashes when error messages contain text that looks like Rich markup tags.

## 5. Feature Request Trends
*   **MCP Resilience:** Users are strongly requesting that the CLI **not crash** if MCP servers fail (Issue #769).
*   **Shell Session State:** There is a recurring demand for **persistent shell state** (pseudo-cwd) so directory changes persist across commands (Issue #766).
*   **Approval Workflow UX:** Users want finer-grained control during execution, specifically the ability to **"Skip"** single tool invocations or dynamically switch to **"YOLO mode"** (Issues #1506, #1414).

## 6. Developer Pain Points
*   **Windows Compatibility:** Windows users are facing a "double whammy" of installation failures (Powershell policies) and runtime encoding crashes (Issue #1513, #1497).
*   **Terminal Instability:** Resizing windows or handling async output during shell commands is causing the UI to freeze, jam, or render out of order (Issues #1531, #1534).
*   **Fragile Parsing:** The CLI is overly sensitive to malformed inputs from LLMs (JSON strictness) or system environments (kernel variables in headers), leading to total failures rather than graceful degradation (Issues #1460, #1321).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: 2026-03-21

## 1. Today's Highlights
The OpenCode community is currently managing significant service disruptions, specifically widespread **OAuth failures** for Anthropic Claude users across both legacy and newer versions. Concurrently, maintainers are pushing critical updates to address the recent legal removal of Anthropic-specific code, while contributors are ramping up efforts on AI SDK v6 integration and resolving critical memory leaks affecting long-running server instances.

## 2. Releases
*No new releases published in the last 24 hours.*

## 3. Hot Issues

*   **[#18267 [OPEN] - Claude code 0auth broked!?](https://github.com/anomalyco/opencode/issues/18267)**
    *   **Why it matters:** This is the most active thread (127+ comments) highlighting a critical failure in Anthropic's OAuth flow (Error 429). Users are locked out of Pro accounts.
    *   **Reaction:** High frustration; users report being unable to login regardless of client version.

*   **[#18362 [OPEN] - Anthropic Claude Pro/Max OAuth fails... invalid authorization code](https://github.com/anomalyco/opencode/issues/18362)**
    *   **Why it matters:** Confirms the OAuth issue affects the latest versions (1.2.27) on Windows, specifically failing at the `/provider/anthropic/oauth/callback` endpoint.
    *   **Reaction:** Users are downgrading or switching providers as a workaround.

*   **[#17908 [OPEN] - Massive memory leak (60GB+ OOM crash) on Server](https://github.com/anomalyco/opencode/issues/17908)**
    *   **Why it matters:** A critical stability bug where closing the Desktop app triggers a massive memory spike in the connected `opencode serve` instance, leading to OOM crashes.
    *   **Reaction:** High urgency; server instability is a blocker for remote development workflows.

*   **[#18432 [OPEN] - Windows: Persistent Directory Corruption](https://github.com/anomalyco/opencode/issues/18432)**
    *   **Why it matters:** Reports of OpenCode creating directory junction loops and reserved "nul" files on Windows, persisting even after uninstallation.
    *   **Reaction:** Users concerned about system stability and difficulty cleaning up the mess.

*   **[#18423 [OPEN] - Ollama subagent executes tool calls correctly but returns empty text](https://github.com/anomalyco/opencode/issues/18423)**
    *   **Why it matters:** Breaks multi-agent workflows using local Ollama models; the orchestrator receives no text feedback despite tools running.
    *   **Reaction:** Significant impact on users relying on local agent orchestration.

*   **[#2072 [OPEN] - Support for Cursor?](https://github.com/anomalyco/opencode/issues/2072)**
    *   **Why it matters:** A perennial top-requested feature. With Cursor releasing a CLI, the community is eager for official integration.
    *   **Reaction:** 136+ upvotes; strong desire for interoperability.

*   **[#16729 [CLOSED] - High memory usage and database bloat](https://github.com/anomalyco/opencode/issues/16729)**
    *   **Why it matters:** Identified SQLite bloat (1.99GB) and memory leaks in long-running instances. Recently closed, suggesting a fix is imminent or deployed.
    *   **Reaction:** Relief regarding the cleanup of database logs.

*   **[#10416 [OPEN] - OpenCode is not private by default?](https://github.com/anomalyco/opencode/issues/10416)**
    *   **Why it matters:** Security/Privacy concern. Session titles appear to be generated by a remote process even when using local LLMs.
    *   **Reaction:** Users demand clearer transparency on telemetry and network usage.

*   **[#7602 [OPEN] - Native Model Fallback / Failover Support](https://github.com/anomalyco/opencode/issues/7602)**
    *   **Why it matters:** High-priority feature request. Currently, OpenCode cannot automatically retry a request with a different model if the primary one rate-limits or errors.
    *   **Reaction:** Strong demand for more resilient routing logic.

*   **[#18398 [OPEN] - How to skip model.dev checks?](https://github.com/anomalyco/opencode/issues/18398)**
    *   **Why it matters:** Users are blocked from using valid models (e.g., Mistral Small 4 on OpenRouter) due to strict schema validation.
    *   **Reaction:** Request for an "advanced override" flag to bypass artificial constraints.

## 4. Key PR Progress

*   **[#18186 [CLOSED] - anthropic legal requests](https://github.com/anomalyco/opencode/pull/18186)**
    *   **Changes:** Removed Anthropic-specific prompts, provider hints, and the `opencode-anthropic-auth` builtin plugin per legal request.
    *   **Impact:** Major structural change to the codebase to comply with legal requirements.

*   **[#18452 [OPEN] - fix: lazy runtime imports in facades to break bundle cycles](https://github.com/anomalyco/opencode/pull/18452)**
    *   **Changes:** Refactors import logic to defer runtime access, preventing `undefined is not an object` crashes in the bundled binary.
    *   **Impact:** Critical stability fix for the TUI and desktop app bundles.

*   **[#18311 [OPEN] - fix: skip Anthropic cache control for OAuth](https://github.com/anomalyco/opencode/pull/18311)**
    *   **Changes:** Ensures Anthropic OAuth requests bypass the cache-control headers that were breaking the login flow.
    *   **Impact:** Directly addresses the critical login issues reported in today's top bugs.

*   **[#18450 [OPEN] - feat: use native Output.object() for structured output](https://github.com/anomalyco/opencode/pull/18450)**
    *   **Changes:** Migrates from a custom `StructuredOutput` tool to the AI SDK's native `Output.object()` via `experimental_output`.
    *   **Impact:** Improves reliability and future-proofing of structured data generation.

*   **[#18433 [OPEN] - feat: AI SDK v6 support](https://github.com/anomalyco/opencode/pull/18433)**
    *   **Changes:** Initial work to support the latest AI SDK v6.
    *   **Impact:** Foundation for future model compatibility and performance improvements.

*   **[#13854 [OPEN] - fix(tui): stop streaming markdown/code after message completes](https://github.com/anomalyco/opencode/pull/13854)**
    *   **Changes:** Fixes a bug where the TUI treated finished messages as still streaming, causing rendering artifacts (e.g., missing last table row).
    *   **Impact:** Visual polish for the TUI.

*   **[#12856 [OPEN] - bugfix to snapshot pruning](https://github.com/anomalyco/opencode/pull/12856)**
    *   **Changes:** Fixes snapshot pruning logic to ensure old directories are deleted, not just the files within them.
    *   **Impact:** Reduces disk space usage by cleaning up session artifacts more effectively.

*   **[#17170 [OPEN] - fix(cli): remove stray dot from --help logo](https://github.com/anomalyco/opencode/pull/17170)**
    *   **Changes:** Fixes a rendering quirk in the CLI help text caused by yargs stripping whitespace.
    *   **Impact:** Minor aesthetic improvement to the CLI.

*   **[#4917 [OPEN] - feat: tool description for Bash tool now advises model as to actual shell](https://github.com/anomalyco/opencode/pull/4917)**
    *   **Changes:** Dynamically updates the Bash tool description to tell the LLM which shell (zsh, bash, etc.) is actually in use.
    *   **Impact:** Reduces syntax errors when the LLM generates shell commands.

*   **[#14251 [OPEN] - feat(tui): show session ID in /status dialog](https://github.com/anomalyco/opencode/pull/14251)**
    *   **Changes:** Adds the current Session ID to the `/status` output.
    *   **Impact:** Improves debuggability for users and developers.

## 5. Feature Request Trends
*   **Interoperability:** High demand for integration with other AI editors and tools, specifically **Cursor CLI** support.
*   **Resiliency:** Users are strongly requesting **Native Model Fallback** mechanisms to handle rate limits and errors automatically without agent failure.
*   **Platform Support:** Continued requests for better **Windows support** (WSL integration) and **SSH-based remote connections** in the Desktop app.
*   **Privacy Controls:** Users are asking for more granular control over network access, specifically the ability to disable remote "telemetry" (like session title generation) when using local models.

## 6. Developer Pain Points
*   **Authentication Fragility:** The current OAuth implementation for major providers (Anthropic) is brittle; updates to provider APIs or strict caching rules are breaking logins entirely.
*   **Memory Leaks:** "Memory fatigue" is setting in. Multiple issues regarding unbounded memory growth (OOM crashes) in `opencode serve` and the Desktop app suggest deep architectural issues with resource cleanup (SSE connections, sidebar prefetching).
*   **Context Saturation:** Developers are frustrated that tool calls consume up to 80% of the context window, leaving little room for actual code logic ("token tax").
*   **Upgrade Friction:** The strict `model.dev` checks are preventing power users from accessing new/unsupported models on providers like OpenRouter, forcing them to fork or wait.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest: 2026-03-21

## 1. Today's Highlights
Qwen Code is rapidly approaching the **v0.13.0** milestone with nightly builds and a preview release (`v0.13.0-preview.1`) currently available. The engineering team is aggressively addressing critical stability concerns regarding file editing safety and "hallucinated" content overwrites, while simultaneously enhancing the VS Code extension with requested features like **Plan Mode** and **Follow-up Suggestions**.

## 2. Releases
**Latest Version:** `v0.13.0-preview.1` & `v0.13.0-nightly.20260321.38caa0b21`
*   **Pipeline Fix:** Resolved an issue with duplicate `finish_reason` chunks from OpenRouter.
*   **System Prompts:** Added options for system prompt customization.
*   **Source:** [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

## 3. Hot Issues

### **Critical Stability Risks**
*   **[#2499 Agent Overwrites Files (Data Loss)](https://github.com/QwenLM/qwen-code/issues/2499)**
    *   **Impact:** High. Users report the agent frequently uses `write_file` to completely overwrite files with incorrect or truncated content, skipping the necessary `read_file` verification step. This poses a significant risk of data loss for source files.
*   **[#2460 Frequent "Edit Failed" & File Corruption](https://github.com/QwenLM/qwen-code/issues/2460)**
    *   **Impact:** High. A user reported that repeated edit failures led the agent to attempt using Node.js/PowerShell to modify files, which resulted in widespread code corruption and project destruction.
*   **[#2540 Dangerous Shell Command Execution](https://github.com/QwenLM/qwen-code/issues/2540)**
    *   **Impact:** High. The agent suggested a command (`taskkill /F /IM node.exe`) to stop Vite servers, which inadvertently killed the Qwen process itself due to over-broad process targeting. Highlights the need for smarter tool execution logic.

### **Usability & Features**
*   **[#2040 Project-Level Insight Support](https://github.com/QwenLM/qwen-code/issues/2040)**
    *   **Reaction:** 15 Comments. High demand for moving the "Insight" functionality from a machine-level view to a project-specific view to better manage multi-project workflows.
*   **[#2523 Follow-up Suggestions in Web UI](https://github.com/QwenLM/qwen-code/issues/2523)**
    *   **Reaction:** 3 Comments. Request to integrate "Next Step Suggestions" (similar to Claude Code) into the Web UI to suggest logical actions (e.g., "run tests") after a task completes.
*   **[#2034 Customize/Disable "Thinking" Quotes](https://github.com/QwenLM/qwen-code/issues/2034)**
    *   **Reaction:** 2 Likes, 2 Comments. Users find the default rotating quotes in the TUI distracting and request an option to customize or disable them.

### **File Handling & Bugs**
*   **[#1977/2084 Chinese Filename Parsing Issues](https://github.com/QwenLM/qwen-code/issues/1977)**
    *   **Impact:** Medium. Recurring reports (multiple issues) that the CLI inserts spaces between numbers and Chinese characters in filenames/paths, causing file lookups to fail.
*   **[#2466 Branching for MCP (Model Context Protocol)](https://github.com/QwenLM/qwen-code/issues/2466)**
    *   **Reaction:** 4 Comments. Users want to define branches or workflows within MCP server configurations, rather than just linear execution.
*   **[#2497 Disable Persistent "Always Allow" Approvals](https://github.com/QwenLM/qwen-code/issues/2497)**
    *   **Reaction:** 3 Comments. Security/Control request to add an option to force confirmation for every action, preventing the "Always Allow" setting from persisting indefinitely.

## 4. Key PR Progress

### **Critical Fixes**
*   **[#2554 Enforce Read-Before-Write Guard](https://github.com/QwenLM/qwen-code/pull/2554)**
    *   **Status:** Open. A high-priority fix addressing Issue #2499. Implements a 3-layer defense (system prompt, tool description, runtime guard) to prevent `write_file` from overwriting files with significantly shorter/hallucinated content.
*   **[#2547 Improve C++/Java/Python LSP Support](https://github.com/QwenLM/qwen-code/pull/2547)**
    *   **Status:** Open. Fixes a bug where document-level operations (definitions, references) failed for non-TypeScript languages (jdtls, clangd, pylsp) due to missing `textDocument/didOpen` events and URI path mismatches.
*   **[#2550 Fix VSCode Input Lag](https://github.com/QwenLM/qwen-code/pull/2550)**
    *   **Status:** Open. Resolves severe input lag (5s+ delays) in long conversations by optimizing the React render cycle with `React.memo`.

### **New Features**
*   **[#2525 Add Follow-up Suggestions Feature](https://github.com/QwenLM/qwen-code/pull/2525)**
    *   **Status:** Open. Implements context-aware "Next Step Suggestions" (similar to Claude Code) for the CLI and WebUI.
*   **[#2551 Enable Plan Mode in VSCode](https://github.com/QwenLM/qwen-code/pull/2551)**
    *   **Status:** Open. Brings "Plan Mode" (approval workflow before execution) to the VSCode extension, achieving feature parity with the CLI.
*   **[#2548 Expose /skills as Slash Command](https://github.com/QwenLM/qwen-code/pull/2548)**
    *   **Status:** Open. Adds a secondary picker UI for the `/skills` command in VSCode, allowing users to visually browse and select available skills.
*   **[#2371 Add `/btw` Slash Command](https://github.com/QwenLM/qwen-code/pull/2371)**
    *   **Status:** Open. Introduces an ephemeral "By The Way" side-question mode that allows users to ask quick questions without adding noise to the main conversation history.

### **Maintenance & Ops**
*   **[#2000 Enable Parallel Tool Call Execution](https://github.com/QwenLM/qwen-code/pull/2000)**
    *   **Status:** Merged/Closed. Switches tool execution from sequential to concurrent (`Promise.allSettled`), significantly improving performance when multiple independent tools are called.
*   **[#2539 Support Non-GitHub Git URLs](https://github.com/QwenLM/qwen-code/pull/2539)**
    *   **Status:** Open. Enables installing extensions from self-hosted GitLab, Bitbucket, or other git sources by fixing URL parsing logic.

## 5. Feature Request Trends
1.  **Safety & Control:** There is a strong trend toward enhancing file safety (#2499) and granular approval control (#2497). Users want the AI to be less "destructive" and more transparent.
2.  **Parity Across Clients:** Users are actively requesting features available in the CLI (like Insight, Plan Mode, Slash commands) be brought to the VSCode extension and Web UI.
3.  **Workflow Efficiency:** "Follow-up Suggestions" (#2523) and "Parallel Execution" (#2000) indicate a desire for the tool to anticipate next steps and handle multi-part tasks faster.

## 6. Developer Pain Points
*   **"Hallucinated" Edits:** The most critical pain point is the `write_file` tool overwriting valid code with incorrect or truncated versions, forcing users to rely on external version control to recover data.
*   **Whitespace/String Handling:** Persistent issues with the agent inserting unwanted spaces in filenames (especially with non-ASCII characters or mixed numbering), leading to "File not found" loops.
*   **Path Handling on Windows:** Multiple reports of the CLI failing to handle backslashes or spaces in Windows paths correctly, breaking file operations.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*