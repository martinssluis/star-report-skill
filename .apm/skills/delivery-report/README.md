**English** · [Português](README.pt-BR.md)

# Skill `delivery-report`

An agent skill that turns software deliveries into structured reports in plain prose — **live**, while the problem is being solved, or **retrospectively**, from an informal description.

- **STAR** for interviews, reviews, and presentations.
- **Technical Summary** for PRs and commits.
- **Technical Decision** (simplified ADR) when one approach was chosen over others.

## Installation

```bash
apm install martinssluis/star-report-skill
```

Or copy this folder to where your agent reads skills (`.claude/skills/` in Claude Code, `.agents/skills/` in most others). The [repository README](../../../README.md) has every option.

## Usage

At the start of the work, for live mode:

```
/delivery-report
```

Or: *"let's fix this and document it as we go"*. For something already done: *"write up the cache fix I did yesterday as a STAR"*.

In live mode the skill asks what's being solved and where to keep the log, then goes back to the problem. At each milestone — reproduced, hypothesis tested, root cause, decision, fix, verified — it updates the log and adds one line to the reply. At the end it asks up to 3 questions, writes the report, and lists what is **[to confirm]** and what to measure (**To strengthen**).

## What it promises not to do

- **Not invent numbers, causes, or dates.** Anything without a source becomes `[to confirm]`.
- **Not present forecasts as results.**
- **Not interrupt debugging** with report questions; they wait until the close.
- **Not keep internal names** in a report you'll share outside the company, if you ask for the anonymized version.

## Structure

```
delivery-report/
├── SKILL.md                 # flow and rules
├── references/
│   ├── formats.md           # formats, voice, and full examples
│   ├── live-mode.md         # milestones, quiet updates, closing
│   └── interview.md         # gap questions, candidate metrics, red flags
└── templates/
    └── session-log.md       # live-mode working file
```
