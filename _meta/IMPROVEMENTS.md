---
type: improvements-log
last_updated: 2026-03-27
---

# Improvements Log

Captured observations, lessons learned, and recommendations for improving the system.
Add an entry whenever something works better than expected, fails, or could be done differently.

---

## Format

```
### YYYY-MM-DD — [Short title]
**Observation:** What happened or was noticed
**Recommendation:** What to change or try
**Status:** Open / In Progress / Done / Rejected
```

---

## Log

### 2026-03-27 — Template must be portable and AI-agnostic
**Observation:** The end goal is to package the template so it can be handed to someone else and used with any AI assistant — Claude, GitHub Copilot Agent, or others.
**Recommendation:** Three things need to change or be added:
1. `CLAUDE.md` is Claude-specific — the template needs a parallel `AGENT.md` (or similar) written in AI-agnostic language so any assistant can load and follow the session protocol
2. A `QUICKSTART.md` needs to exist in the template — a human-readable onboarding doc that tells a new user exactly what to do to stand up their own version of this system from scratch
3. Any Claude-specific syntax or tooling referenced in process docs should be noted as Claude-specific, with a note on what the equivalent would be in other tools
**Status:** Open — delivery format (zip vs. repo) to be decided later. When Kerry says "prepare for sharing," build QUICKSTART.md, AGENT.md, and annotate process docs at that time.

### 2026-03-27 — Multi-environment compatibility: document how to run this in constrained AI tools
**Observation:** This system must work across different AI environments with different capabilities — not just Claude Code. Three environments to target:
1. **Claude Code / VS Code + Copilot Agent** — full file read/write, current implementation
2. **VS Code + GitHub Copilot** — similar file access, different tool syntax and agent behavior
3. **M365 Copilot Chat (enterprise)** — no file creation, paste-based workflow only; session state must be maintained by the user copying/pasting context manually
**Recommendation:** When ready, document a variant of PROCESS.md for each environment. The no-file-access variant (M365) is the most constrained and needs the most creative adaptation — likely a "paste this block at the start of every chat" pattern. Revisit and evaluate whether the current architecture is the best approach for all three, or if a modified structure serves the constrained environments better.
**Status:** Open — deferred, revisit once home project is actively running and structure is proven

### 2026-03-27 — Publish to GitHub when project is active and structure is proven
**Observation:** The kAI project should be published to GitHub, but not yet — the structure needs to be stable and there should be real working content (e.g. active gardening tasks, completed projects) to demonstrate the system in practice.
**Recommendation:** When Kerry says "prepare for GitHub," do the following: (1) review all files and scrub any sensitive personal info (address, personal details) from template files, (2) create a README.md at the kAI root that serves as the GitHub landing page, (3) initialize a git repo and create a remote on GitHub. The home project content can either be excluded via .gitignore (private) or sanitized for sharing — Kerry to decide at that time.
**Status:** Open — deferred until project structure is stable and real tasks are underway

### 2026-03-27 — Two deliverable documents needed: pitch deck and retrospective guide
**Observation:** Two distinct documents need to be created at different points in the project lifecycle:
1. **Early-stage HTML presentation** — created soon, after the foundation is set. Explains what this system is, what it proposes, and why it matters. Audience: someone seeing this for the first time. Purpose: show the vision before the proof is complete.
2. **End-stage process retrospective** — created once the system has been used long enough to validate. Documents how to repeat this process, what worked, why it worked, and the full journey. Audience: someone who wants to build their own version. Purpose: the teachable, shareable guide.
**Recommendation:** When Kerry says "build the intro presentation," generate the HTML deck from current `_meta/` content. When Kerry says "build the retrospective," compile from IMPROVEMENTS.md, DECISIONS.md, and project history.
**Status:** Open — both deferred until prompted

### 2026-03-27 — Future-proofing is a core design requirement
**Observation:** The system must remain useful as AI capabilities advance. Small updates should be sufficient to adapt — no rebuilding from scratch.
**Recommendation:** Always design with this hierarchy in mind: (1) project content files should never need structural changes, (2) behavior/instruction files (CLAUDE.md, session loaders) may need small updates as AI tools evolve, (3) process docs are what make those updates fast and confident. When adding anything new, ask: "If AI capabilities doubled tomorrow, would this still make sense?"
**Status:** Ongoing — apply to every design decision

### 2026-03-27 — Initial system setup via VS Code extension, then migrated to Claude Code CLI
**Observation:** The initial project setup was done in the VS Code Claude extension chat. That chat had no access to the filesystem directly, required copy-pasting file contents, and had no persistent memory. Migrating to Claude Code CLI gave full file read/write access, auto-loading via CLAUDE.md, and a much tighter feedback loop.
**Recommendation:** Always set up new projects using Claude Code CLI, not the extension chat. The extension is useful for quick questions; the CLI is the right tool for file-based project work.
**Status:** Done

### 2026-03-27 — PowerShell profile needed for terminal consistency
**Observation:** New VS Code terminals were not loading the PowerShell profile because `Microsoft.PowerShell_profile.ps1` did not exist — only `Microsoft.VSCode_profile.ps1` did. New terminals use the standard profile, not the VS Code-specific one.
**Recommendation:** When setting up on a new machine, ensure `Microsoft.PowerShell_profile.ps1` exists and dot-sources `Microsoft.VSCode_profile.ps1`. Document this in any machine setup guide.
**Status:** Done

### 2026-03-27 — `claude` command needed a PowerShell wrapper
**Observation:** Claude Code is installed as `claude.cmd` via npm. To always start a session from the kAI directory, a PowerShell wrapper function was needed in the profile. The first attempt using `Get-Command` failed due to path resolution; direct path to `claude.cmd` worked.
**Recommendation:** On new machine setup, add the wrapper function to the PowerShell profile early. Use `& "$env:APPDATA\npm\claude.cmd" @args` as the invocation pattern.
**Status:** Done
