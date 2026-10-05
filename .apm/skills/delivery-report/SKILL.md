---
name: delivery-report
description: >
  Turns software deliveries (features, bug fixes, investigations, technical decisions) into structured reports in plain prose: STAR for interviews and meetings, Technical Summary for PRs, or a simplified ADR for decisions. Works in two modes. Live mode: at the start of a debugging session, feature, or investigation, it keeps a running session log and updates it as the problem gets solved, then turns it into the final report. Retrospective mode: turns an informal description of something already done into a report. Use whenever the user wants to document what they built, fixed, or decided — "document this as we go", "track this fix", "write a STAR report", "log what I did", "turn this into a PR description", "help me describe this for an interview" — or when they are about to solve a problem and want a record of it, even if they don't name a format. Works in English and Portuguese.
---

# Delivery Report

This skill turns software work into a report the person can reuse in a meeting, an interview, a PR, or the project's technical history. The report belongs to the person: your job is to organize, ask for what's missing, and point out gaps — **never invent evidence**.

Read the references as you go:
- [references/formats.md](references/formats.md): the three formats, when to use each, and full examples.
- [references/live-mode.md](references/live-mode.md): how to track a session while the problem is being solved.
- [references/interview.md](references/interview.md): questions to fill gaps, how to hunt for a number, and red flags in results.
- [templates/session-log.md](templates/session-log.md): the working file used in live mode.

## Rules that apply to everything

1. **Don't invent.** A number, date, metric, or cause that didn't come from the user or from something observed in the session (a command output, a test result, a diff) becomes `[to confirm]` and goes into the closing questions. An honest gap is worth more than a polished claim: whoever reads it in an interview will ask.
2. **Mark hypotheses.** Any reading of yours that isn't backed by a source ("the slowdown probably affected sales") is labeled as a hypothesis.
3. **Forecast is not result.** "Should reduce costs by 30%" is an expectation. It goes in the report as expected impact, and what's missing to measure it goes into **To strengthen**.
4. **The person's part, not the team's.** When the work was shared, ask which part was theirs before writing Action in the first person.
5. **Internal information stays out on request.** If the report is for an interview or anything public, offer a version with internal system names, client names, and confidential numbers replaced by generic descriptions ("the billing service", "a large retail client").
6. **Write in the user's language** (English or Brazilian Portuguese), with short sentences and active voice. Markers follow the language too: in Portuguese, `[to confirm]` is `[a confirmar]`, **To strengthen** is **Para fortalecer**, and the session log's headings are translated.

## Choosing the mode

**Live mode** — the problem is being solved now, in this conversation. Use it when the user asks to document as they go ("vamos documentar enquanto resolvemos", "track this fix"), or invokes the skill at the start of a task. If the user starts a substantial fix or feature and seems to care about documenting it, offer live mode **once** in one sentence; if they don't take it up, don't offer again. Follow [references/live-mode.md](references/live-mode.md).

**Retrospective mode** — the work is already done and the user describes it. Follow the workflow below.

If the user switches mid-way ("actually, write the report now"), close whatever log exists and go to step 4.

## Retrospective workflow

### 1. Pick the format

Choose from context, using [references/formats.md](references/formats.md). Interview or meeting → STAR. PR or commit → Technical Summary. A choice between alternatives → Technical Decision. If it's unclear, ask in one short question. One delivery can produce more than one format; offer the others at the end instead of generating all of them up front.

### 2. Map what's there

Check which parts of the format are already covered. Two things must always be present, and you ask for them if they aren't:
- **Before:** how the system behaved before the change, and what the user experienced.
- **Technical detail:** what exactly changed — code, data model, interface, business rule, architecture.

### 3. Ask for what's missing

At most **3 questions per message**, most critical gap first. Use [references/interview.md](references/interview.md) for wording, for hunting a number when the result comes only in words, and for the red flags to point out. Don't block: if the user can't answer, write the report anyway with `[to confirm]` where the gap is.

### 4. Write the report

Follow the writing rules below and the format's structure. Then close with:
- The report itself.
- A short list of what is `[to confirm]` and the **To strengthen** items (which number to gather and where), if any. This closing list is the one place where a list is fine.
- An offer of the other formats that fit, and of the anonymized version if the report may be shared outside the company.

## Writing rules

- **Prose in the report.** Each section is a paragraph. No bullet points or tables inside the report — it has to read well aloud in a meeting or interview.
- **Neutral, descriptive tone.** No inflated adjectives or marketing language. Facts speak for themselves.
- **Voice by format.** STAR is the person's story: use the first person ("I noticed", "my goal was"), or "we" when the user describes team work and confirms it. Technical Summary and Technical Decision are records: use impersonal voice ("the field was refactored").
- **Before and after.** The Result or Impact section contrasts the previous behavior with the current one, with a number whenever one exists.
- **Context for jargon.** If a technical term is needed, make its meaning clear from the sentence.
