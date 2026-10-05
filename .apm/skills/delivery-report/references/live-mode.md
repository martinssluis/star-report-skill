# Live mode: documenting while the problem is solved

In live mode the report is written alongside the work, not reconstructed from memory at the end. You keep a **session log** — raw notes with evidence — and update it at milestones. When the work is done, the log becomes the final report.

The log and the report are different things. The log is a working file: short entries, lists allowed, every fact with its source. The report is prose, written once, at the end, from the log.

## 1. Start

Ask in one message, and only what you can't infer:
- What is being solved (one sentence is enough — you'll refine it).
- Where the log should live. If you have a filesystem, suggest `docs/deliveries/YYYY-MM-DD-<short-slug>.md` in the project and ask whether that folder should be committed or added to `.gitignore`. Without a filesystem (a chat interface), keep the log in the conversation.
- The intended format, if the user already knows (interview, PR, decision). If not, decide at the end.

Create the log from [../templates/session-log.md](../templates/session-log.md) and fill in what you already know.

Then get back to the actual problem. **Solving it is the priority; documenting is secondary.** Don't ask report questions in the middle of a debugging session unless the answer will be lost if you don't ask now (for example, a metric only visible on a dashboard the user has open).

## 2. Milestones that update the log

Update the log when one of these happens — not on every message:

| Milestone | What to record | Feeds |
|---|---|---|
| Problem stated or reproduced | Symptom, who is affected, how to reproduce, error message, scale | Situation, Before |
| Hypothesis tested | What was suspected, how it was checked, result. **Keep discarded hypotheses** | Action (investigation), the "what didn't work" story |
| Root cause found | The cause and the evidence that confirms it | Situation, Action |
| Decision between alternatives | Options, what was chosen, why, trade-off accepted | Action, Technical Decision |
| Change applied | Files or components touched, what changed in behavior | Action, Solution |
| Verified | Test, command, or measurement that proves it works; before and after numbers | Result, Impact |
| Scope change | What was added or dropped, and why | Task |

Each entry records its **source**: `(observed: test output)`, `(observed: diff)`, `(user said)`, or `(hypothesis)`. This is what lets the final report avoid inventing anything.

## 3. How updates appear in the conversation

Updates are quiet. After updating, add at most one line at the end of your normal reply, for example:

> 📝 Log updated: root cause (missing index on `orders.created_at`).

In Portuguese: `📝 Registro atualizado: causa raiz (índice ausente em orders.created_at).`

Without a filesystem, don't paste the whole log every time. Paste it only when the user asks, at the close, or every few milestones as a compact snapshot so it isn't lost in a long conversation.

## 4. Gaps found along the way

When you notice a gap that matters for the report (no "before" number, unclear whose part was whose), add it to the log's **Open questions** section instead of asking right away. Ask them at the close, at most 3, most critical first.

## 5. Close

Close when the user says the work is done, when verification passes and the user moves on, or when they ask for the report. Then:

1. Show the open questions (max 3) and wait. If the user skips them, mark the gaps `[to confirm]`.
2. Pick the format, following [formats.md](formats.md). A session with a decision between alternatives often deserves a Technical Decision as well; a bug hunt with discarded hypotheses makes a good STAR for interviews.
3. Write the report in prose, following the writing rules in SKILL.md. Use the log as the only source of facts.
4. Save the report: in a file, append it under **Final report** in the same log, so evidence and narrative stay together. Without a filesystem, deliver it in the reply.
5. List what's `[to confirm]` and the **To strengthen** items, and offer the other formats and the anonymized version.

## 6. Interrupted sessions

If the conversation ends before the close, the log is still useful. When the user returns ("let's finish the report for that fix"), read the existing log, ask what happened since, and continue from the milestone where it stopped.

## Example of a log in progress

```markdown
## Timeline
- **10:12 · Problem reproduced** — Export of the monthly report times out after 30 s for accounts with more than 50k orders. (observed: curl output, 504)
- **10:25 · Hypothesis discarded** — Suspected the PDF rendering. Timing showed rendering takes 0.8 s; the query takes 31 s. (observed: profiler)
- **10:40 · Root cause** — Query filters by `created_at` with no index; full table scan on 4M rows. (observed: EXPLAIN)
- **10:52 · Decision** — Composite index `(account_id, created_at)` instead of caching the report. Cache would hide the problem and go stale. (user said)
- **11:05 · Verified** — Same export now takes 1.9 s. (observed: curl timing)

## Open questions
- How many clients hit this timeout? Was there a support ticket?
```
