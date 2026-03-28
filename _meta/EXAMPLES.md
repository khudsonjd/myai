---
type: examples
last_updated: 2026-03-28
---

# MetaTemplate — Personalization Examples

Short, generic examples of real patterns used in practice. Adapt these to your own context.

> **Note for Kai:** This file must be updated whenever a new structural pattern, persona type, or system behavior is introduced to the kAI workspace. If we do it in practice and it's generalizable, it belongs here — genericized. Do not wait to be asked.

---

## 1. Multiple Efforts in One Workspace

One SESSION.md pointer table can hold multiple distinct efforts — each with its own project_plan.md and status.md.

```markdown
## Active Projects

| Project         | Status Files                                    | Priority |
|-----------------|-------------------------------------------------|----------|
| Home Renovation | `home/project_plan.md`, `home/status.md`        | HIGH     |
| Framework Build | `framework/project_plan.md`, `framework/status.md` | Active   |
| Research        | `research/project_plan.md`, `research/status.md` | Normal  |
```

SESSION.md stays small regardless of how many efforts exist — it's a pointer table, not a content file.

---

## 2. Keeping a Sensitive Effort Private

Some efforts contain personal or sensitive data that should never appear in shared files or version control.

- Store them in a completely separate folder outside the main workspace
- Reference them only as a pointer in SESSION.md (no content)
- Add the folder to `.gitignore`
- Use memory to tell the AI when and how to load those files

```markdown
# .gitignore
private/
sensitive-effort/
/CONTEXT.md
```

```markdown
# memory file: reference_sensitive_files.md
When [topic] comes up, read:
- /path/to/sensitive/context.md
- /path/to/sensitive/status.md
Never include this data in shared or published files.
```

---

## 3. Persona Modes per Workstream

Different workstreams benefit from different AI response styles. Define all personas in a central `_meta/PERSONAS.md` file, then activate them via the workstream's `/open[Name]` skill.

**Key principles:**
- A **Default** persona is always active — tone, conciseness, terminology labeling, etc.
- Workstream personas **stack on top of Default** — they add traits, not replace them
- The `/open[Name]` skill embeds the persona instructions so they activate at load time
- A **cross-cutting rule** can apply to every session regardless of workstream (e.g., always flag improvements to a shared template)

```markdown
# _meta/PERSONAS.md

## Default (always active)
- Concise and direct
- Label technical terms when the user describes concepts in plain language
- Collaborative — state intent before acting

## Health (stacks on Default)
*Activates on: /openHealth*
- Acknowledge effort and progress explicitly
- Warm, encouraging tone throughout

## Professional (stacks on Default)
*Activates on: /openResearch*
- Formal tone; cite sources and flag assumptions
- Prioritize accuracy over speed; flag uncertainty explicitly

## Cross-Cutting Rule (every session)
When a reusable pattern emerges, flag it inline: `Template note: [what and why]`
If deferred, add it to a running improvements list automatically.
```

```markdown
# .claude/commands/openHealth.md

Read health files.

Activate Health persona:
- Acknowledge effort and progress explicitly
- Warm, encouraging tone

Then summarize current status and ask what to work on.
```

**Common named persona variants:**

| Persona | Traits | Good for |
|---|---|---|
| **Supportive** | Acknowledge progress, warm tone, softer pushback | Health, personal goals, sensitive topics |
| **Builder** | Direct, execute and document, propose before acting | Technical builds, project management |
| **Senior Advisor** | Proactive suggestions, industry standards, future-proofing, flag outdated patterns | System/ops work, architecture, configuration |
| **Professional** | Formal tone, accuracy over speed, flag uncertainty | Research, writing, client-facing work |

**When to use:** Any workspace with multiple efforts that benefit from different interaction styles.

---

## 4. Memory Portability

Memory files live in two places: Claude's internal storage (auto-loaded) and `_memory/` in the workspace (portable, human-readable, backed up).

```
kAI/
└── _memory/
    ├── MEMORY.md          ← index of all memory files
    ├── user_role.md       ← who you are, working relationship
    ├── feedback_*.md      ← behavioral rules and corrections
    └── reference_*.md     ← where to find things
```

Each memory file follows this format:

```markdown
---
name: Short descriptive name
description: One line — used to decide relevance in future sessions
type: user | feedback | project | reference
---

The memory content.

**Why:** Reason this exists.
**How to apply:** When and where this kicks in.
```

When updating memory, update both `~/.claude/projects/.../memory/` and `kAI/_memory/`. The workspace copy is the source of truth.

---

## 5. Session Continuity — Active Work Section

Every status.md includes an "Active Work" section at the top. Updated every session so the next one picks up exactly where this one left off.

```markdown
## Active Work
- Reviewing lab results received [date] — next step: share with GP at [date] appointment
- Framework build: QUICKSTART.md in progress — draft complete, needs review
```

Without this section, sessions lose mid-task context and require re-explanation.

---

## 6. Custom Slash Command Skills

Repetitive session actions (like a welcome greeting) can be turned into a `/skill-name` command so they fire reliably with one word instead of relying on first-message behavior.

Skills are markdown files stored in `.claude/commands/` — the filename becomes the command name.

```
.claude/
└── commands/
    └── kai.md      ← invoked with /kai
```

Example skill file (`kai.md`):
```markdown
Read SESSION.md and the relevant status files, then greet the user with:

"Welcome back, [name]. Here is a summary of the last X decisions:
1. ...
Suggested starting point: ..."
```

**When to use:** Any repeated action that needs consistent output — session greetings, status reports, project summaries, health check-ins. Store in `.claude/commands/` (gitignored — stays private).

---

## 7. Lazy Loading + Explicit Context Injection

Two complementary patterns for keeping sessions lean as workstreams grow.

**Problem:** Loading all workstream files on every session open wastes context and mixes concerns. A workspace with 4+ workstreams becomes unwieldy fast.

**Pattern A — Lazy loading (keyword-triggered):**
A trigger map file maps keywords to files. When a topic comes up mid-session, the relevant file loads on demand — not upfront.

```markdown
# _meta/TRIGGERS.md

| Keywords / Topics | File to Load |
|---|---|
| home, garden, taxes, deck | `home/status.md` |
| health, supplements, energy | health files |
| template, framework, system | `template/status.md` |
```

**Pattern B — Explicit context injection (skill-triggered):**
A `/open[Name]` skill deliberately loads a workstream when you're ready to focus on it. Shows active work and current priorities. Activates the workstream persona.

```markdown
# .claude/commands/openHomeProjects.md

Read `home/status.md` and `home/project_plan.md`.

Activate Home persona. Then show active work, now priorities, and supply needs.
```

**Combined `/open` flow:**
```
/open               → SESSION.md only (last 5 decisions + workstream menu)
/openHomeProjects   → loads home context + activates home persona
/openHealth         → loads health context + activates health persona
```

**Why both:** Lazy loading handles incidental references ("oh, by the way, what's the status on my deck?"). Explicit skills handle intentional focus shifts ("I want to work on home projects today").

**Scaling rule:** Adding a new workstream = one trigger row + one skill file + one line in the `/open` menu.

---

## 8. Professional Opinions + Iterative Document Review

For knowledge workers who regularly review documents, provide feedback, or craft professional responses — a persistent opinions file combined with versioned draft files creates a repeatable, AI-assisted review workflow.

**Structure:**
```
[workstream]/
├── opinions.md        ← standing professional stances; updated over time, applied to all reviews
└── reviews/
    ├── doc_response_v1.md
    ├── doc_response_v2.md
    └── ...
```

**opinions.md** stores reusable positions on technologies, methodologies, or standards. The AI loads and applies these automatically when doing analysis — no re-explaining required across sessions.

```markdown
## Technology & Methodology Stances

### [Technology Name]
**[Claim or comparison]**
Your position here — the reasoning, the nuance, how strongly held.
Updated as your views evolve.
```

**reviews/** stores versioned drafts of responses and analyses. Each version is a snapshot — iterate freely without losing prior drafts.

**Workflow:**
1. Load the document
2. AI summarizes and asks for your positions on the key claims
3. Positions recorded to opinions.md
4. Draft response generated, saved as v1
5. Iterate — each revision saved as a new version

**When to use:** Document reviews, white paper feedback, technical evaluations, professional correspondence where your stance matters and will recur.

---

*Add new examples here as new patterns are established in practice.*
