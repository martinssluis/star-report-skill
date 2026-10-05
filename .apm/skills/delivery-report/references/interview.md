# Filling gaps

Ask at most 3 questions per message, most critical gap first. Prefer one concrete question to a broad one.

## Questions by gap

| Gap | Question |
|---|---|
| Before | How did the system behave before the change? What did the user see? |
| Technical detail | What exactly changed — code, data model, interface, business rule, architecture? |
| Motivation | What triggered this: a user complaint, an incident, a technical limit, a business request? |
| Objective | What needed to be true at the end for this to count as done? |
| Ownership | Which part was yours, and which was the team's? |
| Alternatives | Did you consider another approach? Why didn't you take it? |
| Impact | What improved after the change — speed, effort, reliability, cost? |

## Hunting for the number

If the result comes only in words ("much faster", "users loved it"), offer candidate metrics and ask which one can be gathered:

| Kind of delivery | Candidate metrics |
|---|---|
| Bug fix | Incidents or tickets before and after, error rate, how many users were affected, time to resolve |
| Performance | Response time (p50, p95), page load, query time, timeouts per day |
| Feature or UX | Steps or clicks saved, task time, adoption, support requests |
| Automation or tooling | Hours saved (uses × time saved per use), manual steps removed |
| Refactor or migration | Build or deploy time, lines or modules removed, cost shut down, incidents after |
| Reusable component | Teams or apps using it, time to adopt |

If no number is available, write the report anyway and add a **To strengthen** item: which number to gather and where to find it (dashboard, logs, ticket system, analytics).

In live mode, many numbers already exist in the session — command timings, test counts, row counts in a query plan. Check the log before asking.

## Red flags in the result

Point these out without dropping the content:

- **Forecast presented as result:** "will save 20 hours a month". Ask how much has been realized; if none yet, write it as expected impact.
- **Percentage without method:** "90% faster". Ask how it was measured.
- **Unmeasured causal link:** "reduced load time, so conversion went up". The load time is a fact; the conversion is a hypothesis unless measured.
- **Team result credited only to the person:** ask which part was theirs.
- **Result without a "before":** "it now takes 2 seconds" says little without the previous value.
