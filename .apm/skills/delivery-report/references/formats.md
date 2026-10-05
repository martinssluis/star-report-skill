# Report formats

Pick by where the report will be used. When more than one fits, write the one the user asked for and offer the others at the end.

| Format | Use for | Voice | Sections |
|---|---|---|---|
| STAR | Interviews, performance reviews, team presentations | First person (or "we", confirmed) | Situation, Task, Action, Result |
| Technical Summary | PR descriptions, detailed commits, changelogs | Impersonal | Problem, Solution, Impact |
| Technical Decision (simplified ADR) | A choice between approaches | Impersonal | Context, Decision, Alternatives considered, Consequences |

Section headings stay in the user's language. In Portuguese: Situação, Tarefa, Ação, Resultado · Problema, Solução, Impacto · Contexto, Decisão, Alternativas consideradas, Consequências.

## STAR

A narrative that justifies the problem, the person's choices, and the impact.

- **Situation:** the context and the problem, with scale (how many users, transactions, teams).
- **Task:** what was the person's responsibility — not the team's.
- **Action:** what the person did and decided, including what they ruled out. In live mode, a discarded hypothesis often makes this section more convincing than the fix itself.
- **Result:** before and after, with a number whenever one exists.

### Example

**S — Situation**

During a feedback meeting with users, I learned that the application required running the full flow several times to add different pieces of information to the same process. To add three labels, a user had to run the application three times.

**T — Task**

My goal was to remove that repetition, so the user could select several items in a single run.

**A — Action**

I refactored the subject, label, and reminder fields to accept lists of values instead of a single value, and updated the interface to allow multiple selections before confirming. I considered keeping single values and adding a "repeat last run" shortcut, but it would have kept the extra runs and only made them faster.

**R — Result**

Adding three labels went from three runs to one. Users now complete the process in a single flow, and the list-based fields made it simpler to add new multi-value fields later.

## Technical Summary

A quick record for whoever reviews or maintains the code.

### Example

**Problem**

The label, subject, and reminder fields accepted only one value at a time, so adding several pieces of information required running the full flow repeatedly.

**Solution**

The fields were refactored to store lists of values, and the interface was updated to allow multiple selections before confirming the update.

**Impact**

Several items can now be added in a single run. Adding three labels went from three runs to one.

## Technical Decision (simplified ADR)

For when the delivery involved choosing one approach over others. In live mode, use the **Decisions** section of the log.

### Example

**Context**

The monthly report export was timing out for accounts with more than 50 thousand orders. Profiling showed the query, not the PDF rendering, was responsible: it filtered by creation date with no index, scanning about 4 million rows.

**Decision**

A composite index on account and creation date was added to the orders table.

**Alternatives considered**

Caching the generated report was evaluated and discarded, because it would hide the slow query, serve stale data after new orders, and still time out on the first request of each month.

**Consequences**

The export dropped from 31 seconds to 1.9 seconds. Writes to the orders table carry the small cost of maintaining one more index, which should be watched if insert volume grows significantly.
