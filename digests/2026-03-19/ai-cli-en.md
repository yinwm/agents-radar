# AI CLI Tools Community Digest 2026-03-19

> Generated: 2026-03-18 17:14 UTC | Tools covered: 7

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

# AI Developer Tools Ecosystem Report: 2026-03-19

## 1. Ecosystem Overview
The AI CLI landscape is currently defined by a transition from **experimental agents** to **platform-grade development environments**. While early iterations focused on simple chat-to-code translation, today’s ecosystem is aggressively tackling **architectural scalability**—evidenced by industry-wide movements toward **remote execution daemons**, **MCP (Model Context Protocol) standardization**, and **multi-agent orchestration**. Simultaneously, a "platform maturity" crisis is emerging: tools are struggling with the reliability basics required for enterprise adoption (e.g., Windows stability, efficient context management, and robust permission systems), even as they race to add advanced reasoning capabilities.

## 2. Activity Comparison

| Tool | Issue Activity | PR Velocity | Release Status | Primary Focus Area |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **High** (1.2k+ reactions on top issues) | **High** (10 Major PRs merged) | **v2.1.78** | Plugin Ecosystem & Hooks |
| **OpenAI Codex** | **Medium** (Top req: 386 votes) | **Medium** (Alpha iteration) | **v0.116.0-alpha** | Remote Execution Stack |
| **Gemini CLI** | **Medium** (Plan Mode bugs) | **Medium** (Sandbox/Policy) | **v0.35.0-preview.1** | Agent Planning & Isolation |
| **GitHub Copilot** | **Medium** (UI regressions) | **Low** (1 PR noted) | **v1.0.8-0** | Extensibility & MCP |
| **Kimi Code** | **Low** (Niche UX requests) | **Low** (Internal refactor) | **v1.24.0** | Plan Mode UX |
| **OpenCode** | **High** (Clipboard/Snapshot bugs) | **High** (Multi-session daemon) | **No new release** | Architecture Refactor |
| **Qwen Code** | **Critical** ("Edit Failed" crisis) | **High** (Hotfixes merged) | **v0.12.5-preview.0** | Stability & "Agent Arena" |

## 3. Shared Feature Directions
Across the ecosystem, communities are converging on three critical requirements:

*   **Parallel Execution & Isolation (Git Worktrees):**
    *   **Affected:** *Gemini CLI, OpenCode, Qwen Code.*
    *   **Requirement:** Developers are demanding the ability to run multiple parallel agents. The preferred technical solution is **Git Worktree** integration, allowing agents to work on isolated branches of the same codebase simultaneously without conflicting file states. Qwen Code is pushing this furthest with its "Agent Arena" concept.

*   **Context Management & Observability:**
    *   **Affected:** *Claude Code, OpenAI Codex, Qwen Code, GitHub Copilot.*
    *   **Requirement:** Users are frustrated by "black box" token usage. There is a unified demand for **real-time token counters** and granular breakdowns of context usage (e.g., Qwen's `/context` command). Additionally, inefficient context handling (specifically burning tokens on background tasks or repeated full-file reads) is a top complaint across *Codex* and *Copilot*.

*   **MCP (Model Context Protocol) Integration:**
    *   **Affected:** *GitHub Copilot, OpenCode, Kimi Code.*
    *   **Requirement:** Standardization on **MCP** for extending tool capabilities. *OpenCode* is actively being requested to run *as* an MCP server (client mode), while *Copilot* and *Kimi* are refining server validation and connection stability.

## 4. Differentiation Analysis

*   **Claude Code:** Focuses on **Extensibility via Plugins**. Unlike others, it is solving gaps in its core product (Windows BSOD, Terminals) by shipping them as community-maintained plugins (e.g., `tool-mutex`, `scroll-fix`), fostering a vibrant "fix-it-yourself" ecosystem.
*   **OpenAI Codex:** Focuses on **Enterprise/Remote Infrastructure**. Its development energy is spent on `exec-server` and secure remote auth, positioning it as the choice for enterprise engineering teams requiring remote workspace support, rather than individual local developers.
*   **Qwen Code:** Focuses on **Model Competition**. It is unique in pursuing "Agent Arena" features, allowing users to pit different models (or versions) against the same task. This caters to developers optimizing for model quality and cost.
*   **Kimi Code:** Focuses on **Workflow UX**. It is heavily refining the "Plan Mode" experience, specifically how users interact with and approve AI-generated strategies (e.g., multi-option plan selection), positioning itself as a tool for cautious, controlled refactoring.

## 5. Community Momentum & Maturity

*   **High Maturity, Growing Pains:** **Claude Code**. The community is massive and active (1.2k comments on a single issue), but the tool is suffering from "success problems"—scale-related issues like rate limits and infrastructure strain are creating friction for Max subscribers.
*   **Rapidly Maturing:** **OpenAI Codex**. The shift to a Rust-based architecture (`v0.116.0`) and the heavy focus on remote execution stacks indicate a move away from "science project" to production-grade tooling, though macOS/Windows parity remains a weak point.
*   **Stability Crisis:** **Qwen Code**. The "Critical Edit Failed" regression has created a crisis of confidence. While the feature set (Agent Arena) is innovative, the core editing reliability is currently broken, forcing rollbacks.
*   **Niche/Specialized:** **Kimi Code**. Lower community volume but focused development on specific UX needs (Plan Mode). **OpenCode** has high engagement but is currently stalled by a "Snapshot system" bug that fills disks (9.5GB/hour), representing a significant technical debt hurdle.

## 6. Trend Signals for Developers

1.  **The "Agent" Tax:** Parallel and multi-agent workflows (Worktrees) are becoming the standard for serious AI development workflows. Tools that cannot handle multi-file, multi-branch operations safely will be left behind.
2.  **Windows is an Afterthought:** Despite the user base, Windows support remains the primary instability vector across almost all tools (BSODs in Claude, Path handling in OpenCode/Qwen, Performance issues in Kimi). Developers on Windows should expect to troubleshoot environment-specific bugs.
3.  **Shift to "Permission Fatigue" Solutions:** As tools become more powerful, the constant prompting for permission is breaking flow. *Claude* and *Gemini* are actively working on "Allow Always" policies and "YOLO" modes to reduce friction.
4.  **Standardization via MCP:** The industry is coalescing around MCP. If you are building custom tooling or integrations, supporting MCP is becoming the requirement for interoperability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Analysis Period: Data as of 2026-03-19*

## 1. Top Skills Ranking
Based on pull request activity, technical specificity, and community utility, here are the most impactful Skills currently under review:

*   **[document-typography (#514)](https://github.com/anthropics/skills/pull/514)**
    *   **Functionality:** A quality control skill that prevents common typographic errors in AI-generated docs, specifically orphaned words (1-6 words spilling over) and widow paragraphs (headers stranded at page bottom).
    *   **Status:** Open
    *   **Insight:** Addresses a universal pain point in document generation, offering specific visual formatting rules for AI outputs.

*   **[skill-quality-analyzer & skill-security-analyzer (#83)](https://github.com/anthropics/skills/pull/83)**
    *   **Functionality:** Meta-skills that evaluate other Skills across five dimensions (Structure, Documentation, Safety, Reliability, Efficacy).
    *   **Status:** Open
    *   **Insight:** High-value "dogfooding" tool; essential for maintaining the integrity of the skills marketplace.

*   **[frontend-design (#210)](https://github.com/anthropics/skills/pull/210)**
    *   **Functionality:** A refinement of the frontend-design skill to ensure instructions are actionable and coherent within a single conversation context.
    *   **Status:** Open
    *   **Insight:** Focuses on prompt engineering hygiene—ensuring Claude can actually execute the instructions provided without getting stuck in loops.

*   **[codebase-inventory-audit (#147)](https://github.com/anthropics/skills/pull/147)**
    *   **Functionality:** A 10-step workflow to identify orphaned code, unused files, and documentation gaps, outputting a `CODEBASE-STATUS.md`.
    *   **Status:** Open
    *   **Insight:** Responds to the need for "cleanup" and maintenance in active development environments.

*   **[ODT skill (#486)](https://github.com/anthropics/skills/pull/486)**
    *   **Functionality:** Enables creation, parsing, and template filling of `.odt` (OpenDocument Text) files, an ISO standard format used by LibreOffice and others.
    *   **Status:** Open
    *   **Insight:** Expands document interoperability beyond the proprietary .docx format, crucial for open-source enterprise workflows.

*   **[shodh-memory (#154)](https://github.com/anthropics/skills/pull/154)**
    *   **Functionality:** Implements a persistent memory system for AI agents, maintaining context across different conversations via a `proactive_context` mechanism.
    *   **Status:** Open
    *   **Insight:** A critical infrastructure component for building stateful AI agents rather than stateless chatbots.

## 2. Community Demand Trends
Analysis of open Issues reveals three dominant vectors for Skill development:

*   **Reliability & Debugging Infrastructure:** Users are frustrated by a "0% trigger rate" where Skills fail to invoke correctly (e.g., Issue [#556](https://github.com/anthropics/skills/issues/556)). There is high demand for Skills that debug other Skills or provide better visibility into why a specific Skill failed to trigger.
*   **Governance & Security:** Following Issue [#492](https://github.com/anthropics/skills/issues/492) regarding trust boundary abuse and [#412](https://github.com/anthropics/skills/issues/412) regarding agent governance, the community is prioritizing security analysis tools to verify community-submitted Skills before execution.
*   **Enterprise Interoperability:** Issues like [#29](https://github.com/anthropics/skills/issues/29) (AWS Bedrock usage) and [#532](https://github.com/anthropics/skills/issues/532) (Enterprise SSO compatibility) highlight a need for Skills that function within complex, authenticated enterprise environments rather than just local standalone scripts.

## 3. High-Potential Pending Skills
These PRs are active, unmerged, and solve immediate, high-frequency problems:

*   **[YAML Special Characters Detection (#361)](https://github.com/anthropics/skills/pull/361):** Adds a pre-parse check to prevent silent errors caused by unquoted YAML characters (e.g., `:` or `#`) in Skill descriptions. Critical for the `skill-creator` workflow.
*   **[avoid-ai-writing (#535)](https://github.com/anthropics/skills/pull/535):** An "anti-style" skill that detects and rewrites 21 categories of "AI-isms" to make generated text sound more human. High utility for content creation workflows.
*   **[CONTRIBUTING.md (#509)](https://github.com/anthropics/skills/pull/509):** A documentation update to address the community health gap (repo score: 25%). This is low-code but high-impact for enabling wider community contributions.

## 4. Skills Ecosystem Insight
The community is currently concentrating its demand on **Meta-Skills and Infrastructure**—shifting from asking "what can this tool do?" to "how do we make these tools reliable, secure, and interoperable with enterprise systems?"

---

# Claude Code Community Digest: 2026-03-19

## Today's Highlights

Today's digest centers on **v2.1.78**, which introduces critical hooks for API error handling and plugin state persistence. The community is reacting strongly to persistent **rate limiting issues** affecting Max subscribers and a critical **Windows BSOD bug** caused by parallel file system operations. A vibrant ecosystem of community plugins is emerging to address core gaps, including fixes for terminal scrolling, file system mutexes, and PowerShell integration.

## Releases

**v2.1.78**
*   **Added `StopFailure` hook event:** Allows plugins to react when a turn ends due to API errors (rate limits, auth failures).
*   **Added `${CLAUDE_PLUGIN_DATA}` variable:** Enables persistent state storage for plugins that survives updates; `/plugin uninstall` now prompts before deleting this data.
*   **Added `effort` parameter:** (Note: Changelog text was cut off in data, implies new control over token usage or reasoning depth).

## Hot Issues

1.  **[#16157](https://github.com/anthropics/claude-code/issues/16157) - Usage limits with Max subscription**
    *   **Impact:** High friction for premium users.
    *   **Reaction:** 1,249 comments and 544 reactions. Users report hitting usage limits "instantly" despite being on the top-tier Max subscription ($200/mo).

2.  **[#34229](https://github.com/anthropics/claude-code/issues/34229) - Phone verification**
    *   **Impact:** Authentication blocker.
    *   **Reaction:** 435 comments. High volume of reports regarding failures in the phone verification flow.

3.  **[#13514](https://github.com/anthropics/claude-code/issues/13514) - Feature: Delete Claude Code sessions**
    *   **Impact:** Data management.
    *   **Reaction:** 55 reactions. Long-standing request for users to manage and delete their conversation history.

4.  **[#28240](https://github.com/anthropics/claude-code/issues/28240) - Permission prompts on `cd` in compound bash statements**
    *   **Impact:** Workflow friction.
    *   **Reaction:** 54 reactions. The tool incorrectly triggers approval prompts on the directory change rather than the actual command, breaking flow.

5.  **[#2939](https://github.com/anthropics/claude-code/issues/2939) - Image upload size limit causes persistent failure**
    *   **Impact:** Session corruption.
    *   **Reaction:** 51 comments. Uploading a large image "pollutes" the context, causing all subsequent API calls to fail until the session is reset.

6.  **[#20469](https://github.com/anthropics/claude-code/issues/20469) - M365 Connector for Max Individual Users**
    *   **Impact:** Feature parity.
    *   **Reaction:** 35 reactions. Individual Max users ($200/mo) cannot access the Microsoft 365 Connector, which is available to cheaper Team plans.

7.  **[#26554](https://github.com/anthropics/claude-code/issues/26554) - Cowork: Plan9 mount fails**
    *   **Impact:** Collaboration feature blocker.
    *   **Reaction:** 56 reactions. Users experiencing RPC errors preventing Cowork file mounting on macOS.

8.  **[#23704](https://github.com/anthropics/claude-code/issues/23704) - Read tool PDF support undocumented/broken**
    *   **Impact:** Documentation/UX.
    *   **Reaction:** Users frustrated that PDF reading requires `poppler-utils`, which is undocumented and often missing, causing silent failures.

9.  **[#18699](https://github.com/anthropics/claude-code/issues/18699) - Allow always permission option**
    *   **Impact:** UX/QoL.
    *   **Reaction:** 24 reactions. Users want a "Allow always" option to save permissions to `settings.json` to avoid repeated prompts for trusted commands.

10. **[#35870](https://github.com/anthropics/claude-code/issues/35870) - Permissions bypassed in VS Code/Cursor**
    *   **Impact:** Security.
    *   **Reaction:** Newly reported critical issue where permission prompts are being bypassed or not persisted correctly in the VS Code/Cursor extensions.

## Key PR Progress

1.  **[#35710](https://github.com/anthropics/claude-code/pull/35710) - Add tool-mutex plugin (Critical Windows Fix)**
    *   Addresses **BSOD crashes (Wof.sys)** on Windows by serializing parallel file system operations (Glob/Grep/Read/Bash) that overload the driver.

2.  **[#35864](https://github.com/anthropics/claude-code/pull/35864) - Add worktree-guardian plugin**
    *   Adds a `SessionStart` hook to scan for orphaned agent worktrees with uncommitted changes, preventing silent data loss during cleanup.

3.  **[#35683](https://github.com/anthropics/claude-code/pull/35683) - Add scroll-fix plugin**
    *   Community fix for the widespread terminal "scroll-to-top" regression. Includes a Ctrl+6 toggle to freeze the screen buffer.

4.  **[#35761](https://github.com/anthropics/claude-code/pull/35761) - Add powershell-default plugin**
    *   Configures PowerShell 7+ Preview as the default shell for Claude Code on all platforms, replacing Bash.

5.  **[#35684](https://github.com/anthropics/claude-code/pull/35684) - Add bridge-fix plugin**
    *   Fixes Chrome extension bridge connection failures for Max subscribers via a plugin-based workaround.

6.  **[#35168](https://github.com/anthropics/claude-code/pull/35168) - Add Etudes plugin**
    *   A "sprint coach" tool that interviews developers about their project patterns and generates daily accountability sprints.

7.  **[#15806](https://github.com/anthropics/claude-code/pull/15806) - Fix UTF-8 safe string slicing**
    *   Fixes Rust panics when processing Korean/CJK multi-byte text.

8.  **[#34798](https://github.com/anthropics/claude-code/pull/34798) - Root cause analysis: Terminal scroll**
    *   Deep dive into the `Ink` cursor handling causing the scroll-to-top bug on Windows Terminal.

9.  **[#35350](https://github.com/anthropics/claude-code/pull/35350) - Use portable shebangs in shell scripts**
    *   Fixes plugin hook failures on NixOS and other non-standard distros by using `#!/usr/bin/env bash`.

10. **[#35543](https://github.com/anthropics/claude-code/pull/35543) - Fix resultmessage in headless sdk**
    *   Ensures result messages are correctly emitted when running in headless SDK mode.

## Feature Request Trends

*   **Permission Granularity:** High demand for "Allow always" or "Allow for project" permissions to avoid repetitive approvals for safe commands ([#18699](https://github.com/anthropics/claude-code/issues/18699)).
*   **Session Management:** Users want the ability to delete, archive, or manage the lifetime of their Claude Code sessions ([#13514](https://github.com/anthropics/claude-code/issues/13514)).
*   **Model Selection:** Max users are frustrated by the inability to select specific high-context models (like Sonnet 4.6 1M) via the `/model` command ([#34773](https://github.com/anthropics/claude-code/issues/34773)).

## Developer Pain Points

*   **Windows Stability:** Critical stability issues persist on Windows, ranging from Blue Screen of Death (BSOD) caused by filesystem operations ([#35710](https://github.com/anthropics/claude-code/pull/35710)) to screen flickering in the Desktop app ([#31990](https://github.com/anthropics/claude-code/issues/31990)).
*   **Usage Limit Opacity:** Max subscribers are confused and frustrated by hitting opaque usage limits instantly, indicating a discrepancy between expected quotas and actual enforcement ([#16157](https://github.com/anthropics/claude-code/issues/16157)).
*   **Context/Payload Management:** The tool struggles with large payloads, specifically failing to pre-check the cumulative size of PDFs or images before sending them to the API, resulting in "Request too large" errors that require session resets ([#26018](https://github.com/anthropics/claude-code/issues/26018), [#2939](https://github.com/anthropics/claude-code/issues/2939)).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest: 2026-03-19

## 1. Today's Highlights

The `openai/codex` repository is seeing significant activity focused on stabilizing the **v0.116.0-alpha** Rust release cycle, with three alpha versions pushed in the last 24 hours. Development focus is heavily skewed towards improving **remote execution capabilities** and hardening **security/sandboxing** features, particularly regarding MDM configuration and authorization workflows. The community remains vocal regarding resource management, specifically concerning **token usage spikes** and **macOS Intel support**.

## 2. Releases

*   **rust-v0.116.0-alpha.6 / 0.116.0-alpha.5 / 0.116.0-alpha.4**
    *   **Status:** Rapid iteration on the alpha channel.
    *   **Focus:** These releases appear to be part of a continuous integration effort, likely addressing stability issues and preparing for the upcoming stable v0.116.0 feature set.

## 3. Hot Issues

Here are the top 10 issues drawing significant community attention:

1.  **[#10450](https://github.com/openai/codex/issues/10450) - Remote Development in Codex Desktop App** 👍 386
    *   **Why it matters:** The top-voted request highlights a critical gap between the new Desktop App and traditional VS Code workflows.
    *   **Reaction:** Users are eager to use the Desktop App for SSH/Remote development but are currently blocked by the lack of support for remote workspaces compared to VS Code Remote extensions.

2.  **[#10410](https://github.com/openai/codex/issues/10410) - Codex Desktop App: macOS Intel (x86_64) support** 👍 185
    *   **Why it matters:** A segment of the developer community is still on Intel-based Macs and cannot use the Desktop App.
    *   **Reaction:** High frustration from users who feel abandoned by the Apple Silicon-only focus, requesting Universal binaries or x86_64 support.

3.  **[#14593](https://github.com/openai/codex/issues/14593) - Burning tokens very fast with VS Code extension** 👍 53
    *   **Why it matters:** Critical cost concern for Business/Pro users.
    *   **Reaction:** Users report that the latest extension updates (v26.311.21342) are depleting quotas significantly faster than expected,怀疑 (suspecting) inefficiencies in how context is being sent or cached.

4.  **[#12115](https://github.com/openai/codex/issues/12115) - Dynamically loading nested AGENTS.md** 👍 20
    *   **Why it matters:** Context management for large repositories.
    *   **Reaction:** Users want behavior similar to Claude Code, where nested config/agent files load on-demand rather than all at once, preventing confusion and token bloat.

5.  **[#5237](https://github.com/openai/codex/issues/5237) - Reads files outside working directory** (Closed)
    *   **Why it matters:** Security/Sandbox integrity.
    *   **Reaction:** Although closed, users remain wary of the sandbox's ability to access files outside the designated working directory without explicit permission.

6.  **[#14936](https://github.com/openai/codex/issues/14936) - "Don't ask again" ignored in CLI 0.115.0** (Closed)
    *   **Why it matters:** Developer workflow interruption.
    *   **Reaction:** A regression in v0.115.0 caused the CLI to prompt for approval on almost every command, ignoring previous preferences. This has been addressed in subsequent alphas.

7.  **[#14209](https://github.com/openai/codex/issues/14209) - Reconnecting issue worsening** 👍 16
    *   **Why it matters:** Service stability.
    *   **Reaction:** Reports from Europe indicate connection stability has degraded significantly in recent days, making the tool unreliable for continuous work.

8.  **[#14762](https://github.com/openai/codex/issues/14762) - Paid Usage Dropping too Quickly** 👍 19
    *   **Why it matters:** Billing transparency.
    *   **Reaction:** Users are alarmed at how quickly credits are being consumed, even for simple tasks or when the agent is idle (e.g., overnight).

9.  **[#12491](https://github.com/openai/codex/issues/12491) - MCP child processes not reaped (Memory Leak)** 👍 3
    *   **Why it matters:** System resource exhaustion.
    *   **Reaction:** A scary report of the GUI spawning 1300+ zombie processes and leaking 37GB of RAM due to MCP server handling.

10. **[#11981](https://github.com/openai/codex/issues/11981) - 100% CPU Usage** 👍 0
    *   **Why it matters:** Performance degradation.
    *   **Reaction:** Users with high-spec Macs are experiencing the app pinning the CPU even with minimal agent activity.

## 4. Key PR Progress

Active development is focused on the "remote execution" stack and sandbox hardening:

1.  **[#15069](https://github.com/openai/codex/pull/15069) - Add the exec-server end-to-end stack**
    *   **Description:** A major architectural addition. This PR introduces the `exec-server` crate and protocol, routing unified exec and filesystem tools through a dedicated server. It sets the foundation for robust remote development.

2.  **[#14853](https://github.com/openai/codex/pull/14853) & [#14847](https://github.com/openai/codex/pull/14847) - Wire remote app-server auth / Websocket auth**
    *   **Description:** Implementing secure authentication for remote app-server connections using websockets. This ensures that unauthenticated clients are rejected at the handshake stage.

3.  **[#15036](https://github.com/openai/codex/pull/15036) - Disable command_might_be_dangerous when unsandboxed**
    *   **Description:** A logic fix to ensure that if a user explicitly disables the sandbox, the "ApprovalPolicy::Never" (block dangerous commands) is also relaxed to allow necessary operations.

4.  **[#15067](https://github.com/openai/codex/pull/15067) - Protect first-time project .codex creation**
    *   **Description:** Updates protocol path protection to require explicit approval before writing a top-level `.codex` project config, closing a sandbox gap on macOS and Windows.

5.  **[#14970](https://github.com/openai/codex/pull/14970) - Simple directory mentions**
    *   **Description:** Adds support for mentioning directories in the TUI (with a trailing slash). This improves context management by allowing agents to target specific folders.

6.  **[#15020](https://github.com/openai/codex/pull/15020) - Harden plugin feature gating**
    *   **Description:** Improves the robustness of plugin management by skipping bad `marketplace.json` files rather than failing the entire list, and guarding plugin flows behind feature gates.

7.  **[#15056](https://github.com/openai/codex/pull/15056) - Add graph representation of agent network**
    *   **Description:** Introduces a graph structure for managing multi-agent interactions, specifically to handle "cascade close" (closing parent closes children) and "cascade resume."

8.  **[#15066](https://github.com/openai/codex/pull/15066) - Route remote project docs through executor**
    *   **Description:** Extends the remote execution stack to handle project documentation and repository skill discovery through the new executor-backed environment.

9.  **[#14818](https://github.com/openai/codex/pull/14818) - Handle invalid MDM config entries safely**
    *   **Description:** A critical fix for enterprise deployment. Previously, a single invalid MDM (Mobile Device Management) setting could prevent Codex from loading config entirely, causing fleet-wide outages. This makes the parser "fail-soft."

10. **[#15011](https://github.com/openai/codex/pull/15011) - Forward tool call task headers to MCP**
    *   **Description:** Improves observability and context handling by forwarding request-scoped task headers through MCP (Model Context Protocol) tool calls.

## 5. Feature Request Trends

Based on the activity, the community is clamoring for:

*   **Cross-Platform Parity:** There is a strong push to ensure the Desktop App matches the feature set of VS Code, specifically regarding **Remote Development/SSH** (Issue #10450) and **macOS Intel support** (Issue #10410).
*   **Advanced Context Control:** Developers want finer-grained control over how Codex ingests context. Specific requests include **nested `AGENTS.md` loading** (Issue #12115) and **Renaming Threads** (Issue #12564) to better manage history.
*   **Multi-Agent Orchestration:** Users are looking for better tools to manage parallel agents, such as **Git Worktrees support** (Issue #8570) and per-subagent model selection (Issue #14039).
*   **Visual Improvements:** Requests for **LaTeX rendering** (Issue #10715) to improve the readability of math-heavy documentation within the app.

## 6. Developer Pain Points

*   **Token Efficiency & Cost:** The most persistent complaint is the rapid depletion of tokens (Issues #14593, #14762). Users feel the tool is "burning" credits for background tasks or inefficient context management without clear transparency.
*   **Sandbox & Permission Fatigue:** While security is appreciated, the implementation is causing friction. Issues range from the "don't ask again" button being ignored (Issue #14936) to overzealous file blocking (Issue #12280) and zombie processes from MCP servers (Issue #12491).
*   **Platform Instability:** Users on Windows and Intel Macs feel like second-class citizens, facing specific regressions like the "Mouse Properties dialog" bug (Issue #9370) or lack of app support entirely.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest: 2026-03-19

## 1. Today's Highlights
The community is currently focused on a significant architectural push towards **Git Worktree support** to enable isolated, parallel development sessions. Concurrently, the maintainers are refining the **Agent Planning** experience, addressing bugs where agents drop context after plan approval or execute changes unexpectedly in read-only mode.

## 2. Releases
*   **v0.35.0-preview.1**
    *   **Customizable Shortcuts:** Introduced the ability to customize CLI keyboard shortcuts ([#21945](https://github.com/google-gemini/gemini-cli/pull/21945)).
    *   **Core Context Updates:** Improved `AgentLoopContext` threading through the core system ([#21944](https://github.com/google-gemini/gemini-cli/pull/21944)).
*   **v0.34.0**
    *   **Chat Resume:** Added a footer to facilitate resuming chats upon session quit ([#20667](https://github.com/google-gemini/gemini-cli/pull/20667)).
    *   **SVG Snapshots:** Added support for bold text and other styles in SVG snapshots ([#20937](https://github.com/google-gemini/gemini-cli/pull/20937)).

## 3. Hot Issues

*   **[Isolated Parallel Sessions via Git Worktrees](https://github.com/google-gemini/gemini-cli/issues/22945)**
    *   *Priority:* High. Users are requesting first-class support for Git worktrees to allow multitasking on different branches without conflicting working directories. The current manual setup is described as "cumbersome."
*   **[Agent "Ghosts" Context After Plan Approval](https://github.com/google-gemini/gemini-cli/issues/22266)**
    *   *Impact:* Critical workflow blocker. The agent successfully generates a plan, but upon approval, it silently drops the context and fails to execute the next step.
*   **[Agent Executes Changes in Plan Mode](https://github.com/google-gemini/gemini-cli/issues/22434)**
    *   *Status:* Possible Duplicate. Users report that despite being in "Plan Mode" (expected to be read-only), the agent is executing file modifications, causing unintended changes.
*   **[Subagent Recovery Misrepresented as Success](https://github.com/google-gemini/gemini-cli/issues/22323)**
    *   *Bug:* When a subagent hits `MAX_TURNS`, it reports a "GOAL success" status, masking the fact that the task was actually interrupted due to limits.
*   **[Browser Agent Fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**
    *   *Environment:* Linux/Wayland. The browser subagent is failing specifically on Wayland sessions, limiting functionality for Linux users.
*   **[CLI Scrolls to Top on Click (VS Code)](https://github.com/google-gemini/gemini-cli/issues/22028)**
    *   *UX Frustration:* Clicking anywhere in the terminal causes the view to jump to the top, severely disrupting readability during long agent outputs.
*   **[Automatic Update Failures](https://github.com/google-gemini/gemini-cli/issues/14423)**
    *   *Status:* Closed. Addressed issues where the auto-updater failed, requiring manual intervention.
*   **[Slow Response Times](https://github.com/google-gemini/gemini-cli/issues/22953)**
    *   *Performance:* A user reported latency of 1–1.5 hours for simple table structure suggestions, indicating potential backend or routing issues.
*   **[Add `/plan` Prompt Support](https://github.com/google-gemini/gemini-cli/issues/22855)**
    *   *Request:* Users want `/plan` to accept text arguments immediately (e.g., `/plan refactor X`) rather than entering a separate interactive state.
*   **[Memory Subagent Routing (Global vs. Project)](https://github.com/google-gemini/gemini-cli/issues/22819)**
    *   *Enhancement:* Discussion on how the memory subagent should distinguish and route preferences between global user settings (`~/.gemini/`) and project-specific settings (`.gemini/`).

## 4. Key PR Progress

*   **[feat(policy): map --yolo to allowedTools wildcard](https://github.com/google-gemini/gemini-cli/pull/22893)**
    *   Refactored the `--yolo` flag to map directly to a wildcard policy (`allowedTools: ["*"]`), removing the distinct `ApprovalMode.YOLO` state for cleaner policy handling.
*   **[fix(cli): consume Escape key in BaseSettingsDialog](https://github.com/google-gemini/gemini-cli/pull/22941)**
    *   Fixed a critical interaction bug where pressing `Escape` to close settings would inadvertently cancel the active agent turn.
*   **[feat(core): resilient subagent tool rejection](https://github.com/google-gemini/gemini-cli/pull/22951)**
    *   Improved subagent logic so that if a user denies a tool execution, the agent re-evaluates its strategy rather than immediately failing the task.
*   **[feat(core): implement strict macOS sandboxing](https://github.com/google-gemini/gemini-cli/pull/22832)**
    *   Implemented a strict default-deny sandbox for macOS using `Seatbelt`, enhancing security by explicitly allowing only necessary system accesses.
*   **[fix(sessionUtils): handle empty sessions and prevent residual data](https://github.com/google-gemini/gemini-cli/pull/22943)**
    *   Improved session management to ensure no data leaks between sessions when starting new ones or handling empty states.
*   **[fix(core): explicitly map execution context](https://github.com/google-gemini/gemini-cli/pull/22949)**
    *   Refactored `LocalAgentExecutor` to define execution context properties explicitly, preventing unintended property propagation and potential circular references.
*   **[feat(ui): add dynamic toggle for alternate buffer mode](https://github.com/google-gemini/gemini-cli/pull/22869)**
    *   Added a runtime toggle for "Alternate Buffer Mode," allowing users to switch between full-screen and inline terminal views without restarting.
*   **[fix(plan): sandbox path resolution in Plan Mode](https://github.com/google-gemini/gemini-cli/pull/22737)**
    *   Addressed LLM path hallucinations by restricting path resolution to the designated `plansDir` during plan mode.
*   **[feat: standardized Git Worktree skill](https://github.com/google-gemini/gemini-cli/pull/22218)**
    *   Introduced a standardized skill for managing Git worktrees and enforcing a "Base Folder Strategy," facilitating better multi-tasking workflows.
*   **[fix(ui): add space between distinct thought subjects](https://github.com/google-gemini/gemini-cli/pull/22828)**
    *   UX improvement adding vertical spacing between distinct thought blocks in subagent outputs to improve readability.

## 5. Feature Request Trends

*   **Workflow Isolation:** There is a strong demand for features that support parallel workflows, specifically through **Git Worktree integration** and dedicated slash commands to switch contexts mid-session.
*   **Memory & Personalization:** Users are requesting robust **long-term memory** capabilities, specifically asking for the agent to proactively remember and apply user preferences (e.g., "I prefer tabs over spaces") across sessions.
*   **Planning Mode:** Users want stricter adherence to read-only behavior in Plan Mode and the ability to pass arguments directly to the `/plan` command.

## 6. Developer Pain Points

*   **Agent Reliability:** Developers are experiencing "Ghosting," where agents stop responding or drop context immediately after a user approves a plan. Additionally, subagents are reporting "Success" when they actually failed due to timeouts or turn limits.
*   **UI/UX Glitches:** There are persistent reports of the UI scrolling to the top uncontrollably on click (VS Code) and issues with the browser agent crashing on Linux (Wayland).
*   **Unsafe Agent Behavior:** Reports of agents using unsafe commands (like `git reset --force`) without warning or attempting to execute destructive actions during read-only `Plan Mode` are causing concern.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest: 2026-03-19

## 1. Today's Highlights
The release of **v1.0.8-0** brings significant enhancements to extensibility, introducing extension mode settings and allowing MCP server validation via the `MCP_ALLOWLIST` flag. Meanwhile, the community is actively troubleshooting stability issues in v1.0.7, with particular attention paid to terminal scrolling behavior in Tmux/SSH environments and new TypeScript runtime crashes during parallel agent execution.

## 2. Releases
### v1.0.8-0 & v1.0.7 (2026-03-17 / 2026-03-19)
*   **MCP & Extensibility:** v1.0.8-0 adds an "extension mode" setting and enables MCP server validation against configured registries via the `MCP_ALLOWLIST` experimental flag.
*   **Configuration:** Support for defining hooks in `settings.json` and `settings.local.js` has been added.
*   **Usability:** `--resume` now accepts task IDs in addition to session IDs.
*   **UI/UX:** v1.0.7 improved color contrast for accessibility and introduced visual differentiation for user messages.
*   **Model Support:** Added support for the `gpt-5.4-mini` model.

## 3. Hot Issues
**Top Community Concerns:**

1.  **[Terminal Flickering & Scrolling Chaos](https://github.com/github/copilot-cli/issues/1584)** (👍 16)
    The "Incessant Scrolling" issue is the most upvoted bug recently, with users reporting that the terminal viewport jumps wildly during long operations. A related [issue](https://github.com/github/copilot-cli/issues/1811) (👍 11) reports similar flickering within Visual Studio's integrated terminal.
2.  **[Authorization Errors](https://github.com/github/copilot-cli/issues/1897)**
    Users with Copilot Pro are reporting "You are not authorized" errors, suggesting potential glitches in policy enforcement or authentication token validation.
3.  **[React Hooks Error in v1.0.6](https://github.com/github/copilot-cli/issues/2117)**
    A critical bug causing `Rendered more hooks than during the previous render` has appeared, leading to CLI crashes.
4.  **[Linux Clipboard Broken](https://github.com/github/copilot-cli/issues/2082)**
    The standard `Ctrl+Shift+C` shortcut for copying text fails on Ubuntu 24.04, breaking workflow for Linux users.
5.  **[Nix/direnv Deadlocks](https://github.com/github/copilot-cli/issues/1838)** (👍 5)
    The CLI hangs indefinitely when launched in Nix flake environments due to subprocess I/O deadlocks.
6.  **[Tmux Scrolling Issues](https://github.com/github/copilot-cli/issues/1842)**
    Users cannot scroll through Copilot's responses in Tmux, making long outputs unreadable.
7.  **[Model Availability Errors](https://github.com/github/copilot-cli/issues/2099)**
    Agents configured to use "Claude Sonnet 4.5" or "4.6" are failing with "not available" warnings and falling back to defaults.
8.  **[API Transient Errors & Rate Limiting](https://github.com/github/copilot-cli/issues/2101)**
    Reports of "Request failed due to a transient API error" are increasing, often leading to rate limit warnings.
9.  **[OOM Crashes in Parallel Sessions](https://github.com/github/copilot-cli/issues/2132)**
    Running parallel background agents is causing abrupt crashes due to memory/runtime errors in long sessions.
10. **[Missing Mode Colors](https://github.com/github/copilot-cli/issues/2124)**
    Visual indicators for Plan/Autopilot modes have lost their distinct color coding, making it difficult to distinguish modes.

## 4. Key PR Progress
*Note: Only one PR was updated in the last 24h.*

1.  **[Create blank.yml #1850](https://github.com/github/copilot-cli/pull/1850)**
    A straightforward pull request to add a `blank.yml` file, likely related to workflow templates or scaffolding configurations.

## 5. Feature Request Trends
Based on community issue activity:
*   **Kitty Graphics Protocol:** Users want to render images (specifically SVGs) directly in the CLI using the [Kitty Graphics Protocol](https://github.com/github/copilot-cli/issues/557).
*   **User-Level Hooks:** There is a strong demand (👍 21) for defining hooks at the user level, rather than just project-level, to automate tasks across different projects ([#1067](https://github.com/github/copilot-cli/issues/1067)).
*   **Custom Terminal Titles:** Users want more granular control over terminal titles during status updates without losing the ability to see custom titles ([#1211](https://github.com/github/copilot-cli/issues/1211)).
*   **Scheduled Prompts:** Requests for "recurring" or "scheduled" prompts suggest a desire for background agent tasks that run automatically ([#2056](https://github.com/github/copilot-cli/issues/2056)).

## 6. Developer Pain Points
*   **UI Instability in Tmux/SSH:** The rendering engine continues to struggle with multiplexers (Tmux) and remote sessions (SSH), causing flickering, loss of color coding, and scrolling bugs.
*   **Environment Compatibility:** Developers using non-standard environments (Nix, direnv) are facing blocking hangs and I/O deadlocks.
*   **Subagent Limitations:** Users are frustrated that custom skills defined in `.github/skill` are not accessible to subagents spawned by the main agent ([#839](https://github.com/github/copilot-cli/issues/839)).
*   **Authentication Fatigue:** Frequent requests to re-login and "not authorized" errors are disrupting workflows, even for Pro users.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest: 2026-03-19

## 1. Today's Highlights
Version **1.24.0** has been released, introducing significant improvements to Plan Mode workflow—specifically allowing `StrReplaceFile` edits without approval and enabling multi-option plan selection. Concurrently, the community is actively discussing performance and stability issues, with critical fixes applied to Windows startup speeds and the unified prompt router.

## 2. Releases
**v1.24.0 (2026-03-18)**
This release focuses on enhancing the "Plan Mode" experience and refactoring core input handling.
*   **Plan Mode Flexibility:** The AI can now edit plan files using `StrReplaceFile` without triggering repeated approval prompts.
*   **Multi-Option Planning:** The `ExitPlanMode` function now supports presenting multiple execution paths to the user, rather than a simple binary approve/reject choice.
*   **Input Handling:** A refactor of the prompt router to ensure user input is preserved during agent runs and state changes.

## 3. Hot Issues
*   [#1442](https://github.com/MoonshotAI/kimi-cli/issues/1442) **[Invoicing UI]**
    Users are asking where to find the invoicing interface within the CLI tool, indicating a gap in billing/management features.
*   [#1296](https://github.com/MoonshotAI/kimi-cli/issues/1296) **[MCP Disconnections]**
    Reports of intermittent errors when MCP (Model Context Protocol) servers disconnect. Users are experiencing instability during long-running tasks.
*   [#1489](https://github.com/MoonshotAI/kimi-cli/issues/1489) **[Input Aggression]**
    Community feedback (Closed) highlighted that the CLI's auto-collapse feature for pasted text was too aggressive, hindering voice and typeless input workflows.
*   [#1493](https://github.com/MoonshotAI/kimi-cli/issues/1493) **[UI Feedback]**
    Developers reported that the CLI animation stops rotating during execution, causing confusion about whether the process is stuck or simply running.
*   [#1495](https://github.com/MoonshotAI/kimi-cli/issues/1495) **[Configuration]**
    A request to allow users to configure the save directory for plans generated in Plan Mode via `config.toml`.
*   [#1343](https://github.com/MoonshotAI/kimi-cli/issues/1343) **[Windows Performance]**
    Significant community concern regarding slow startup times on Windows when installed via `uv tool install`, attributed to encoding and `loguru` imports (Closed).
*   [#1487](https://github.com/MoonshotAI/kimi-cli/issues/1487) **[HTTPS MCP]**
    Users are requesting that the MCP client include a default `User-Agent` header for better compatibility.
*   [#1492](https://github.com/MoonshotAI/kimi-cli/issues/1492) **[UX Customization]**
    Developers want the ability to configure or disable the truncation of shell commands in the output display.

## 4. Key PR Progress
*   [#1496](https://github.com/MoonshotAI/kimi-cli/pull/1496) **[Release]**
    Bumped version to 1.24.0 and synchronized changelogs.
*   [#1490](https://github.com/MoonshotAI/kimi-cli/pull/1490) **[Plan Mode]**
    Allowed `StrReplaceFile` to edit plan files in plan mode, streamlining the editing workflow.
*   [#1494](https://github.com/MoonshotAI/kimi-cli/pull/1494) **[Plan Mode]**
    Implemented support for multi-option selection in `ExitPlanMode`, allowing users to choose between different AI-generated strategies.
*   [#1491](https://github.com/MoonshotAI/kimi-cli/pull/1491) **[Core Refactor]**
    Unified the prompt router architecture to maintain persistent input during agent runs, improving the reliability of user interruptions.
*   [#1488](https://github.com/MoonshotAI/kimi-cli/pull/1488) **[UI Fix]**
    Addressed community complaints by raising the pasted text collapse threshold (to 15 lines/1000 chars).
*   [#1486](https://github.com/MoonshotAI/kimi-cli/pull/1486) **[Performance]**
    Streamlined startup paths and optimized logger/metadata loading to fix the slow startup issue reported in #1343.
*   [#1495](https://github.com/MoonshotAI/kimi-cli/issues/1495) **[Feature Request]**
    *Note: Discussion only.* Proposal to add `[paths] plans_dir` configuration.
*   [#884](https://github.com/MoonshotAI/kimi-cli/pull/884) **[Dependencies]**
    Automated dependency bump for `ruff` from 0.14.14 to 0.15.0.
*   [#1485](https://github.com/MoonshotAI/kimi-cli/pull/1485) **[Maintenance]**
    Fixed test failures and lint errors related to the new token usage stats feature.

## 5. Feature Request Trends
*   **Configurability:** Users are demanding more control over the CLI environment, specifically requesting configuration options for file paths (where plans are saved) and UI behavior (command collapsing).
*   **Plan Mode Enhancement:** There is a clear trend toward making Plan Mode more robust, specifically in how plans are edited, saved, and approved (multi-option selection).

## 6. Developer Pain Points
*   **Performance on Windows:** A specific segment of the user base is struggling with slow startup times caused by Python imports and logger initialization on Windows.
*   **UI/UX Feedback:** Developers are frustrated with the lack of visual feedback regarding system status (animations freezing) and aggressive text truncation, which makes reviewing pasted code difficult.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: 2026-03-19

## 1. Today's Highlights
Today's digest highlights significant concerns regarding the OpenCode **Snapshot system**, with multiple reports of severe performance degradation and disk space leakage (filling at ~9.5GB/hour). Additionally, community discussion is heating up around architectural proposals for a **Multi-Session Daemon** with tab support and the integration of **MCP server** capabilities. On the model provider front, contributors are actively adding support for new providers like **GitLab Agent Platform** and refining authentication flows for GitHub Enterprise.

## 2. Releases
**No new releases** in the last 24 hours.

## 3. Hot Issues
*   **[#14811 Snapshot system leaks tmp_pack_* files indefinitely](https://github.com/anomalyco/opencode/issues/14811)** (👍 1)
    *   **Why it matters:** Critical performance bug. The snapshot system is allegedly filling user disks at a rate of ~9.5 GB per hour due to uncleaned temporary pack files.
*   **[#4283 Copy To Clipboard is not working](https://github.com/anomalyco/opencode/issues/4283)** (👍 55)
    *   **Why it matters:** High-impact UX frustration. Users cannot copy text from the TUI response window. This issue has garnered the highest reaction count in the last 24 hours.
*   **[#3936 Github Enterprise authorization](https://github.com/anomalyco/opencode/issues/3936)** (👍 15)
    *   **Why it matters:** Enterprise blocker. Users cannot log in via GitHub Enterprise due to unexpected errors during the authentication flow.
*   **[#296 Opencode as MCP server](https://github.com/anomalyco/opencode/issues/296)** (👍 17)
    *   **Why it matters:** Strategic feature request. The community is asking for OpenCode to run as an MCP (Model Context Protocol) server to enable powerful agent workflows, similar to Claude Code.
*   **[#4340 [FEATURE]: Add Windows arm64 support](https://github.com/anomalyco/opencode/issues/4340)** (👍 23)
    *   **Why it matters:** Platform support. While officially closed, discussion persists regarding full support for Windows 11 on arm64 architecture.
*   **[#16331 Permissions ignored](https://github.com/anomalyco/opencode/issues/16331)**
    *   **Why it matters:** Security/Configuration. Users report that `opencode.json` permission settings (specifically deny rules) are being ignored, allowing access to restricted files like `.env`.
*   **[#18088 The Chinese, Japanese, and Korean text that has been answered will be hidden](https://github.com/anomalyco/opencode/issues/18088)**
    *   **Why it matters:** Localization regression. A rendering bug causes CJK characters to disappear when pop-ups occur in the interface.
*   **[#18108 Truncated tool calls are misclassified and unrecoverable](https://github.com/anomalyco/opencode/issues/18108)**
    *   **Why it matters:** LLM Reliability. When a model hits token limits during a tool call, OpenCode reportedly enters a "doom loop" instead of handling the truncation gracefully.
*   **[#7048 Copy Text "Copied to clipboard" does never work](https://github.com/anomalyco/opencode/issues/7048)**
    *   **Why it matters:** Recurring UX issue. Similar to #4283, specifically affecting users on Ubuntu/GhostTTY where the copy command appears to succeed but fails.
*   **[#18072 Snapshot git add runs indefinitely on worktrees with large non-code files](https://github.com/anomalyco/opencode/issues/18072)** (👍 1)
    *   **Why it matters:** Workflow halt. The snapshot system hangs indefinitely trying to index large non-code files (datasets/models) in git worktrees.

## 4. Key PR Progress
*   **[#17984 feat: multi-session daemon with tabs](https://github.com/anomalyco/opencode/pull/17984)**
    *   Draft PR proposing a major architectural shift to a daemon-based system to support multiple concurrent sessions via tabs.
*   **[#18014 feat: enable GitLab Agent Platform with workflow model discovery](https://github.com/anomalyco/opencode/pull/18014)**
    *   Adds full support for the GitLab Agent Platform, including dynamic model discovery workflows.
*   **[#18110 feat: auto discover models from custom providers](https://github.com/anomalyco/opencode/pull/18110)**
    *   Introduces a `discover` field for provider configurations to auto-fetch models via the `/v1/models` endpoint.
*   **[#18093 refactor(effect): unify service namespaces and align naming](https://github.com/anomalyco/opencode/pull/18093)**
    *   A significant internal refactor following the `EFFECT_MIGRATION_PLAN`, unifying service namespaces to simplify the codebase.
*   **[#18105 feat(app): sidebar improvements](https://github.com/anomalyco/opencode/pull/18105)**
    *   Quality-of-life update for the app sidebar: introduces pinned sessions, double-click to rename, and hover fixes.
*   **[#18103 feat: integrate multistep auth flows into desktop app](https://github.com/anomalyco/opencode/pull/18103)**
    *   Companion PR to #18035, bringing complex multi-step authentication flows (required by some providers) into the desktop app.
*   **[#18097 feat(codex): add GPT-5.4 mini and nano support](https://github.com/anomalyco/opencode/pull/18097)**
    *   Updates the Codex OAuth allowlist to support the newest GPT-5.4 Mini and Nano models.
*   **[#4604 feat(formater): restrict formatting to only the changed range](https://github.com/anomalyco/opencode/pull/4604)**
    *   Improves the Edit tool for clang-format to only reformat the specific lines changed, preventing unrelated formatting noise in diffs.
*   **[#13719 fix: render permission and question prompts from nested subagent session](https://github.com/anomalyco/opencode/pull/13719)**
    *   Fixes a bug where permission prompts from nested (grandchild+) subagent sessions would silently hang the TUI.
*   **[#17276 feat(cli): add --json and --json-schema flags](https://github.com/anomalyco/opencode/pull/17276)**
    *   Extends the `opencode run` CLI with `--json` and `--json-schema` flags for better structured output handling.

## 5. Feature Request Trends
*   **Cross-Device Sync & Configuration:** Users are increasingly asking for seamless ways to sync `opencode.json` and session history across machines, with community members proposing Git-based syncing scripts.
*   **MCP Server Mode:** There is a strong push for OpenCode to function not just as a client, but as a server (via MCP) to other AI agents.
*   **Tabbed/Daemon Interface:** The draft PR for a multi-session daemon reflects a growing desire to manage multiple OpenCode sessions simultaneously without restarting the process.
*   **Advanced Model Support:** Requests continue to pour in for diverse model integrations, specifically mentioning OpenAI-compatible endpoints (DeepSeek, Kimi) and the latest GPT-5.4 variants.

## 6. Developer Pain Points
*   **Snapshot System Instability:** The snapshot/git integration is currently a major source of friction, cited for causing file leaks, indefinite hangs on large files, and ignored timeout settings.
*   **Clipboard Reliability:** Copy-paste functionality remains broken across different environments (Windows SSH, Ghostty, Ubuntu), suggesting a systemic issue with how OpenCode interacts with the system clipboard.
*   **Windows Path Handling:** Despite recent fixes, path normalization issues (e.g., drive letter casing, slash directions) continue to break session visibility and configuration on Windows.
*   **Token Limit & Timeout Management:** Developers are frustrated by "Context Overflow" errors where `compaction.auto: false` settings are ignored, and hard 5-minute timeouts in the Node.js SDK that cannot be adjusted.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest: 2026-03-19

## 1. Today's Highlights
The Qwen Code project is accelerating towards the **v0.13.0** milestone, marked by the release of `v0.12.5-preview.0` and a flurry of merged Pull Requests. The development team is aggressively addressing stability concerns, specifically fixing critical context compression errors (`/compress`), Windows file URI handling, and tool output truncation. Concurrently, significant strides are being made in UI/UX improvements—such as real-time token usage indicators and fuzzy search for file completions—while the community intensifies requests for advanced features like an "Agent Arena" for competitive model execution.

## 2. Releases
*   **[v0.12.5-preview.0](https://github.com/QwenLM/qwen-code/compare/v0.12.6...v0.12.5-preview.0) & Nightly (v0.12.6-nightly)**
    *   **Status:** Pre-release snapshots for the upcoming v0.13.0 cycle.
    *   **TypeScript SDK v0.1.6:** Includes a backfilled release for NPM (version 0.1.5) and bundles the latest CLI source.
    *   **Focus:** These releases bridge the gap between the current stable version and the imminent feature-rich 0.13.0 update, likely containing the fixes for the critical "edit failed" and context overflow bugs reported in the last 24 hours.

## 3. Hot Issues
Here are the top community concerns discussed in the last day:

1.  **[#2460](https://github.com/QwenLM/qwen-code/issues/2460) - Critical "Edit Failed" Regression**
    *   **Issue:** Users report severe, frequent failures in the editing functionality, where the agent claims it cannot find the text to edit ("0 occurrences found"), often damaging code files.
    *   **Impact:** High severity; described as "almost unusable" and "destroying projects."
    *   **Reaction:** 8 comments; urgent request for a rollback to v0.12.2.

2.  **[#2382](https://github.com/QwenLM/qwen-code/issues/2382) - VS Code Extension Broken**
    *   **Issue:** The VS Code companion extension stops working ("Preparing Qwen Code...") starting from v0.12.3.
    *   **Impact:** Affects core IDE integration workflows.
    *   **Reaction:** 8 comments; users forced to downgrade VS Code versions to no avail.

3.  **[#2426](https://github.com/QwenLM/qwen-code/issues/2426) - Free Tier Quota Reduction**
    *   **Issue:** Users believe the daily free request limit has been silently cut from ~1000 to <300.
    *   **Impact:** Affects accessibility for casual developers and testing.
    *   **Reaction:** 4 comments; strong sentiment that "Qwen can't afford this?"

4.  **[#1873](https://github.com/QwenLM/qwen-code/issues/1873) - LSP Configuration Ignored**
    *   **Issue:** The experimental LSP support fails to respect `.lsp.json` configurations, resulting in "No document symbols found" for valid C/C++ files.
    *   **Impact:** Breaks deep codebase understanding for C/C++ projects.
    *   **Reaction:** 5 comments; long-standing issue still awaiting a triage.

5.  **[#2447](https://github.com/QwenLM/qwen-code/issues/2447) - Skill Testing Framework**
    *   **Issue:** Community request for a formal testing framework (Record/Playback/Assertions) for the growing library of Skills.
    *   **Impact:** Maintains quality as the ecosystem scales.
    *   **Reaction:** 3 comments; strong technical support for the proposal.

6.  **[#2465](https://github.com/QwenLM/qwen-code/issues/2465) - MiniMax-M2.5 Config Error**
    *   **Issue:** The official Alibaba Coding Plan documentation generates a wrong configuration for `MiniMax-M2.5`.
    *   **Impact:** Blocks users trying to connect specific models via the official guide.
    *   **Reaction:** New issue; needs documentation fix.

7.  **[#2306](https://github.com/QwenLM/qwen-code/issues/2306) - Crash on "Always Allow"**
    *   **Issue:** CLI crashes when the user selects "Always allow" for command execution permissions.
    *   **Impact:** Major disruption to automated workflows.
    *   **Reaction:** 4 comments; regression introduced post-v0.11.1.

8.  **[#2456](https://github.com/QwenLM/qwen-code/issues/2456) - Language Mixing & Spacing Bugs**
    *   **Issue:** Qwen 3.5 Plus model adds extra spaces in mixed English/Chinese output, breaking shell commands.
    *   **Impact:** Generated code becomes non-executable (e.g., `cat git 手册` vs `cat "git 手册"`).
    *   **Reaction:** User frustration with model reliability.

9.  **[#2454](https://github.com/QwenLM/qwen-code/issues/2454) - Settings.json Overwrite**
    *   **Issue:** Using the `/model` CLI command silently deletes manually added models from `settings.json`.
    *   **Impact:** Prevents advanced configuration customization.
    *   **Reaction:** New bug report.

10. **[#2409](https://github.com/QwenLM/qwen-code/issues/2409) - Feature Parity with Claude Code**
    *   **Issue:** Analysis that Qwen Code's subagent system lags behind Claude Code (implementing only ~40-45% of features).
    *   **Impact:** Sets the roadmap for competitive development.
    *   **Reaction:** 3 comments; community eager for "Agent Arena" features.

## 4. Key PR Progress
*   **[#2445](https://github.com/QwenLM/qwen-code/pull/2445) - Real-time Token Usage (Merged)**
    *   Adds a visual display of output token counts in the loading spinner and status line, addressing user requests for better context visibility.
*   **[#2437](https://github.com/QwenLM/qwen-code/pull/2437) - Fuzzy File Search (Merged)**
    *   Refactors the VS Code file completion system to use backend fuzzy search (replacing client-side substring matching), vastly improving search quality in large projects.
*   **[#1835](https://github.com/QwenLM/qwen-code/pull/1835) - `/context` Command (Merged)**
    *   Introduces a slash command to break down context window usage, helping developers understand where their token limit is going.
*   **[#2464](https://github.com/QwenLM/qwen-code/pull/2464) - Fix `/compress` Reliability (Merged)**
    *   Addresses the "Internal error" reported in [#2459](https://github.com/QwenLM/qwen-code/issues/2459), ensuring compression resets failed flags and handles context limits gracefully.
*   **[#2457](https://github.com/QwenLM/qwen-code/pull/2457) - Windows URI Handling Fix (Merged)**
    *   Fixes the DiffManager to properly handle `C:\...` paths on Windows using `vscode.Uri.file()`, resolving "file not found" errors.
*   **[#2440](https://github.com/QwenLM/qwen-code/pull/2440) - `qwen auth` CLI Command (Merged)**
    *   Introduces a dedicated command for configuring authentication (OAuth/Alibaba Coding Plan), streamlining the setup process.
*   **[#2434](https://github.com/QwenLM/qwen-code/pull/2434) - Concurrent Task Execution (Merged)**
    *   Improves performance by allowing task tools (sub-agents) to run concurrently, as they share no mutable state.
*   **[#2446](https://github.com/QwenLM/qwen-code/pull/2446) - MCP Truncation Support (Merged)**
    *   Adds truncation for MCP tool outputs to prevent context window overflow, matching the logic used for built-in tools like `grep` or `shell`.
*   **[#2463](https://github.com/QwenLM/qwen-code/pull/2463) - Markdown Table Escaping (Open)**
    *   A hotfix to address the issue where `|` characters in table cells break the markdown rendering (related to Issue #2461).
*   **[#1912](https://github.com/QwenLM/qwen-code/pull/1912) - Agent Arena (Merged)**
    *   Adds the "Agent Collaboration Arena" feature, allowing multiple models to execute a task in parallel using Git worktrees, enabling result comparison.

## 5. Feature Request Trends
Based on the issues and PRs, the community is pushing for three main themes:
1.  **Competitive Testing (Agent Arena):** Users want to pit different models against the same task to see who performs best without leaving the editor. (PR #1912 addresses this).
2.  **Observability:** There is a clear demand for metrics. Users want to see real-time token counts (delivered in PR #2445) and detailed context breakdowns (delivered in PR #1835) directly in the UI.
3.  **Cross-Directory Skill Support:** Requests to load skills from non-Qwen directories (e.g., `.cursor`, `.claude`) are gaining traction (PR #2202), suggesting users want a unified agent layer across different AI tools.

## 6. Developer Pain Points
*   **Reliability Anxiety:** The recent surge in "edit failed" and "crash" reports (v0.12.3+) has shaken confidence. Developers are hesitant to upgrade or use the tool on critical codebases without manual backups.
*   **Configuration Fragility:** Issues like the `/model` command wiping manual settings (#2454) and `.lsp.json` being ignored (#1873) suggest the configuration system is struggling to manage complexity.
*   **Context Management:** While `/compress` exists, it fails silently or causes internal errors at the worst moments (when the context is 100% full), leaving users with no recovery option other than restarting the session.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*