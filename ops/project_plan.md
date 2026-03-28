---
type: project-plan
project: ops
last_updated: 2026-03-28
---

# Ops — Reference Plan

**Context:** How Kerry and Kai work together — session architecture, personas, skills, configuration, and system design.

---

## System Architecture

### Session Loading Pattern
- **Layer 1 (always):** CLAUDE.md + MEMORY.md — behavioral rules and persistent memory
- **Layer 2 (/open):** SESSION.md only — last 5 decisions + immediate focus + workstream menu
- **Layer 3 (explicit):** `/open[Workstream]` skills — intentional context injection per workstream
- **Layer 4 (lazy):** Keyword-triggered file loads mid-session — see `_meta/TRIGGERS.md`

### File Roles
| File | Role | When loaded |
|---|---|---|
| `SESSION.md` | Pointer table + last 5 decisions | Always on /open |
| `[ws]/status.md` | Active work + Now priorities | Explicit skill or keyword trigger |
| `[ws]/project_plan.md` | Full reference + all priority tiers | Planning trigger or explicit request |
| `[ws]/completed.md` | Archive with reusable detail | When referenced |
| `_meta/TRIGGERS.md` | Keyword→file map | Governs lazy loading |
| `_meta/PERSONAS.md` | Persona definitions per workstream | Reference; embedded in skill files |
| `CONTEXT.md` | Static personal/property context | Deep context trigger |

---

## Personas

Defined in `_meta/PERSONAS.md`. Summary:
- **Default** — always active; concise, technical terms labeled, collaborative
- **Health** — adds encouragement and progress acknowledgment
- **MetaTemplate** — adds professional tone, future-proof thinking, generalization pushback
- **Ops** — adds architectural thinking, decision documentation, pattern recognition

**Cross-cutting rule:** In any session, flag MetaTemplate improvements inline → defer to `_meta/IMPROVEMENTS.md` if not acted on.

---

## Workstream Registry

| Workstream | Skill | Status file | Persona |
|---|---|---|---|
| Home & Garden | `/openHomeProjects` | `home/status.md` | Default |
| MetaTemplate | `/openMetaTemplate` | `template/status.md` | MetaTemplate |
| Health | `/openHealth` | health files (external) | Health |
| Ops | `/openOps` | `ops/status.md` | Ops |

---

## Adding a New Workstream

Full checklist in `_meta/TRIGGERS.md`. Steps:
1. Add trigger row (keywords → status.md)
2. Create workstream files from `_template/`
3. Add to SESSION.md Active Projects
4. Create `open[Name].md` skill
5. Add skill to `/open` workstream list

---

## Plan Ahead

| Item | Notes |
|---|---|
| Repo restructure for sharing | Promote AGENT.md/SESSION.md/CONTEXT.md to repo root; prune _template/; add .claude/commands/ |
| Persona system evolution | Health persona traits may expand; review after a few health sessions |
| Additional workstreams | TBD as Kerry's needs grow |
