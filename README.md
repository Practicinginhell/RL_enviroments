# AI-Native Project Template

A universal starting point for **any** software project — web, mobile, desktop, CLI,
ML/LLM, game, or backend — designed so AI coding agents (Claude Code, Codex, Gemini
CLI, Cursor, Copilot, and whatever ships next) are first-class collaborators from
commit one. It contains no application code: it is the knowledge and control structure
you wrap *around* your code.

## The core idea

Agents fail for predictable reasons: they guess commands, miss project conventions,
re-propose rejected designs, and declare "done" without proof. This template gives
every failure mode a designated home, in **one tool-agnostic layer** with **thin
per-tool adapters** — so adopting a new AI tool costs one pointer file, not a
migration.

| Layer | Question it answers | Where | Loaded |
| --- | --- | --- | --- |
| **Global AI instructions** | How should any agent behave here? | `AGENTS.md` (adapters: `CLAUDE.md`, `GEMINI.md`, `.github/copilot-instructions.md`) | Always |
| **Project context** | What must an agent know about *this* system? | `ai/context/` | On demand, per the policy in `AGENTS.md` |
| **Reusable skills** | What procedures can the agent apply — or a human invoke as `/name`? | `.claude/skills/` (portable SKILL.md format; slash commands are skills now) | When the task matches the skill's description, or on `/name` |
| **Prompts** | How does a human ask an agent to do X well? | `ai/prompts/` | When a human invokes one |
| **Templates** | What shape should this artifact take? | `ai/templates/` | When creating a spec/ADR/bug report/skill |
| **Checklists** | How is "done" proven? | `ai/checklists/` | At verification gates |
| **Documentation** | What do humans need to understand/operate this? | `docs/` | Read by people; optional for agents |
| **Working memory** | What is the agent doing right now / what has it learned? | `tasks/` | Per task / per session |
| **Uniform commands** | How do you build/test/run this, regardless of stack? | `scripts/` | Called by agents and CI alike |

## Full layout

```
.
├── AGENTS.md                     # ★ Canonical agent instructions — edit behavior HERE, once
├── CLAUDE.md                     # Claude Code adapter: imports AGENTS.md + Claude-only notes
├── GEMINI.md                     # Gemini CLI adapter: imports AGENTS.md
├── README.md                     # This file — for humans adopting the template
├── .editorconfig                 # Whitespace baseline shared by humans, editors, agents
├── .env.example                  # Documents env var NAMES (never values); copy → .env
├── .gitignore                    # Excludes secrets, local agent settings, build output
├── .mcp.json                     # Project MCP servers — external tools shared with the team
│
├── .claude/                      # Claude Code adapter (executable config)
│   ├── settings.json             # Shared permissions: pre-approves ./scripts/*, denies .env reads
│   ├── settings.local.json.example  # Copy → settings.local.json for personal overrides (gitignored)
│   ├── agents/                   # Subagents with their own context window
│   │   ├── code-reviewer.md      #   reviews diffs against project conventions
│   │   └── test-runner.md        #   runs/diagnoses/fixes the test suite
│   └── skills/                   # Auto-triggered procedures AND typed /name workflows
│       ├── wire-stack/           #   wire scripts/* to a chosen stack (adoption step 1)
│       ├── update-context/       #   keep ai/context + AGENTS.md map matching the code
│       ├── write-adr/            #   record a structural decision in docs/adr/
│       ├── capture-lesson/       #   turn a user correction into a rule in tasks/lessons.md
│       ├── checklist/            #   /checklist <name> — verify change vs ai/checklists/<name>.md
│       ├── plan/                 #   /plan <task> — user-invoked plan before code
│       ├── new-skill/            #   author the next skill (trigger-description craft)
│       └── example-skill/        #   annotated placeholder — delete when it's served its purpose
│
├── .github/
│   ├── copilot-instructions.md   # Copilot adapter: points to AGENTS.md
│   ├── PULL_REQUEST_TEMPLATE.md  # Verification evidence + AI-assistance disclosure
│   └── workflows/ci.yml          # CI calls the same ./scripts/* agents use (wire, then enable)
│
├── ai/                           # ★ Tool-agnostic AI knowledge base (plain Markdown)
│   ├── README.md                 # Taxonomy + authoring rules for this directory
│   ├── context/                  # PROJECT CONTEXT — loaded on demand
│   │   ├── architecture.md       #   system map, components, invariants, links to ADRs
│   │   ├── domain.md             #   glossary: the one true name for each concept
│   │   └── conventions/          #   per-concern rules
│   │       ├── code-style.md     #     what formatters can't enforce
│   │       ├── testing.md        #     the agent's feedback loop, kept trustworthy
│   │       ├── git-workflow.md   #     branches, commits, agent guardrails
│   │       └── security.md       #     hard rules + defaults at trust boundaries
│   ├── prompts/                  # PROMPTS — human-invoked, work in any tool
│   │   ├── explore-codebase.md   #   build an accurate mental model before changing code
│   │   ├── debug-issue.md        #   root-cause discipline, not patch roulette
│   │   ├── refactor-safely.md    #   behavior-preserving restructuring
│   │   ├── write-tests.md        #   coverage that can actually fail
│   │   ├── review-diff.md        #   merge-blocking problems only, before human review
│   │   └── fan-out-audit.md      #   one subagent per unit, evidence-checked, one table
│   ├── templates/                # TEMPLATES — shapes to fill in
│   │   ├── feature-spec.md       #   spec whose acceptance criteria = definition of done
│   │   ├── adr.md                #   decision record (final home: docs/adr/)
│   │   ├── bug-report.md         #   a report an agent can act on with zero follow-ups
│   │   └── skill.md              #   scaffold for new .claude/skills/
│   └── checklists/               # CHECKLISTS — gates passed with evidence
│       ├── pre-merge.md          #   definition of done for every change
│       ├── security-review.md    #   extra gate for trust-boundary changes
│       └── release.md            #   extra gate for shipping
│
├── docs/                         # HUMAN documentation
│   ├── adr/                      # Architecture Decision Records (0001 included)
│   └── runbooks/                 # operational procedures (empty; shape documented)
│
├── tasks/                        # Agent WORKING MEMORY (committed, shared)
│   ├── todo.md                   # per-task plans: goal → steps → verify → review
│   └── lessons.md                # corrections turned into rules; skimmed each session
│
├── scripts/                      # UNIFORM VERBS — wire these to your stack first
│   ├── setup / dev / test / lint / format / build
│   └── README.md                 # the contract each wrapper must honor
│
├── src/                          # your code (placeholder — restructure freely)
└── tests/                        # your tests (placeholder — or co-locate and delete)
```

## How the tools plug in

One canonical file, thin adapters — supporting a new tool never means duplicating
rules:

| Tool | Reads | Wiring in this template |
| --- | --- | --- |
| Claude Code | `CLAUDE.md`, `.claude/` | `CLAUDE.md` imports the canon via `@AGENTS.md` |
| OpenAI Codex | `AGENTS.md` | Native — no adapter needed |
| Gemini CLI | `GEMINI.md` | Imports the canon via `@AGENTS.md` |
| Cursor | `AGENTS.md` | Native — no adapter needed |
| GitHub Copilot | `.github/copilot-instructions.md` | Pointer to `AGENTS.md` |
| Future tools | `AGENTS.md` | Add one pointer file if the tool doesn't read it natively |

The `@AGENTS.md` import is Claude Code's officially documented pattern for AGENTS.md
repos (a symlink works too, but the import lets `CLAUDE.md` carry Claude-only notes).
Claude Code's `/import` command can also copy another tool's config in one shot when
migrating an existing repo onto this layout.

`AGENTS.md` itself has two halves: **project facts** (snapshot, command table,
repository map, context-loading policy — you fill these in) and a **working contract**
(think before coding, surgical changes, verification before done — travels with the
template unchanged).

## Design principles

1. **One source of truth per fact.** Behavior rules live in `AGENTS.md`; project
   knowledge in `ai/context/`; adapters only point. Duplicated instructions drift,
   and drifted instructions are worse than none.
2. **Context is budgeted.** Always-on files stay small; depth is filed where the
   loading policy can pull it on demand. That's why `ai/context/` is many small files,
   not one big one.
3. **Commands are verbs, not incantations.** Agents and CI both call `./scripts/*`;
   the stack behind them can change without any instruction file changing.
4. **"Done" requires evidence.** Checklists and the PR template demand command output,
   not confidence.
5. **Knowledge upkeep is part of every change.** The pre-merge checklist makes
   updating `AGENTS.md` / `ai/context/` / ADRs a gated step, so the map keeps matching
   the territory.
6. **Fail loud until configured.** Script stubs exit 1 and `TODO:` markers flag
   unfilled sections, so an agent can't mistake template boilerplate for project truth.

## Adopting the template

1. **Copy the repo** (or use it as a GitHub template). Delete `implementation_plan.md`
   if present — and anything else that isn't yours.
2. **Wire `scripts/`** to your stack — this unlocks agents, CI, and half the
   checklists. Then enable the push/PR triggers in `.github/workflows/ci.yml`.
3. **Fill the Project Snapshot** in `AGENTS.md` (running your tool's `/init` and
   distilling the result works well).
4. **Seed `ai/context/`**: one honest paragraph in `architecture.md`, your first five
   glossary terms in `domain.md`, and stack-specific rules in `conventions/`.
5. **Tune the guardrails**: permissions and hooks in `.claude/settings.json` (hooks
   for anything that must happen every time — e.g. format-after-edit), MCP servers in
   `.mcp.json`, and the git rules in `ai/context/conventions/git-workflow.md`.
6. **Write your first skill** from `ai/templates/skill.md` for the task you repeat
   most; delete `example-skill/`.
7. **Put code in `src/`** (restructure freely — then update the Repository Map in
   `AGENTS.md` and `ai/context/architecture.md`).
8. **Let it evolve**: corrections → `tasks/lessons.md`; decisions → `docs/adr/`;
   recurring lessons get promoted into `AGENTS.md` or `ai/context/conventions/`.

### Driving the agent (Claude Opus 5.5)

Adapted from [Getting the most out of Opus 5.5](https://claude.dev/blog/getting-the-most-out-of-opus-5-5/).
The agent-side rules are already in `AGENTS.md` §4, §5, §7 and §9. These tips are for
the human at the keyboard:

- **Send the whole task in one message, with a finish line** ("Done means: …"). Leave
  out "think hard"; the model already decides how much to reason.
- **Add to a running task instead of restarting it.** A follow-up message ("also keep
  the old names as aliases") gets folded into the current run.
- **Read the end of a long run from the top:** the *Needs from you* block first, then
  the rest. For progress in the middle of a run, read `tasks/todo.md`.
- **Attach screenshots and diagrams** instead of describing them in words.
- **Fast mode** (`/fast`) is worth it when you review every reply before sending the
  next one. It costs more tokens.
- **If a message is flagged** and the session switches to an older model: switch back
  with `/model`, or press Esc twice to edit and retry. Set auto-switching in
  `/config`, and report a wrong flag with `/feedback`.

### Scaling up

- **Monorepo:** keep this structure at the root; add a nested `AGENTS.md` (plus
  `CLAUDE.md`/`GEMINI.md` pointer) per package for package-specific rules — most tools
  merge nested instruction files, nearest-first.
- **Personal vs shared:** everything committed here is team-shared. Personal agent
  config belongs in `~/.claude/` (global) or `.claude/settings.local.json`
  (per-machine, gitignored) — never fork shared files for personal taste.
- **More gates:** new recurring artifact → `ai/templates/`; new recurring procedure →
  a skill; new class of mistake → one checklist item. Resist growing `AGENTS.md`;
  it's the always-loaded budget.
- **Reuse across repos:** once your `.claude/` setup stabilizes, package it as a
  Claude Code plugin (skills + agents + hooks in one installable unit) so other repos
  get it via `/plugin` instead of copy-paste.
