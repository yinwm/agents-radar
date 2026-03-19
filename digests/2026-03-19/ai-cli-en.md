# AI CLI Tools Community Digest 2026-03-19

> Generated: 2026-03-19 01:23 UTC | Tools covered: 7

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

# AI CLI Tools Ecosystem Report: 2026-03-19

## 1. Ecosystem Overview
The AI CLI ecosystem is currently undergoing a pivotal architectural shift, moving from single-agent interfaces to robust, multi-agent orchestration platforms. While **Claude Code** leads in ecosystem extensibility through a rapidly maturing plugin architecture, **OpenAI Codex** and **Qwen Code** are focusing on underlying infrastructure stability, specifically regarding remote execution environments and context window management. A critical wave of stability issues—ranging from Windows filesystem crashes (Claude Code) to session context loss (Gemini/Qwen)—suggests that tools are struggling to balance aggressive feature iteration with reliability. Simultaneously, "Plan Mode" workflows have emerged as a standard UI paradigm, with Kimi, Gemini, and GitHub Copilot all releasing features to formalize agent planning before execution.

## 2. Activity Comparison

| Tool | Issue Activity | PR Velocity | Release Status | Stability Trend |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **High** (10 Critical/Hot Issues) | **High** (10 Major PRs) | **Active** (v2.1.79) | **Regressing** (Scroll/Login bugs) |
| **OpenAI Codex** | **High** (Memory/Network issues) | **Medium** (Architectural refactor) | **Alpha** (Rust v0.116.0-x) | **Stable** (Backend focus) |
| **Gemini CLI** | **Medium** (Context "Ghosting") | **High** (Memory subsystem) | **Nightly** (v0.36.0) | **Improving** (Context fixes) |
| **GitHub Copilot** | **Medium** (UX/Extensibility) | **Low** (1 PR updated) | **Stable** (v1.0.8) | **Mixed** (UI regressions) |
| **Kimi Code** | **Low** (Resolved) | **High** (Windows/Plan mode) | **Stable** (v1.24.0) | **Improving** (Perf gains) |
| **OpenCode** | **Medium** (Windows/Sync) | **Medium** (Desktop Git) | **Gap** (No release) | **Vulnerable** (Runtime crashes) |
| **Qwen Code** | **High** (Edit failures) | **High** (Concurrency) | **Blocked** (Pipeline fail) | **Regressing** (Critical bugs) |

## 3. Shared Feature Directions
*   **Agent "Plan Mode" Workflows:**
    *   **Claude Code & GitHub Copilot:** Integrating approval loops for read-only planning vs. execution.
    *   **Kimi Code:** Enhanced `ExitPlanMode` to support multi-option selection (v1.24.0).
    *   **Gemini CLI:** Addressing critical bugs where "Plan Mode" unexpectedly executes changes.
*   **Multi-Agent Orchestration & Context:**
    *   **Qwen Code & OpenAI Codex:** Pushing parallel execution frameworks (`exec-server` for Codex, concurrent task tools for Qwen).
    *   **Gemini CLI:** Developing a "Memory Manager" agent to handle long-term context and sub-agent injection.
*   **Remote Development & SSH:**
    *   **OpenAI Codex:** Top-voted request (389👍) for SSH support in Desktop App.
    *   **Claude Code:** High demand for parity between CLI and VS Code extension features (e.g., `/rc`).
*   **Observability & Cost Monitoring:**
    *   **Claude Code & Qwen Code:** Users demanding real-time token stats and quota visibility in the `statusLine` (Claude) or progress spinners (Qwen).
*   **Plugin & Extensibility Standards:**
    *   **Claude Code:** Community-driven plugins (Model Router, Tool Mutex) filling core gaps.
    *   **GitHub Copilot:** standardizing hooks in `settings.json` and MCP integration.

## 4. Differentiation Analysis
*   **Claude Code (The Ecosystem Player):** Focuses on being the "OS for AI development" via plugins. Its community is actively building infrastructure (e.g., tool-mutex to fix Windows BSODs) that the core team hasn't shipped yet. Target user: Technical users willing to tweak configurations.
*   **OpenAI Codex (The Architect):** investing heavily in backend infrastructure (`exec-server`) to separate execution from the client. Target user: Enterprise teams needing remote isolation and sandbox security.
*   **Kimi Code (The Productivity Polisher):** Focused on UX refinements (input persistence, pasted text handling) and Windows performance. Target user: Developers valuing speed and "snappy" terminal interactions.
*   **GitHub Copilot (The Integrator):** Focused on deep IDE parity and standardized hooks. Target user: Users already locked into the GitHub ecosystem wanting seamless extensions.
*   **Qwen Code (The Feature Racer):** iterating fast on features (concurrency, fuzzy search) but suffering from "feature creep" instability (edit failures, regression anxiety).

## 5. Community Momentum & Maturity
*   **Most Mature:** **Claude Code** and **GitHub Copilot**. Both have established release cadences and distinct communities (Plugin ecosystem for Claude, Extension marketplace for Copilot).
*   **Highest Iteration Speed:** **Kimi Code** and **Qwen Code**. Both are shipping features daily, though Qwen is currently paying the "stability tax" with pipeline failures and critical regressions.
*   **Momentum Shifts:**
    *   **Claude Code** is seeing the strongest "community-led" development, with plugins effectively acting as a distributed dev team.
    *   **OpenAI Codex** is in a "quiet period" of heavy refactoring (Rust/Exec-Server), which usually precedes a major feature release.
*   **At Risk:** **OpenCode** and **Qwen Code**. OpenCode is facing significant runtime stability issues (Bun on Windows), while Qwen is struggling with a broken release pipeline (v0.13.0 failed).

## 6. Trend Signals
1.  **The "Plan-First" Mandate:** The uniform adoption of "Plan Modes" across Kimi, Gemini, and Copilot signals a developer requirement for *determinism*. Users no longer want "auto-pilot"; they want "co-pilot" that explicitly proposes changes before executing them to prevent "spaghetti code" generation.
2.  **Platform Wars (Windows/Linux):** There is a clear trend of instability on non-macOS platforms. **Claude Code** (Windows BSOD), **OpenCode** (Bun crashes), and **Kimi Code** (slow startups) all show that AI tooling is heavily optimized for Apple Silicon, leaving Windows/Linux enterprise users as second-class citizens.
3.  **Context Fragility is the Ceiling:** Almost every digest (Qwen's "Edit Failed", Gemini's "Ghosting", OpenCode's "SSE Timeout") highlights that **context management**—reliably preserving state and files during long agent runs—is the single biggest technical hurdle preventing full autonomy.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Analysis Period:** Data as of 2026-03-19 | Repository: `anthropics/skills`

---

## 1. Top Skills Ranking
Based on the most active Pull Requests, the community is heavily focused on **document quality**, **system integrity**, and **infrastructure standards**.

*   **[#514: document-typography](https://github.com/anthropics/skills/pull/514)** (Open)
    *   **Functionality:** Enforces typographic quality control, fixing orphaned words, widow paragraphs, and numbering misalignment in AI-generated documents.
    *   **Discussion:** Addresses a universal pain point ("affects every document Claude generates") where visual polish is often overlooked by LLMs.
    *   **Status:** Open; high relevance for document-heavy workflows.

*   **[#83: skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** (Open)
    *   **Functionality:** Meta-skills that audit other skills for structure, documentation, resource management, and security risks.
    *   **Discussion:** Represents a maturation of the ecosystem; the community is building tools to police and maintain quality standards.
    *   **Status:** Open; proposed addition to the `example-skills` marketplace.

*   **[#210: frontend-design improvement](https://github.com/anthropics/skills/pull/210)** (Open)
    *   **Functionality:** Refines the `frontend-design` skill to ensure instructions are actionable, coherent, and executable within a single conversation context.
    *   **Discussion:** Focuses on "token efficiency" and steering Claude behavior more effectively during UI/UX tasks.
    *   **Status:** Open; targets workflow optimization.

*   **[#95: Comprehensive system documentation](https://github.com/anthropics/skills/pull/95)** (Open)
    *   **Functionality:** Adds detailed architectural flowcharts and evidence management system documentation (`SYSTEM_OVERVIEW.md`, `ARCHITECTURE.md`).
    *   **Discussion:** Highlights a demand for better internal documentation standards within complex skill implementations.
    *   **Status:** Open.

*   **[#509: Add CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509)** (Open)
    *   **Functionality:** Formalizes contribution guidelines to improve the repository's community health score (currently 25%).
    *   **Discussion:** Directly addresses Issue #452; recognized as the "most impactful single addition" for onboarding new contributors.
    *   **Status:** Open.

*   **[#181: SAP-RPT-1-OSS predictor](https://github.com/anthropics/skills/pull/181)** (Open)
    *   **Functionality:** Integrates SAP's open-source tabular foundation model for predictive analytics on business data.
    *   **Discussion:** Signals strong interest in connecting Claude Code with enterprise-grade data models and business intelligence.
    *   **Status:** Open.

---

## 2. Community Demand Trends
Analysis of open Issues reveals three primary pillars of demand:

**A. Ecosystem Hygiene & Security**
*   **Trust Boundaries:** Users are concerned about skill impersonation ([#492](https://github.com/anthropics/skills/issues/492)), where community skills misuse the `anthropic/` namespace, creating security risks.
*   **Standardization:** There is a call to update foundational tools like `skill-creator` to match best practices rather than acting as educational documentation ([#202](https://github.com/anthropics/skills/issues/202)).

**B. Technical Stability & Evaluation**
*   **Evaluation Frameworks:** A critical bug was flagged where `run_eval.py` fails to trigger skills/commands ([#556](https://github.com/anthropics/skills/issues/556)), preventing developers from validating their work.
*   **API Reliability:** Multiple reports ([#406](https://github.com/anthropics/skills/issues/406), [#403](https://github.com/anthropics/skills/issues/403), [#389](https://github.com/anthropics/skills/issues/389)) indicate instability with skill uploading, deletion, and the OPUS 4.5 API configuration.

**C. Integration & Expansion**
*   **MCP Integration:** Requests to expose Skills as MCPs (Model Context Protocols) ([#16](https://github.com/anthropics/skills/issues/16)) suggest users want to modularize and package AI software components more effectively.
*   **Enterprise Compatibility:** Users need solutions for environments lacking API keys (Enterprise/SSO) ([#532](https://github.com/anthropics/skills/issues/532)), ensuring `skill-creator` works in locked-down corporate environments.

---

## 3. High-Potential Pending Skills
These PRs are active and unresolved, likely to impact the ecosystem soon:

*   **[#535: avoid-ai-writing](https://github.com/anthropics/skills/pull/514)** (Open)
    *   **Potential:** High. A content auditor that removes "AI-isms" (21 pattern categories). Addresses the growing need for human-like tonal quality in AI-generated text.

*   **[#486: ODT (OpenDocument Text) Skill](https://github.com/anthropics/skills/pull/486)** (Open)
    *   **Potential:** Moderate to High. Adds ISO-standard support for `.odt` files (LibreOffice/OpenOffice format). Vital for interoperability in open-source ecosystems.

*   **[#363: Fix feature-dev workflow bug](https://github.com/anthropics/skills/pull/363)** (Open)
    *   **Potential:** High. Fixes a critical `TodoWrite` overwrite bug causing workflow phases to skip. This is a maintenance fix for a core workflow.

*   **[#374: x402 BSV auth + micropayment skill](https://github.com/anthropics/skills/pull/374)** (Open)
    *   **Potential:** Niche but Innovative. Enables natural-language-triggered micropayments for AI services. Represents a novel monetization pathway.

---

## 4. Skills Ecosystem Insight
The community is currently prioritizing **operational maturity**—shifting focus from experimental skills to **quality assurance, security standardization, and API reliability**—to support professional, enterprise-grade deployments.

*Data synthesized from the `anthropics/skills` repository activity logs dated 2026-03-19.*

---

# Claude Code Community Digest: 2026-03-19

## 1. Today's Highlights

The release of **v2.1.79** brings immediate fixes for critical CLI usability issues, specifically resolving a hang when `claude -p` is spawned as a subprocess and adding a toggle for turn duration. However, the release appears to have introduced a **regression causing automatic task interruptions**, which has generated significant community backlash in the form of duplicate bug reports. On the ecosystem front, the community is aggressively developing **plugins** to address core gaps, including critical fixes for Windows BSODs caused by parallel filesystem operations and persistent terminal scrolling glitches.

## 2. Releases

**v2.1.79**
*   **Authentication:** Added `--console` flag to `claude auth login` to support Anthropic Console (API billing) authentication flows.
*   **Config:** Added "Show turn duration" toggle to the `/config` menu.
*   **Bug Fixes:** Fixed `claude -p` hanging when spawned as a subprocess without explicit stdin (e.g., Python `subprocess.run`). Fixed `Ctrl+` interruption handling.

## 3. Hot Issues

1.  **[BUG] Authorization failed: "Internal server error"** ([#36004](https://github.com/anthropics/claude-code/issues/36004))
    *   *Impact:* Critical. Users are completely blocked from logging in.
    *   *Reaction:* High urgency (23 comments in 24h); suggests a backend outage or failure in the auth flow for v2.1.79.

2.  **[BUG] Forces scroll to top when outputting code** ([#33814](https://github.com/anthropics/claude-code/issues/33814))
    *   *Impact:* High usability disruptor. The TUI forces the viewport to the top during code output, not just during scrolling.
    *   *Reaction:* 19 comments; users report this makes reading long outputs nearly impossible.

3.  **[BUG] Remote control (/rc) not supported in VS Code extension** ([#28951](https://github.com/anthropics/claude-code/issues/28951))
    *   *Impact:* Feature parity gap. CLI feature missing from the IDE integration.
    *   *Reaction:* 44 comments; high demand for deep VS Code integration.

4.  **[Feature] Microsoft 365 Connector for Max Plan** ([#20469](https://github.com/anthropics/claude-code/issues/20469))
    *   *Impact:* Feature restriction. Max users ($200/mo) cannot access M365 connectors available to Team users ($30/seat).
    *   *Reaction:* 31 comments; users feel the tier restrictions are artificially limiting high-value subscribers.

5.  **[Enhancement] cowork for ARM processor** ([#30864](https://github.com/anthropics/claude-code/issues/30864))
    *   *Impact:* Hardware support. Native ARM support for the `cowork` feature is missing.
    *   *Reaction:* 45 comments; high demand from Apple Silicon and ARM server users.

6.  **[BUG] CLI crazy scrolling** ([#34242](https://github.com/anthropics/claude-code/issues/34242))
    *   *Impact:* Visual stability.
    *   *Reaction:* Duplicate of #33814; indicates the scrolling issue is widespread across different environments.

7.  **[FEATURE] Expose Thinking Mode Status in StatusLine JSON** ([#9488](https://github.com/anthropics/claude-code/issues/9488))
    *   *Impact:** Observability. Users want to build custom UIs that reflect the current thinking state.
    *   *Reaction:* 40 👍; strong desire for deeper status integration.

8.  **[BUG] Bash(ls:*) allow rule still prompts** ([#33595](https://github.com/anthropics/claude-code/issues/33595))
    *   *Impact:* Permission fatigue. Even with allow rules in `settings.local.json`, users are prompted for `ls` commands.
    *   *Reaction:* Breaks the expected behavior of the permission system.

9.  **[Feature] Expose /usage subscription quota data** ([#28999](https://github.com/anthropics/claude-code/issues/28999))
    *   *Impact:* Cost monitoring. Users want quota visibility in the statusLine JSON payload.
    *   *Reaction:* 35 👍; critical for users managing spend.

10. **[BUG] Shell snapshot causes 8s overhead** ([#31437](https://github.com/anthropics/claude-code/issues/31437))
    *   *Impact:* Performance. Every Bash tool call incurs ~8s latency due to snapshotting logic.
    *   *Reaction:* Significant productivity killer for terminal-heavy workflows.

## 4. Key PR Progress

1.  **feat(plugins): add model-router plugin** ([#35960](https://github.com/anthropics/claude-code/pull/35960))
    *   Adds a plugin that classifies prompts using Haiku to recommend models (Opus/Sonnet) before execution.
    *   *Value:* Optimizes cost/performance by routing complex queries to stronger models automatically.

2.  **fix(critical): Add tool-mutex plugin** ([#35710](https://github.com/anthropics/claude-code/pull/35710))
    *   Addresses a **critical Windows BSOD** (Wof.sys crash) caused by parallel filesystem operations (Glob/Grep).
    *   *Value:* Essential for stability on Windows; prevents system crashes during agent tasks.

3.  **Add scroll-fix plugin** ([#35683](https://github.com/anthropics/claude-code/pull/35683))
    *   Community fix for the terminal scroll-to-top regression via cursor clamping and a freeze toggle (Ctrl+6).
    *   *Value:* Immediately addresses the top-voted usability bug while the core fix is pending.

4.  **feat: Add developer-utilities plugin** ([#11713](https://github.com/anthropics/claude-code/pull/11713))
    *   Adds `/clean` (cache cleanup), `/validate-commands`, and `/session-picker`.
    *   *Value:* Fills gaps in CLI hygiene and workflow management.

5.  **Add worktree-guardian plugin** ([#35864](https://github.com/anthropics/claude-code/pull/35864))
    *   Detects orphaned agent worktrees with unsaved work to prevent data loss during cleanup.
    *   *Value:* Protects against data loss when the agent manages git branches.

6.  **Add powershell-default plugin** ([#35761](https://github.com/anthropics/claude-code/pull/35761))
    *   Replaces Bash with PowerShell 7+ Preview as the default shell on all OSs.
    *   *Value:* Improves experience for Windows-centric developers.

7.  **Add bridge-fix plugin** ([#35684](https://github.com/anthropics/claude-code/pull/35684))
    *   Fixes Chrome extension bridge connection failures for specific Max subscriber configurations.
    *   *Value:* Restores IDE-to-CLI communication functionality.

8.  **fix: UTF-8 safe string slicing** ([#15806](https://github.com/anthropics/claude-code/pull/15806))
    *   Prevents Rust panics when processing Korean/CJK multi-byte text.
    *   *Value:* Critical stability fix for international users.

9.  **Root cause analysis: terminal scrolls** ([#34798](https://github.com/anthropics/claude-code/pull/34798))
    *   Deep dive into the `Ink` cursor rendering issue causing scroll jumps.
    *   *Value:* Provides the technical groundwork for the official fix.

10. **fix: resultmessage never emitted in headless sdk** ([#35543](https://github.com/anthropics/claude-code/pull/35543))
    *   Fixes missing message emissions in SDK/headless mode.
    *   *Value:* Necessary for integration reliability.

## 5. Feature Request Trends

*   **Observability & Monitoring:** There is a strong trend towards integrating subscription quota data ([#28999](https://github.com/anthropics/claude-code/issues/28999)) and internal state (Thinking Mode [#9488](https://github.com/anthropics/claude-code/issues/9488)) into the `statusLine` JSON. Users want to build custom dashboards to track costs and model behavior.
*   **Platform Parity:** Requests for ARM support ([#30864](https://github.com/anthropics/claude-code/issues/30864)) and VS Code feature parity ([#28951](https://github.com/anthropics/claude-code/issues/28951)) dominate the enhancement list. The community is demanding that "Cowork" and advanced CLI features work everywhere.
*   **Plugin Ecosystem:** The surge in Plugin PRs (Model Router, Dev Utilities, PowerShell) suggests users are taking customization into their own hands rather than waiting for core features.

## 6. Developer Pain Points

*   **Terminal Instability:** The "scroll-to-top" regression ([#33814](https://github.com/anthropics/claude-code/issues/33814)) is the most significant detractor from the user experience today, making the TUI difficult to use for code review.
*   **Platform-Specific Crashes:** Windows users are facing severe instability, ranging from Blue Screen of Death (BSOD) caused by filesystem operations ([#35710](https://github.com/anthropics/claude-code/pull/35710)) to WebView loading errors ([#24142](https://github.com/anthropics/claude-code/issues/24142)).
*   **Auth Fragility:** The spate of "Internal server error" login failures ([#36004](https://github.com/anthropics/claude-code/issues/36004)) is creating high friction, preventing developers from even starting their work sessions.
*   **Performance Overhead:** Reports of 8-second delays per Bash call ([#31437](https://github.com/anthropics/claude-code/issues/31437)) indicate that the environment snapshotting mechanism needs optimization.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest: 2026-03-19

## 1. Today's Highlights
The Codex engineering team is aggressively pushing the boundaries of the **`exec-server` architecture**, with four new Pull Requests detailing a remote execution protocol that moves environment abstraction to a server level. This technical refactoring is happening alongside a spike in user-reported issues regarding **memory management**, **network stability**, and **token billing accuracy** following recent extension updates. Users are also highly anticipating new SDK convenience methods and Python SDK improvements.

## 2. Releases
*   **Rust v0.116.0-alpha series** (Alpha 10, 9, 8, 6): OpenAI has released four rapid-fire alpha versions for the Rust implementation of Codex. While specific changelogs are not detailed in the digest, the versioning jump suggests active stabilization of the underlying runtime or `exec-server` components.
    *   [View Release: v0.116.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.116.0-alpha.10)

## 3. Hot Issues
1.  **[#10410 macOS Intel (x86_64) support](https://github.com/openai/codex/issues/10410)** *(Enhancement)*
    *   **Why it matters:** A highly requested feature (186👍) for users on older Intel Macs who are currently unable to use the native Desktop App, highlighting fragmentation in Apple hardware support.
2.  **[#14593 Burning tokens very fast](https://github.com/openai/codex/issues/14593)** *(Bug)*
    *   **Why it matters:** A critical billing concern. Users report that the latest VS Code extension (v26.311.21342) is consuming tokens significantly faster than usual, impacting Pro and Business users.
3.  **[#10450 Remote Development in Desktop App](https://github.com/openai/codex/issues/10450)** *(Enhancement)*
    *   **Why it matters:** The top-voted request (389👍). Developers want the Desktop App to support SSH/Remote development workflows similar to VS Code, which is currently a major blocker for adoption in enterprise environments.
4.  **[#14209 Reconnecting issues in Europe](https://github.com/openai/codex/issues/14209)** *(Bug)*
    *   **Why it matters:** Users are reporting severe connectivity degradation, specifically noting that the reconnection logic is "worse than last days," suggesting a regression in network handling.
5.  **[#8745 LSP integration for Codex CLI](https://github.com/openai/codex/issues/8745)** *(Enhancement)*
    *   **Why it matters:** A high-value request (188👍) to add Language Server Protocol support directly to the CLI, enabling Codex to understand project symbols and diagnostics better without manual configuration.
6.  **[#11984 App UI extremely slow/laggy](https://github.com/openai/codex/issues/11984)** *(Bug)*
    *   **Why it matters:** Reports of the Electron UI becoming unresponsive during long coding sessions, likely related to memory leaks or DOM node bloating in the desktop interface.
7.  **[#14094 Prompt stuck on "Thinking"](https://github.com/openai/codex/issues/14094)** *(Bug)*
    *   **Why it matters:** A UI deadlock bug where the "Thinking" state persists indefinitely, forcing users to restart the app entirely to resume work.
8.  **[#12491 MCP child processes not reaped](https://github.com/openai/codex/issues/12491)** *(Bug)*
    *   **Why it matters:** A severe memory leak report where the App creates zombie processes (1300+) and consumes 37GB of RAM due to Model Context Protocol (MCP) handlers not cleaning up after themselves.
9.  **[#10601 Sandbox setup error on Windows](https://github.com/openai/codex/issues/10601)** *(Bug)*
    *   **Why it matters:** Windows users are facing blockers when trying to utilize the secure sandbox environments, preventing the use of agent capabilities.
10. **[#12888 Agent edits failing in Sandbox](https://github.com/openai/codex/issues/12888)** *(Bug)*
    *   **Why it matters:** Agents are encountering cryptic "command failed" errors inside the sandbox, leading to poor user experience when trying to automate edits.

## 4. Key PR Progress
1.  **[#15121 Experimental network delegation transport](https://github.com/openai/codex/pull/15121)**
    *   **Details:** Introduces a new protocol surface for delegated model requests and stream metadata. This likely enables complex routing of AI requests through intermediate servers (e.g., for security or monitoring).
2.  **[#15125 Move environment abstraction into exec server](https://github.com/openai/codex/pull/15125)**
    *   **Details:** A significant architectural shift where `codex-exec` exposes an `Environment` struct backed by either local or remote servers. This abstracts the difference between running commands locally vs. in a remote sandbox.
3.  **[#15091 Add exec-server filesystem RPC implementation](https://github.com/openai/codex/pull/15091)**
    *   **Details:** Part 3 of the exec-server stack. Adds the Remote Procedure Call logic for file system operations, allowing the agent to read/write files on a remote server.
4.  **[#15090 Add exec-server exec RPC implementation](https://github.com/openai/codex/pull/15090)**
    *   **Details:** Part 2 of the stack. Implements the actual execution of shell commands and process flow handling within the new server architecture.
5.  **[#15088 Add Python SDK thread.run convenience methods](https://github.com/openai/codex/pull/15088)**
    *   **Details:** Quality of life improvement for Python developers. Adds `thread.run()` methods to simplify synchronous execution flows in the SDK.
6.  **[#14525 Add granular builtin tool enablement](https://github.com/openai/codex/pull/14525)**
    *   **Details:** Adds a `[tools.<feature>]` config surface, allowing users to finely control which built-in tools (like web search or file editing) are available on a per-thread or per-config basis.
7.  **[#14970 Simple directory mentions](https://github.com/openai/codex/pull/14970)**
    *   **Details:** Adds support for mentioning directories (with a trailing slash) in the TUI, allowing agents to scope context to entire folders rather than single files.
8.  **[#15127 Handle stale managed auth refresh races](https://github.com/openai/codex/pull/15127)**
    *   **Details:** Fixes a login bug where cached refresh tokens could expire before being used, causing forced re-logins. It adds a "guarded reload" to refresh tokens locally before attempting a server refresh.
9.  **[#15095 Fix rollout recorder not adding turns after error](https://github.com/openai/codex/pull/15095)**
    *   **Details:** Fixes a data loss bug where the "rollout recorder" (logging system) would stop recording messages if it hit a transient error (like disk full), resulting in missing chat history upon app restart.
10. **[#14416 Reuse skill-scoped managed network proxies](https://github.com/openai/codex/pull/14416)**
    *   **Details:** Improves network handling for "Skills" (custom scripts), ensuring that domain-specific allow/deny rules are correctly applied via dedicated proxies.

## 5. Feature Request Trends
*   **Remote Development & SSH:** The community is clamoring for robust Remote Development support in the Desktop App, a feature standard in VS Code but currently missing in Codex.
*   **Intel Mac Support:** There is a notable divide in hardware support, with Intel Mac users feeling left behind by the current ARM-only builds.
*   **LSP Integration:** Developers want Codex CLI to be "smarter" by ingesting standard Language Server Protocol data, rather than relying solely on context window inference for code understanding.

## 6. Developer Pain Points
*   **Resource Exhaustion:** Multiple reports indicate the Desktop App is creating "zombie" processes (via MCP) and leaking massive amounts of RAM (37GB reported), leading to system slowdowns.
*   **Configuration Fragility:** Users are struggling with `config.toml`, specifically regarding `sandbox_workspace_write` network settings and `apiKeyHelper` dynamic loading, with behaviors differing between CLI and App.
*   **Windows Stability:** Windows users are facing a disproportionate number of issues regarding mapped network drives, sandbox setups, and UI interactions (e.g., Mouse Properties dialog opening unexpectedly).
*   **Token Management:** Anxiety around high token consumption persists, with specific complaints about "burning tokens fast" after updates, suggesting a lack of transparency or control over context caching.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest: 2026-03-19

## 1. Today's Highlights

Development activity is surging around the **Memory Subsystem**, with multiple PRs and issues addressing a new "Memory Manager" agent designed to replace the current `save_memory` tool. Concurrently, the team is prioritizing fixes for the Agent's reliability, specifically targeting context loss after `/plan` approval and optimizing context injection for sub-agents.

## 2. Latest Releases

**v0.36.0-nightly.20260318**
*   **CI Stability**: Fixed a false positive trigger in CI evaluations caused by merge commits ([#22237](https://github.com/google-gemini/gemini-cli/pull/22237)).
*   **Core Fix**: Explicitly passed `messageBus` to the policy engine to resolve issues with MCP tool saves ([#22](https://github.com/google-gemini/gemini-cli/pull/22)).

## 3. Hot Issues

*   [#22266](https://github.com/google-gemini/gemini-cli/issues/22266) | **Agent Context Loss ("Ghosting")**
    *   **Impact**: Users report that after approving a `/plan`, the agent drops context and fails to transition to the execution phase.
    *   **Reaction**: High frustration (6 comments); "Ghosting" implies a critical workflow failure where the agent stops responding.

*   [#22434](https://github.com/google-gemini/gemini-cli/issues/22434) | **Plan Mode Executes Changes**
    *   **Impact**: A safety concern where `plan` mode is actually executing file changes instead of remaining read-only.
    *   **Reaction**: Labeled `status/possible-duplicate`, suggesting this is a known regression affecting trust in the planning feature.

*   [#22028](https://github.com/google-gemini/gemini-cli/issues/22028) | **VS Code Scroll Jumps**
    *   **Impact**: UI inconsistency where the CLI terminal scrolls to the top upon clicking.
    *   **Reaction**: Persistent annoyance; affects usability in VS Code environments.

*   [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) | **Wayland Compatibility**
    *   **Impact**: The browser sub-agent fails on Linux Wayland sessions.
    *   **Reaction**: Priority P1; highlights the need for better Linux desktop environment support.

*   [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) | **Passive Sub-Agent Usage**
    *   **Impact**: The main agent rarely invokes custom skills or sub-agents unless explicitly instructed.
    *   **Reaction**: Community feels the "agentic" capabilities are underutilized.

*   [#23037](https://github.com/google-gemini/gemini-cli/issues/23037) | **Ubuntu 24.04 Installation Failures**
    *   **Impact**: Fresh installs via npm or snap are failing to launch.
    *   **Reaction**: Critical onboarding blocker for new users.

*   [#22267](https://github.com/google-gemini/gemini-cli/issues/22267) | **Browser Agent Ignores Settings**
    *   **Impact**: `settings.json` overrides (like `maxTurns`) are ignored by the Browser Agent.
    *   **Reaction**: Breaks configuration management expectations.

*   [#22093](https://github.com/google-gemini/gemini-cli/issues/22093) | **Agents Running Without Permission**
    *   **Impact**: Sub-agents activated automatically in v0.33.0 despite being set to "disabled".
    *   **Reaction**: Major concern regarding user control and consent.

*   [#22186](https://github.com/google-gemini/gemini-cli/issues/22186) | **Crash on "Get Shit Done" Summary**
    *   **Impact**: The CLI crashes during the final summary output of complex tasks.
    *   **Reaction**: Loss of work and context at the worst possible moment.

*   [#22855](https://github.com/google-gemini/gemini-cli/issues/22855) | **`/plan` Needs Prompt Argument**
    *   **Impact**: Users want to kick off a plan in a single command (e.g., `/plan refactor auth`) rather than entering a separate mode.
    *   **Reaction**: Strong request for workflow efficiency (2 👍).

## 4. Key PR Progress

*   [#22726](https://github.com/google-gemini/gemini-cli/pull/22726) | **Experimental Memory Manager Agent**
    *   **Change**: Introduces a `memoryManager` setting to replace the simple `save_memory` tool with a full sub-agent capable of adding, removing, and deduplicating memories in `GEMINI.md`.
    *   **Significance**: Major upgrade to long-term memory capabilities.

*   [#23032](https://github.com/google-gemini/gemini-cli/pull/23032) | **Memory & JIT Context Injection**
    *   **Change**: Modifies `LocalAgentExecutor` to inject environment memory and JIT context into subagents.
    *   **Significance**: Ensures sub-agents have the same contextual awareness as the main agent.

*   [#22893](https://github.com/google-gemini/gemini-cli/pull/22893) | **`--yolo` Policy Mapping**
    *   **Change**: Maps the `--yolo` flag to a wildcard policy (`allowedTools: ["*"]`) rather than a distinct application state.
    *   **Significance**: Cleans up approval logic and integrates power-user modes into the standard policy engine.

*   [#22869](https://github.com/google-gemini/gemini-cli/pull/22869) | **Dynamic Alternate Buffer Toggle**
    *   **Change**: Allows users to switch between inline and full-screen alternate buffer modes mid-session.
    *   **Significance**: Improves UI flexibility without restarting the CLI.

*   [#22880](https://github.com/google-gemini/gemini-cli/pull/22880) | **Generalized Tool Output Truncation**
    *   **Change**: Extends truncation logic to all string-based tool outputs to prevent "JavaScript heap out of memory" errors.
    *   **Significance**: Critical stability fix for handling large file reads or tool outputs.

*   [#23030](https://github.com/google-gemini/gemini-cli/pull/23030) | **UX Journey Testing Framework**
    *   **Change**: Introduces a "white box" testing framework to verify React component presence and visual state in the terminal.
    *   **Significance**: Improves automated testing coverage for the TUI.

*   [#22978](https://github.com/google-gemini/gemini-cli/pull/22978) | **Partial Threading of AgentLoopContext**
    *   **Change**: Part of an effort to resolve context threading issues in the agent loop.
    *   **Significance**: Architectural improvement aimed at fixing "ghosting" and state loss bugs.

*   [#23029](https://github.com/google-gemini/gemini-cli/pull/23029) | **Fix ToS Link in `/auth`**
    *   **Change**: Corrects the broken Terms of Service link.
    *   **Significance**: Hygiene fix for the onboarding flow.

*   [#22664](https://github.com/google-gemini/gemini-cli/pull/22664) | **ACP Full File Path Reporting**
    *   **Change**: Reports full file paths in ACP notifications instead of just filenames.
    *   **Significance**: Improved clarity for Editor/ACP integration users.

## 5. Feature Request Trends

*   **Enhanced `/plan` Workflow**: Users want `/plan` to accept a prompt argument directly (Issue #22855) and want assurance that plan mode is strictly read-only (Issue #22434).
*   **Memory Architecture**: A clear push toward a dedicated memory subagent (Issue #22726) that intelligently routes between global (`~/.gemini/`) and project (`.gemini/`) context (Issue #22819).
*   **AST-Aware Tooling**: Investigation is underway into using Abstract Syntax Tree (AST) parsing for more precise code reading and mapping (Issue #22745), which would significantly reduce noise and token usage.
*   **Safety & Destructive Actions**: Requests for the agent to actively discourage or stop destructive behaviors (like `git reset --hard`) unless explicitly necessary (Issue #22672).

## 6. Developer Pain Points

*   **Context Loss**: The "Ghosting" issue where the agent drops context after approval (Issue #22266) remains a top frustration.
*   **Sub-Agent Reliability**: Problems with sub-agents hitting `MAX_TURNS` but reporting "GOAL success" (Issue #22323) or executing when they shouldn't (Issue #22093).
*   **Platform Instability**: Installation issues on Ubuntu (Issue #23037) and crashes on Wayland (Issue #21983) or during task summaries (Issue #22186) indicate fragile stability across different environments.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-03-19

## 1. Today's Highlights
Version `1.0.8` has been released, focusing heavily on visual fidelity for terminal environments (correcting colors in `tmux`/SSH) and enabling the alternate screen buffer by default. A pre-release (`1.0.8-0`) simultaneously introduces significant extensibility features, including hooks in `settings.json` and validation for MCP servers. The community is actively debugging high-friction regressions in v1.0.6, specifically "React hooks" errors and truncated text, while extensibility remains a major theme with the introduction of `joinSession` capabilities for extensions.

## 2. Releases
**v1.0.8 (Stable)**
*   **Terminal Rendering:** Fixed agent mode labels and border colors for non-truecolor terminals (tmux, SSH, screen).
*   **UX Improvement:** Alternate screen buffer is now enabled by default to prevent shell history clutter.
*   **Tooling:** The "Exit plan mode" tool now remains available when extension subprocesses join an active session.
*   **View Release:** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

**v1.0.8-0 (Pre-release)**
*   **Extensibility:** Added extension mode settings and support for defining hooks directly in `settings.json` or `settings.local.js`.
*   **MCP Support:** Experimental `MCP_ALLOWLIST` feature flag for validating servers against registries.
*   **Resume Workflow:** `--resume` now accepts task IDs in addition to session IDs.

## 3. Hot Issues
*   **[#2117 React hooks error in v1.0.6](https://github.com/github/copilot-cli/issues/2117)** ⚠️ **High Impact**
    Users on macOS are reporting a "Rendered more hooks than during the previous render" error, causing the CLI to crash. This appears to be a regression introduced in the latest version.
*   **[#1584 Incessant Scrolling](https://github.com/github/copilot-cli/issues/1584)** 🐛 **Visual Stability**
    A top-voted issue describing "seizure-inducing" terminal scrolling during long-running operations. Users are desperate for a stable UI refresh.
*   **[#1838 Deadlock in Nix/direnv](https://github.com/github/copilot-cli/issues/1838)** 🚫 **Blocking Bug**
    The CLI hangs indefinitely when launched in directories with Nix flake-based environments due to subprocess I/O deadlocks.
*   **[#2090 Truncated Questions](https://github.com/github/copilot-cli/issues/2090)** 🗨️ **UX Regression**
    Clarification questions from the agent are being cut off in the terminal, preventing users from effectively interacting with planning mode.
*   **[#2076 Extensions override hooks.json](https://github.com/github/copilot-cli/issues/2076)** 🔌 **Extensibility**
    When a CLI extension uses `joinSession` hooks (e.g., `onPreToolUse`), it appears to disable the existing `hooks.json` pipeline rather than merging with it.
*   **[#2142 onSessionStart hook ignored](https://github.com/github/copilot-cli/issues/2142)** ⚙️ **API Compliance**
    The `additionalContext` return value documented in the Copilot SDK for `onSessionStart` is being silently ignored by the CLI.
*   **[#1897 Authorization Errors](https://github.com/github/copilot-cli/issues/1897)** 🛡️ **Auth**
    Users with Copilot Pro are seeing "You are not authorized" errors, suggesting a bug in policy detection or a change in enterprise requirements.
*   **[#970 macOS Gatekeeper Block](https://github.com/github/copilot-cli/issues/970)** 🍎 **Platform Friction**
    High-voted issue regarding HomeBrew upgrades triggering macOS malware warnings, forcing users to manually bypass security settings.
*   **[#2082 Ctrl+Shift+C Copy Issue](https://github.com/github/copilot-cli/issues/2082)]** 📋 **Input Handling**
    The standard Linux copy shortcut (Ctrl+Shift+C) stopped working in v1.0.4, disrupting workflows for Ubuntu users.
*   **[#2132 OOM Crashes during Agent Tasks](https://github.com/github/copilot-cli/issues/2132)** 💥 **Stability**
    Long sessions running parallel background agents crash abruptly with TypeScript runtime errors, losing in-flight work.

## 4. Key PR Progress
*(Note: Only 1 PR was updated in the last 24 hours)*
*   **[#1850 Create blank.yml](https://github.com/github/copilot-cli/pull/1850)**
    A new pull request opened by CaioCavagnollI. While details are sparse, the title suggests it may relate to workflow templates or agent configurations.

## 5. Feature Request Trends
*   **Global Hooks Configuration**
    Users are requesting a move away from repo-specific `.github/copilot-hooks.json` to a global/user-level configuration to avoid repetitive setup across projects.
*   **Base URL / Custom API Override**
    There is a strong desire for a `COPILOT_BASE_URL` environment variable to allow developers to proxy requests or use alternative APIs while keeping the Copilot UX.
*   **Sub-repository Indexing**
    Requests for the `@` file reference operator to index files contained within git sub-repositories (submodules), not just the root project.

## 6. Developer Pain Points
*   **Unicode Handling:** Multiple reports (WSL/Windows) indicate that copying text containing Unicode characters (e.g., Chinese) results in garbled output or corruption.
*   **Rate Limit Visibility:** Users are frustrated by "Transient API errors" that turn into hard rate limits without clear warning, burning through request quotas during Autopilot or long agent tasks.
*   **Extension Composition:** Developers building extensions are finding it difficult to have their hooks play nicely with the existing `hooks.json` system, leading to broken workflows.
*   **Model Availability:** Confusion and warnings regarding "Claude Sonnet 4.5" not being available for custom agents, forcing fallbacks to default models unexpectedly.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest: 2026-03-19

## 1. Today's Highlights
Version **1.24.0** has been released, focusing heavily on "Plan Mode" enhancements and Windows performance optimizations. Key updates include multi-option selection for plan execution and significant startup speed improvements for Windows users, addressing long-standing latency issues. Additionally, the prompt architecture has been refactored for a more persistent user experience during agent runs.

## 2. Releases
**v1.24.0 (Latest)**
*   **Plan Mode Flexibility:** Introduced multi-option selection in `ExitPlanMode` (#1494), allowing the AI to propose multiple approaches for user selection rather than a simple approve/reject flow. Also enabled `StrReplaceFile` to edit plan files directly without constant approval (#1490).
*   **UI/UX Refactoring:** Implemented a unified prompt router that preserves user input during agent executions (#1491), preventing the loss of typed text when the AI is processing.
*   **Windows Performance:** Merged critical startup optimizations (#1486) to resolve slow launches on Windows (specifically for `uv tool install` users).
*   **Shell Usability:** Adjusted paste collapsing thresholds (#1488) to prevent short code snippets from being aggressively hidden.

## 3. Hot Issues
*   **[#1493 CLI Animation Freeze](https://github.com/MoonshotAI/kimi-cli/issues/1493)** (Bug)
    *   **Impact:** Users cannot distinguish if the CLI is stuck or processing.
    *   **Details:** Reported in v1.23.0; the spinner/animation stops rotating during execution, causing confusion about the application state.
*   **[#1427 Startup Log Spam](https://github.com/MoonshotAI/kimi-cli/issues/1427)** (Bug - Closed)
    *   **Impact:** Noise pollution in terminal output.
    *   **Details:** Users reported excessive logging upon startup. This issue was recently closed, likely alongside the performance refactor in #1486.
*   **[#1343 Windows Slow Startup](https://github.com/MoonshotAI/kimi-cli/issues/1343)** (Bug - Closed)
    *   **Impact:** Developer workflow friction on Windows.
    *   **Details:** Identified `encodings.aliases` and `loguru` as bottlenecks adding ~1.5s delay. Resolved in v1.24.0 via lazy-loading strategies.
*   **[#1495 Configurable Plan Save Location](https://github.com/MoonshotAI/kimi-cli/issues/1495)** (Enhancement)
    *   **Impact:** Project organization.
    *   **Details:** Users want the ability to configure where Plan Mode generates files (e.g., `.kimi/plans`) via `config.toml`.
*   **[#1442 Invoicing UI Missing](https://github.com/MoonshotAI/kimi-cli/issues/1442)** (Bug)
    *   **Impact:** Billing/Account management access.
    *   **Details:** Users cannot find how to issue invoices or access billing windows within the CLI interface.
*   **[#1487 HTTPS MCP User-Agent](https://github.com/MoonshotAI/kimi-cli/issues/1487)** (Bug)
    *   **Impact:** MCP Server connectivity.
    *   **Details:** The HTTP MCP client lacks a default `User-Agent` header, potentially causing connection rejections by some servers.
*   **[#1489 Pasted Text Auto-Collapse](https://github.com/MoonshotAI/kimi-cli/issues/1489)** (Bug - Closed)
    *   **Impact:** Usability of voice/typeless input.
    *   **Details:** Previously, pasted text was collapsed too aggressively, making it hard to review input. Addressed in v1.24.0 by raising thresholds.
*   **[#1492 Command Length Config](https://github.com/MoonshotAI/kimi-cli/issues/1492)** (Enhancement)
    *   **Impact:** Visibility of shell commands.
    *   **Details:** Users want to disable or configure the truncation of long shell commands (e.g., `Used Shell (cd /...)`) to see full context.
*   **[#884 Ruff Dependency Bump](https://github.com/MoonshotAI/kimi-cli/pull/884)** (Dependencies)
    *   **Impact:** Developer experience.
    *   **Details:** PR open to bump `ruff` from 0.14 to 0.15.0, indicating the team is adopting the latest linting standards.
*   **[#1485 Token Stats Test Failures](https://github.com/MoonshotAI/kimi-cli/pull/1485)** (Bug)
    *   **Impact:** Stability of new features.
    *   **Details:** A PR is currently open to fix test failures related to the token usage stats feature, ensuring reliability of cost tracking.

## 4. Key PR Progress
*   **[#1491 Unified Prompt Router](https://github.com/MoonshotAI/kimi-cli/pull/1491)** (Closed -> Merged)
    *   Replaced the dual-prompt architecture (idle vs. running) with a single persistent prompt router. This ensures that if a user starts typing while the AI is thinking, their input is not lost when the agent finishes its turn.
*   **[#1486 Windows Startup Optimization](https://github.com/MoonshotAI/kimi-cli/pull/1486)** (Closed -> Merged)
    *   Implemented lazy-loading for the package logger, version metadata, and heavy CLI subcommands. Routes standard streams to `null` during early startup to prevent overhead. Directly addresses Issue #1343.
*   **[#1490 Plan Mode File Editing](https://github.com/MoonshotAI/kimi-cli/pull/1490)** (Closed -> Merged)
    *   Allowed `StrReplaceFile` tool to modify plan files directly in Plan Mode without triggering repeated approval prompts, streamlining the iterative planning process.
*   **[#1488 Paste Placeholder Thresholds](https://github.com/MoonshotAI/kimi-cli/pull/1488)** (Closed -> Merged)
    *   Raised the clipboard paste collapsing limit from 3 lines/300 chars to 15 lines/1000 chars, improving readability for medium-sized code snippets.
*   **[#1494 Multi-Option Plan Exit](https://github.com/MoonshotAI/kimi-cli/pull/1494)** (Closed -> Merged)
    *   Enhanced Plan Mode to allow the AI to present multiple solution paths (options) to the user, who can then select which specific plan to execute.

## 5. Feature Request Trends
*   **Plan Mode Customization:** There is a clear trend toward making "Plan Mode" more robust and user-configurable. Users are asking for better file management (configurable save paths #1495) and more flexible execution options (multi-select PR #1494).
*   **UI/UX Transparency:** Users are demanding better visibility into system status and content.
    *   **Status:** Request for animated spinners to confirm activity (#1493).
    *   **Content:** Request to prevent command truncation (#1492) and text collapsing (#1489).

## 6. Developer Pain Points
*   **Windows Performance:** Historically slow startup times (caused by Python encoding handling and logging) have been a major friction point. While addressed in v1.24.0, it remains a key area of user sensitivity.
*   **Input Handling Feedback:** Developers are frustrated by "black box" states where the CLI appears frozen (lack of animation #1493) or input is inadvertently hidden/collapsed (pasted text #1489, shell commands #1492).
*   **Workflow Disruption:** Issues like the loss of input during agent runs (fixed in #1491) highlight a desire for a more resilient and interrupt-driven interactive shell.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest: 2026-03-19

## Today's Highlights
The OpenCode community is actively addressing significant stability concerns regarding the Bun runtime environment on Windows, following the `1.3.5` release. Concurrently, the development team is pushing forward with user experience enhancements for the Desktop application, introducing native git integration and refined permission management. The synchronization infrastructure (`PR #17814`) remains a primary focus for long-term architectural improvements.

## Releases
*No new releases published in the last 24 hours.*

## Hot Issues
1.  **[#3936](https://github.com/anomalyco/opencode/issues/3936) - [OPEN] GitHub Enterprise Authorization Failures**
    *   **Impact:** High. Blocks enterprise users from logging in.
    *   **Reaction:** 57 comments indicate widespread frustration with self-hosted GitHub instances.

2.  **[#8598](https://github.com/anomalyco/opencode/issues/8598) - [CLOSED] "Model Not Supported" Errors in Copilot**
    *   **Impact:** High. Disrupts users with specific model configurations (5.2-Codex, Raptor).
    *   **Reaction:** 46 comments; while closed, the volume suggests the fix is critical for user retention.

3.  **[#17318](https://github.com/anomalyco/opencode/issues/17318) - [OPEN] SSE Read Timed Out**
    *   **Impact:** High. Breaks file writing operations.
    *   **Reaction:** 31 👍 reflects that this is a top stability priority for v1.2.25+ users.

4.  **[#4659](https://github.com/anomalyco/opencode/issues/4659) - [OPEN] Sliding Window Context Management**
    *   **Impact:** Strategic. Proposes a fundamental shift in how long-running sessions handle memory.
    *   **Reaction:** High interest (18 👍) in architectural improvements over simple summarization.

5.  **[#8785](https://github.com/anomalyco/opencode/issues/8785) - [OPEN] Bun v1.3.5 Crashes (Windows)**
    *   **Impact:** Critical. Renders the app unusable on Windows Zen builds.
    *   **Reaction:** Users are reporting crash dumps related to AVX and CPU optimization.

6.  **[#5220](https://github.com/anomalyco/opencode/issues/5220) - [OPEN] Glob Search CPU Saturation**
    *   **Impact:** Performance. Search operations lock the CPU.
    *   **Reaction:** 12 👍; indicates urgent need for async search optimization.

7.  **[#17796](https://github.com/anomalyco/opencode/issues/17796) - [OPEN] TUI Copy via Selection Broken**
    *   **Impact:** UX. Core workflow failure in the terminal UI.
    *   **Reaction:** Users report the clipboard action is silent/ineffective.

8.  **[#11865](https://github.com/anomalyco/opencode/issues/11865) - [OPEN] Subagents Hang Indefinitely**
    *   **Impact:** Workflow. Stops multi-agent tasks dead.
    *   **Reaction:** Highlights a need for timeout/retry logic in agent orchestration.

9.  **[#18134](https://github.com/anomalyco/opencode/issues/18134) - [OPEN] Desktop "Close" Behavior**
    *   **Impact:** UX. Users expect minimizing to tray rather than full exit.
    *   **Reaction:** Reflects a desire for background operation parity with Slack/Discord.

10. **[#18151](https://github.com/anomalyco/opencode/issues/18151) - [OPEN] File Write Failures**
    *   **Impact:** Critical. Core functionality of creating/updating files is unstable.
    *   **Reaction:** Reports suggest `{}` arguments are being passed to the write tool.

## Key PR Progress
1.  **[#18144](https://github.com/anomalyco/opencode/pull/18144) - Bump Bun to 1.3.11**
    *   **Change:** Upgrading the runtime from the crash-prone 1.3.10/1.3.5 to 1.3.11.
    *   **Significance:** Likely addresses the wave of Windows crash reports.

2.  **[#17814](https://github.com/anomalyco/opencode/pull/17814) - Core Syncing Implementation**
    *   **Change:** Initial implementation of the syncing service.
    *   **Significance:** A massive technical undertaking enabling state synchronization across devices.

3.  **[#18152](https://github.com/anomalyco/opencode/pull/18152) - Native Commit Actions in Desktop**
    *   **Change:** Adds a GUI for git commits (staging, committing) within the Desktop app.
    *   **Significance:** Reduces reliance on CLI/git tools for Desktop users.

4.  **[#18170](https://github.com/anomalyco/opencode/pull/18170) - Show Git Branch in TUI Sidebar**
    *   **Change:** Displays the active branch below the folder path.
    *   **Significance:** Essential context for developers juggling multiple feature branches.

5.  **[#17484](https://github.com/anomalyco/opencode/pull/17484) - Permissions Settings Panel**
    *   **Change:** Adds a UI tab to manage default tool permissions.
    *   **Significance:** Improves security and configurability without editing JSON configs.

6.  **[#17067](https://github.com/anomalyco/opencode/pull/17067) - Normalize Directory Paths (Windows)**
    *   **Change:** Fixes path casing (B: vs b:) issues causing session visibility bugs.
    *   **Significance:** Improves reliability on Windows file systems.

7.  **[#18163](https://github.com/anomalyco/opencode/pull/18163) - Resolve Model from Agent Config**
    *   **Change:** Ensures `plan` and `build` agents use their specific configured models.
    *   **Significance:** Fixes agent configuration hierarchy issues.

8.  **[#18157](https://github.com/anomalyco/opencode/pull/18157) - Opt-in Auto-Continue**
    *   **Change:** Experimental feature to automatically continue if the AI stops prematurely.
    *   **Significance:** Reduces user intervention for "incomplete" responses.

9.  **[#18146](https://github.com/anomalyco/opencode/pull/18146) - Support Windsurf in "Open In"**
    *   **Change:** Adds Windsurf editor to the desktop file opener dropdown.
    *   **Significance:** Expands IDE interoperability.

10. **[#13854](https://github.com/anomalyco/opencode/pull/13854) - Stop Streaming Markdown on Completion**
    *   **Change:** Fixes visual artifacts where tables/code render incorrectly if the message is finished.
    *   **Significance:** Polish for the TUI reading experience.

## Feature Request Trends
*   **Native Git Integration:** Users want git status (branches) directly visible in the TUI sidebar and native commit flows in the Desktop GUI to avoid context switching.
*   **Configuration Management:** There is a strong push for granular control over agent models, tool permissions (at a conversation level), and "Sliding Window" context management for long sessions.
*   **Desktop UX Parity:** Requests are aligning the Desktop app behavior with standard industry expectations, such as minimizing to the system tray and clickable file references in the chat stream.

## Developer Pain Points
*   **Windows Stability:** A cluster of issues regarding `Bun` crashes (AVX errors) and path normalization is making the Windows experience fragile.
*   **Timeouts & Connectivity:** "SSE read timed out" errors are rampant, causing data loss when writing files or using large local models.
*   **Agent Reliability:** Subagents are getting stuck in loops or hanging indefinitely, forcing users to restart sessions manually.
*   **Resource Usage:** High CPU usage during file searches (glob/rg) is degrading system performance.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest: 2026-03-19

## 1. Today's Highlights
The Qwen Code ecosystem is experiencing significant instability surrounding the **v0.13.0** release, with both `preview` and `nightly` workflows failing in the last 24 hours. Despite these release hiccups, development activity remains high, focusing heavily on **concurrency improvements** (parallel sub-agents) and **usability enhancements** (token visibility, fuzzy search) in the upcoming milestone. The community is actively vocal about regressions in the current stable version (0.12.x), specifically regarding "edit failures" and session interruptions.

## 2. Latest Releases
*   **[sdk-typescript-v0.1.6-preview.0](https://github.com/QwenLM/qwen-code/releases)**: A minor release bump primarily to backfill the npm-published version 0.1.5. This release bundles CLI version 0.13.0, indicating the SDK is trying to catch up to the pre-release tooling chain.

## 3. Hot Issues
*   **[#2460: Critical "Edit Failed" Regression](https://github.com/QwenLM/qwen-code/issues/2460)** (type/bug)
    Users are reporting that the latest CLI & VS Code versions suffer from severe and frequent editing failures ("0 occurrences found"). One user reported that aggressive failed attempts damaged their codebase using external editors, marking this as a high-priority stability issue.
*   **[#2382: VS Code Extension Non-functional](https://github.com/QwenLM/qwen-code/issues/2382)** (scope/vscode)
    Multiple reports confirm the Qwen Code Companion extension is broken in v0.12.3, failing to initialize ("Preparing Qwen Code...") even after downgrading VS Code versions.
*   **[#2426: Free Tier Quota Confusion](https://github.com/QwenLM/qwen-code/issues/2426)** (type/badcase)
    Users are complaining that the advertised free quota (1000 requests/day) has been significantly reduced (estimated <300) without clear communication, causing friction for daily drivers.
*   **[#2459: `/compress` Command Fails at Context Limit](https://github.com/QwenLM/qwen-code/issues/2459)** (status/needs-triage)
    When the context window hits 100%, the manual `/compress` command throws an "Internal error" instead of resolving the session, forcing users to restart their work.
*   **[#2409: Feature Parity with Claude Code](https://github.com/QwenLM/qwen-code/issues/2409)** (type/feature-request)
    A detailed request comparing Qwen Code’s subagent system (~40-45% feature complete) to Claude Code, asking for specific gaps in markdown handling and agent coordination to be filled.
*   **[#2462 & #2449: Abrupt Session Termination](https://github.com/QwenLM/qwen-code/issues/2462)** (type/bug)
    Users are experiencing sessions that end abruptly with `[object Object]` output or immediately after tool calls, making the tool unreliable for long tasks.
*   **[#2306: Crash on "Always Allow" Permission](https://github.com/QwenLM/qwen-code/issues/2306)** (type/bug)
    A regression introduced in v0.12.0 causes the CLI to crash and exit to the terminal when users select "always allow" for command execution prompts.
*   **[#1873: LSP Config Ignored](https://github.com/QwenLM/qwen-code/issues/1873)** (status/needs-triage)
    The experimental LSP support fails to read `.lsp.json` configurations, resulting in "No document symbols found" for valid C/C++ files despite correct setup.
*   **[#2461: Table Rendering Bug](https://github.com/QwenLM/qwen-code/issues/2461)** (type/bug)
    The `|` character in Markdown tables is not being escaped correctly, causing cell data to leak into adjacent columns or break formatting.
*   **[#2468 & #2467: Release Pipeline Failures](https://github.com/QwenLM/qwen-code/issues/2468)** (type/badcase)
    Automated GitHub Actions have failed to publish both the `v0.13.0-preview.0` and nightly builds, blocking access to the latest fixes for users waiting on these branches.

## 4. Key PR Progress
*   **[#2445: Token Usage in Progress Indicator](https://github.com/QwenLM/qwen-code/pull/2445)** (feat/ui)
    Merged for v0.13.0. This PR adds real-time token output counts to the loading spinner, giving developers visibility into costs and context usage during generation.
*   **[#1835: `/context` Slash Command](https://github.com/QwenLM/qwen-code/pull/1835)** (feat)
    Merged for v0.13.0. Introduces a command to display a detailed breakdown of context window usage, helping developers manage long sessions more effectively.
*   **[#2437: Fuzzy Search for File Completion](https://github.com/QwenLM/qwen-code/pull/2437)** (refactor)
    Merged for v0.13.0. Replaces simple substring matching with backend fuzzy search for the `@` file menu, significantly improving file discovery in large projects.
*   **[#2434: Concurrent Task Execution](https://github.com/QwenLM/qwen-code/pull/2434)** (feat/core)
    Merged for v0.13.0. Enables parallel execution of "task tools" (sub-agents), dramatically speeding up workflows that require multiple independent agents (e.g., test + lint).
*   **[#2446: MCP Tool Output Truncation](https://github.com/QwenLM/qwen-code/pull/2446)** (fix)
    Merged for v0.13.0. Prevents MCP server responses from overwhelming the context window by applying the same truncation logic used by built-in shell tools.
*   **[#2458: Improved Error & Quota Detection](https://github.com/QwenLM/qwen-code/pull/2458)** (refactor/core)
    Merged for v0.13.0. Refines error handling to specifically distinguish Qwen "free quota exceeded" errors (429) from other API failures, improving user feedback.
*   **[#2464: Fix `/compress` Reliability](https://github.com/QwenLM/qwen-code/pull/2464)** (fix)
    Addresses Issue #2459. Fixes a bug where compression would report success but fail to actually reduce token count, leading to API crashes.
*   **[#2431: Tab Key "Fill-Only" Behavior](https://github.com/QwenLM/qwen-code/pull/2431)** (feat(vscode))
    Merged for v0.13.0. Changes the VS Code completion menu so `Tab` fills the suggestion without executing, allowing users to edit the prompt before sending.
*   **[#2450: OpenAI API Compliance Fix](https://github.com/QwenLM/qwen-code/pull/2450)** (fix)
    Currently Open. Addresses a 400 error when using tools with OpenAI-compatible APIs (like OpenRouter) by fixing the storage format of tool responses in history.
*   **[#2202: Multi-Directory Skill Support](https://github.com/QwenLM/qwen-code/pull/2202)** (feat)
    Currently Open. Allows loading skills from standard directories like `.cursor/skills/` or `.claude/skills/`, improving interoperability for users migrating between AI IDEs.

## 5. Feature Request Trends
*   **Multi-Agent Orchestration**: There is strong interest in "Agent Arena" (competitive execution) and "Agent Teams" (collaborative execution). Users want to run multiple models in parallel or have specialized sub-agents coordinate complex tasks (Issues #1815, #1814).
*   **Enhanced Context Management**: With v0.12.x hitting context limits frequently, users are aggressively requesting better compression (Issue #2459), visual usage indicators (Added in PR #2445), and handling of large file outputs.
*   **Interoperability**: Users want Qwen Code to share configs with other tools. Requests include supporting `.cursor` rules, standard MCP transport modes, and standard VS Code authentication flows (Issue #2436, PR #2202).

## 6. Developer Pain Points
*   **Regression Anxiety**: The community is reporting that newer versions (0.12.2/0.12.3) feel less stable than previous iterations, specifically citing the inability to edit code successfully and random crashes during permission prompts.
*   **Context Window Fragility**: Once the context limit is reached, the tool becomes unusable. The fallback mechanisms (compression) are failing, forcing session restarts and lost work.
*   **Edit Logic Gaps**: The strict string matching required for code edits ("old_string not found") is failing on whitespace or encoding differences, leading to "destructive" edit attempts where the tool loops trying to fix invisible formatting errors.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/yinwm/agents-radar).*