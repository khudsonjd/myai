---
type: process-guide
last_updated: 2026-03-27
---

# Project Setup Process

A repeatable guide for spinning up a new AI-assisted project in the kAI system.

---

## Prerequisites
- Claude Code installed and accessible via `claude` in PowerShell
- `kAI/` directory exists somewhere on your machine (location is up to you)
- `CLAUDE.md` is at the kAI root (controls Claude's session behavior)
- `_template/` contains blank `SESSION.md` and `project_plan.md`

---

## Steps to Add a New Project

### 1. Create the project folder
```
kAI/[project-name]/
```

### 2. Copy templates into the new folder
```
_template/project_plan.md  →  [project-name]/project_plan.md
```

### 3. Create status.md
No template — create fresh each project. Minimum sections:
- Recently Completed
- Priority Summary (Now / Soon / Anytime / Plan Ahead)
- Supply Needs (if applicable)

### 4. Fill in project_plan.md
Replace all placeholder brackets with real content. Keep it stable — this is reference data, not active state.

### 5. Update root SESSION.md
Add the new project to the Active Projects table and update Immediate Focus if it's high priority.

### 6. Start a session
```powershell
claude
```
Claude reads `CLAUDE.md` automatically, which instructs it to load `SESSION.md` and the relevant status file.

---

## File Roles (Quick Reference)

| File | Purpose | Update frequency |
|---|---|---|
| `CLAUDE.md` | Instructs Claude how to behave in this directory | Rarely |
| `SESSION.md` | Master loader — orients Claude at session start | When projects or focus change |
| `[project]/project_plan.md` | Stable reference data for the project | Rarely |
| `[project]/status.md` | Current state — priorities, deadlines, active items | Every session |
| `_template/` | Blank files to copy for new projects | When templates improve |
| `_meta/` | Process docs, decisions, improvement log | As needed |

---

## Starting a Session
```powershell
claude
```
Claude will automatically:
1. Read `CLAUDE.md`
2. Read `SESSION.md`
3. Read the status file for the active project
4. Confirm ready and state current focus
