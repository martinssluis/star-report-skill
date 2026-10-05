**English** · [Português](README.pt-BR.md)

# star-report

An agent skill that turns software work into reports you can reuse — in a meeting, an interview, a pull request, or your project's technical history.

The new part: it can **document while you solve the problem**. Start a debugging session or a feature with the skill active and it keeps a session log as the work goes — the reproduced bug, the hypotheses you discarded, the decision you made, the test that proved the fix. When you're done, the log becomes the report. No more reconstructing from memory what you did two weeks ago.

It's written in plain Markdown, in the `SKILL.md` format, and works in **any agent that reads skills** — Claude Code, Claude.ai, GitHub Copilot, Codex, Cursor, and others.

---

## Two modes

| Mode | When | What happens |
|---|---|---|
| **Live** | The problem is being solved now | The skill keeps a session log, updated at milestones, and writes the report at the end |
| **Retrospective** | The work is already done | You describe it informally; the skill asks what's missing and writes the report |

### How live mode works

```
problem reproduced ─► hypothesis tested ─► root cause ─► decision ─► fix applied ─► verified
        │                    │                 │             │            │             │
        └────────────────────┴─────────────────┴── session log ───────────┴─────────────┘
                                                        │
                                                        ▼
                                  STAR · Technical Summary · Technical Decision
```

Updates are quiet: one line at the end of a reply (`📝 Log updated: root cause`). Questions for the report are held until the end — solving the problem comes first. In agents with file access, the log is a Markdown file in your project (by default `docs/deliveries/YYYY-MM-DD-<slug>.md`); in chat interfaces it lives in the conversation.

> A skill is activated by its description or by invoking it. To get live mode, call the skill (or ask to "document as we go") **when you start** the work — it can't reconstruct milestones that happened before it was active, though it will use whatever is already in the conversation.

---

## Formats

| Format | For | Sections |
|---|---|---|
| **STAR** | Interviews, performance reviews, presentations | Situation, Task, Action, Result |
| **Technical Summary** | PRs, commits, changelogs | Problem, Solution, Impact |
| **Technical Decision** (simplified ADR) | Choosing between approaches | Context, Decision, Alternatives, Consequences |

The skill picks the format from context, or asks. One session can produce more than one — a bug hunt makes a good STAR and a good PR description.

---

## Installation

### With apm (recommended)

[apm](https://github.com/microsoft/apm), the Agent Package Manager, installs and updates the skill without copying folders. This repository is an apm package: `apm.yml` at the root and the skill in `.apm/skills/`.

```bash
# install apm if you don't have it
brew install apm                        # macOS
curl -sSL https://aka.ms/apm-unix | sh  # Linux, or macOS without Homebrew
irm https://aka.ms/apm-windows | iex    # Windows, PowerShell

# then, in your project folder
apm install martinssluis/star-report-skill
```

To choose the agent folder explicitly:

```bash
apm install martinssluis/star-report-skill --target claude
apm install martinssluis/star-report-skill --target copilot
apm install martinssluis/star-report-skill --target all
```

**Update:** `apm install --update`. **Remove:** `apm uninstall star-report-skill`. To pin a version: `martinssluis/star-report-skill#v2.0.0`.

### Copying the folder

| Agent | Project folder | Personal folder |
|---|---|---|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Copilot | `.github/skills/` | see the docs |
| Other agents (Codex, Cursor…) | `.agents/skills/` | see the docs |

```bash
git clone https://github.com/martinssluis/star-report-skill.git
mkdir -p .claude/skills
cp -R star-report-skill/.apm/skills/delivery-report .claude/skills/
```

### Claude.ai

Zip the `delivery-report` folder (or download `delivery-report.skill` from the releases) and upload it under **Settings → Capabilities → Skills**.

---

## Usage

**Live**, at the start of the work:

```
/delivery-report
```

or in natural language: *"let's fix this timeout and document it as we go"*, *"track this investigation for a STAR report"*.

**Retrospective:** *"I added multi-select to the label field last week, write it up for my review"*, *"turn this fix into a PR description"*.

The skill writes in the language you write in (English or Portuguese).

---

## Principles

1. **It doesn't invent.** A number or cause without a source becomes `[to confirm]`.
2. **Hypotheses are marked.** The agent's own readings are labeled as such.
3. **Forecast is not result.** "Should save 20 h/month" is written as expected impact, with a **To strengthen** note on what to measure.
4. **Evidence over narrative.** In live mode, every log entry records its source: observed output, your statement, or a hypothesis.
5. **Discarded hypotheses are kept.** "What didn't work" is often the most convincing part of an interview answer.
6. **Internal information can stay out.** For interviews or public use, the skill offers a version without internal system names, clients, or confidential numbers.

---

## Repository structure

```
star-report-skill/
├── apm.yml
├── README.md / README.pt-BR.md
└── .apm/skills/delivery-report/
    ├── SKILL.md                 # flow and rules (read by the agent)
    ├── README.md / README.pt-BR.md
    ├── references/
    │   ├── formats.md           # the three formats, with examples
    │   ├── live-mode.md         # tracking a session as it happens
    │   └── interview.md         # gap questions, metrics, red flags
    └── templates/
        └── session-log.md       # the working file in live mode
```

The files the agent reads (`SKILL.md`, `references/`, `templates/`) are in English, which models follow most consistently. Reports come out in the user's language.

## Contributing

Issues and PRs are welcome. When changing the skill, keep the `name` in `SKILL.md` equal to the folder name, bump `version` in `apm.yml`, and update both READMEs.

Structure inspired by [skills-protagonista](https://github.com/dudscode/skills-protagonista).

by [@martinssluis](https://github.com/martinssluis)
