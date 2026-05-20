---
name: delivery-report
description: >
  Use this skill whenever the user wants to document a software feature, bug fix, technical decision, or any development delivery as a structured report. Triggers include: "document this feature", "write a STAR report", "log what I did", "write a delivery report", "help me describe this for an interview", "document this for a meeting", or any informal description of something built or fixed in a software context. Even if the user doesn't mention a specific format, if they are describing something they implemented or solved, consider using this skill. The goal is to turn informal descriptions into clear, professional, reusable documentation — for meetings, interviews, or technical history.
---

# Skill: Software Delivery Report

Turns informal descriptions of features, bug fixes, and technical decisions into structured, professional reports written in plain prose.

---

## Available formats

Pick the format that best fits the context before generating the report. If it's not clear from the user's description, ask.

### 1. STAR (for meetings and interviews)
Best when the user wants to explain a delivery as a narrative — justifying the problem, the solution, and the impact. Widely used in technical interviews and team presentations.

- **S — Situation:** context and problem identified
- **T — Task:** what needed to be solved
- **A — Action:** what was implemented and how
- **R — Result:** impact on the user or system

### 2. Technical Summary (for PRs and commits)
Best for quick technical records, pull request descriptions, or detailed commit messages.

- **Problem:** what was broken or missing
- **Solution:** what was implemented
- **Impact:** what changes for the user or system

### 3. Technical Decision (simplified ADR)
Best when the user made an architecture decision or chose one approach over alternatives.

- **Context:** why the decision needed to be made
- **Decision:** what was chosen
- **Alternatives considered:** what else was evaluated (if any)
- **Consequences:** what changes as a result

---

## Workflow

### Step 1 — Identify the format
Based on what the user described, choose the most appropriate format. If the user didn't specify and the context isn't clear, ask directly and simply.

### Step 2 — Map available information
Read what the user provided and identify which components of the chosen format are already covered and which are missing or unclear.

### Step 3 — Ask for what's missing
If any essential component is missing, ask short and direct questions. Never ask more than 3 questions at once. Prioritize the most critical gaps.

**Two pieces of information must always be investigated if not provided:**
- **Before behavior:** How did the system behave before this change? What did the user see or experience?
- **Technical details of the solution:** What exactly was changed — code structure, data model, interface, business logic, architecture?

**Other common gaps and how to ask:**
- Missing problem/situation → "What motivated this change? Was there a user complaint or a technical limitation?"
- Missing impact → "What improved after the implementation? Did something become faster, easier, or more reliable?"
- Missing objective → "What was the main goal that needed to be achieved?"

### Step 4 — Generate the report
With enough information, generate the report in **plain prose** — no bullet points, no tables. Each section flows as a natural paragraph.

---

## Writing rules

- **Plain prose always:** no lists, no bullet points, no tables. Each section is a paragraph.
- **Neutral and descriptive tone:** like a technical report. No inflated adjectives, no marketing language. Facts speak for themselves.
- **First person when narrative:** "The solution was to...", "The goal was to...", "After the implementation..."
- **No unnecessary jargon:** if technical terms are used, make sure they are contextualized.
- **Language:** respond in the same language the user is writing in.

---

## Example output — STAR format

**S — Situation**

During a feedback meeting with users, it was identified that the application required running the full flow multiple times to add different information to the same process. To add three labels, for example, the user had to run the application three times.

**T — Task**

The goal was to eliminate that repetition, allowing the user to select multiple items in a single run and making the flow more efficient and intuitive.

**A — Action**

The subject, label, and reminder fields were refactored to support lists of values instead of a single value. The interface was updated to allow multiple selections before confirming the update.

**R — Result**

Users can now add multiple groups of information in a single flow, eliminating the need for repeated runs. The experience became more fluid and the application gained cohesion and better scalability for future needs.

---

## Example output — Technical Summary format

**Problem**

The label, subject, and reminder fields accepted only one value at a time, forcing the user to run the full flow repeatedly to add multiple pieces of information.

**Solution**

The fields were refactored to support lists of values. The interface was updated to allow multiple selections before confirming the update.

**Impact**

Users can now add multiple items in a single run, reducing friction and improving the overall experience of the application.
