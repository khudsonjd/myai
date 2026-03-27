# AI Project Template

A lightweight, file-based system for managing projects with an AI assistant — Claude, GitHub Copilot, or any AI with file access.

## What This Is

A small set of markdown files that give your AI assistant persistent context across sessions. Instead of re-explaining your project every time you open a chat, the AI reads a few files and picks up where you left off.

Works for any kind of project: home improvement, software development, research, business planning, or anything else you want to manage with AI assistance.

## How It Works

- `SESSION.md` — the AI reads this at the start of every session to orient itself
- `project_plan.md` — stable reference data that rarely changes
- `status.md` — current state: priorities, deadlines, what's next
- The AI updates `status.md` as you work, so the next session starts with accurate context

## Getting Started

1. Copy `_template/SESSION.md` and `_template/project_plan.md` into a new folder
2. Create a `status.md` (see `_meta/PROCESS.md` for the minimum sections)
3. Fill in what you know — leave the rest blank and let your AI help you build it out
4. Open a chat, share `SESSION.md`, and start working

Full setup guide: [`_meta/PROCESS.md`](_meta/PROCESS.md)

## Repository Contents

```
├── _template/              ← copy these to start a new project
│   ├── SESSION.md
│   └── project_plan.md
└── _meta/                  ← process documentation
    ├── PROCESS.md          ← how to set up and run a project
    ├── DECISIONS.md        ← why the system is structured this way
    ├── IMPROVEMENTS.md     ← lessons learned and recommendations
    └── presentation.html   ← overview presentation (open in browser)
```

## Philosophy

- **Minimal setup** — one project name and a description is enough to start
- **AI-agnostic** — plain markdown files work with any AI tool
- **Persistent context** — the AI stays oriented across sessions without you re-explaining anything
- **Evolves with use** — the template improves as you use it; `_meta/IMPROVEMENTS.md` captures lessons as they happen

## License

MIT
