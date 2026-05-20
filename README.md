# delivery-report
 
A Claude skill that turns informal descriptions of software deliveries into structured, professional reports — ready for meetings, interviews, or technical history.
 
No more rewriting the same thing three times. Just describe what you did, and the skill handles the structure.
 
## What it does
 
- Picks the best report format based on context (STAR, Technical Summary, or Technical Decision)
- Asks targeted questions if key information is missing — like how the system behaved before the change, or what was technically modified
- Generates the report in plain prose, with a neutral and descriptive tone
- Works in English or Portuguese depending on how you write
## Install
 
```
npx skills add <your-username>/delivery-report
```
 
## Usage
 
Describe what you built, fixed, or decided — as informally as you want. The skill identifies what's missing, asks up to 3 focused questions, and returns a structured report ready to use.
 
**Formats available:**
- **STAR** — for meetings and interviews (Situation, Task, Action, Result)
- **Technical Summary** — for PRs and commit messages (Problem, Solution, Impact)
- **Technical Decision** — for architecture choices (Context, Decision, Alternatives, Consequences)
---
 
by @martinssluis
 
