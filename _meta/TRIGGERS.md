---
type: trigger-map
last_updated: 2026-03-28
---

# Trigger Map

When Kerry references any of the following keywords or topics, load the corresponding file before responding. Do not load files proactively — only when the topic comes up.

| Keywords / Topics | File to Load |
|---|---|
| home, house, garden, yard, deck, crawlspace, garage, stream, blueberry, blackberry, kiwi, potato, maple, taxes, VA, disability, renovation, under-sink, basketball, raised bed, soil, planting, spring | `home/status.md` |
| template, MetaTemplate, AGENT.md | `template/status.md` |
| ops, session architecture, skill, persona, workstream, CLAUDE.md, TRIGGERS, lazy load, context injection, configure, /open, /close | `ops/status.md` |
| health, supplements, energy, protocol, sleep, recovery, workout, nutrition | health files at `C:\Users\kerry\OneDrive\kAI2026\` |
| kPro, developer, software engineer, career, resume, LinkedIn, technology, tech stack, build guide, coding, framework, language, IT, programming | `kpro/status.md` |
| planning, full list, road map, all projects, what else, bigger picture | `[workstream]/project_plan.md` |
| completed, finished, how did I, last time, previously, archive, reference | `[workstream]/completed.md` |
| who am I, property, background, personal context, Fort Mill, address | `CONTEXT.md` |

## Adding a New Workstream

When Kerry says "I want to start a new workstream", complete all of the following:

1. Add one row to the trigger table above (keywords → `status.md` path)
2. Create `[workstream]/status.md`, `[workstream]/project_plan.md`, `[workstream]/completed.md` from `_template/`
3. Add the workstream to SESSION.md Active Projects table
4. Create `.claude/commands/open[WorkstreamName].md` — explicit context injection skill
5. Add the new skill to the "Load a workstream" list in `.claude/commands/open.md`
