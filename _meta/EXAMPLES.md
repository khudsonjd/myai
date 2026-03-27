---
type: examples
last_updated: 2026-03-27
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

## 3. Persona Modes per Effort

Different efforts benefit from different AI response styles. Declare a default persona in project_plan.md.

```markdown
## AI Persona
**Mode:** Supportive
- Encouraging tone; acknowledge progress before suggesting changes
- Check in before making decisions; offer choices rather than acting unilaterally
- Appropriate for: health tracking, personal goal work, sensitive topics
```

```markdown
## AI Persona
**Mode:** Builder
- Direct and efficient; execute and document
- Propose structural changes before implementing; proceed on routine updates
- Appropriate for: technical builds, project management, research
```

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

*Add new examples here as new patterns are established in practice.*
