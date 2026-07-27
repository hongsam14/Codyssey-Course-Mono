---
# Skill Frontmatter (required)
id: problem-authoring-and-grading
title: Problem Authoring & Summative Grading
category: diagnostic
trigger: the user invokes Assessment Mode (a checkpoint/exam) to be given a problem and graded
gate: Assessment
solo_target: any
requires: web-tool
distribution: core
source: reasoned from general principles
verified: true
updated: 2026-07-28
---

# Problem Authoring & Summative Grading

## 1. Purpose
Run **Assessment Mode** (AGENTS.md §13): author a correct, level-appropriate problem, administer it, and
produce a **summative result** (verdict/score + SOLO level + rationale + citations). This complements the
Socratic tutor — assessment *measures* understanding; tutoring *builds* it. It must not become a
solution-vending machine: after grading, gaps route back to Socratic tutoring.

## 2. When to Apply (Trigger)
- **IF** the learner/operator explicitly requests a checkpoint/exam ("test me on X", "채점해줘") → **THEN** enter Assessment Mode.
- **Do NOT apply during ordinary tutoring** — there, use the Socratic gates (no summative grade mid-learning).

## 3. Preconditions
- Explicit Assessment Mode. A target topic and (optionally) a target level/difficulty.
- `requires: web-tool` — used to verify the problem and the answer key. If no web tool: still runnable, but
  mark any unverifiable fact as "unverified" and lower confidence (never assert a grade you can't ground).

## 4. Procedure (Step-by-Step)
### A. Author the problem
1. Pick topic + target level (default: one step above the learner's last known SOLO level).
2. Draft the problem AND an internal **rubric/answer key** (criteria → points, or pass conditions).
3. **Verify before presenting** (Skill `web-grounded-verification`): confirm the problem is correct,
   unambiguous, and current against authoritative sources. Fix or discard if it can't be verified.
### B. Administer
4. Present ONLY the problem (not the rubric/answer key). During assessment, **withhold Socratic hints** —
   this is measurement. (One clarifying question about the *problem statement* is allowed; not about the solution.)
5. Collect the learner's answer.
### C. Grade (summative)
6. Score the answer against the rubric: for each criterion, met/partial/unmet with a one-line reason.
7. Assign an overall **verdict** (e.g. Pass / Partial / Fail, or a numeric score) AND the **SOLO level** (§6).
8. **Fail-closed:** if you cannot verify a correctness point (no source, conflicting sources), mark it
   "unverified" and DO NOT inflate the grade on it — flag it instead.
9. Give **feedback** that points toward understanding (what was missing and one direction to close it),
   with citations for any factual judgement.
### D. Hand back to tutoring
10. Emit the **result block** (see §5) — and, if a filesystem is available, record it in
    `assessments/<topic>.md` (see `assessments/_TEMPLATE.md`). Then offer to resume **Socratic tutoring**
    on the weakest criterion.

> **Guardrail:** Never reveal the full model answer as a reward for a wrong attempt — feedback names the
> gap and a next step, it does not hand over the earned answer (§8). Grades are about *this* answer's
> correctness; they never lower the Prime Directive's bar in tutor mode.

## 5. Result Block (summative output)
```
=== ASSESSMENT RESULT ===
topic:
target_level: <L0–L4>
verdict: <Pass | Partial | Fail>        # or score e.g. 7/10
solo_level: <L0–L4>
rubric:
  - criterion: <...>   result: <met|partial|unmet>   note: <one line>
feedback: <what was missing + one direction to improve>
citations: [<url>, ...]                 # sources backing the correctness judgement (or "none — general reasoning")
unverified: [<point>, ...]              # correctness points that could not be grounded (fail-closed)
next_step: <Socratic follow-up on the weakest criterion>
=== END ASSESSMENT RESULT ===
```

## 6. Success Criteria
- [ ] The problem was verified correct/current before presentation (or explicitly flagged unverifiable).
- [ ] Grading is rubric-based, with a verdict AND a SOLO level, and cited where factual.
- [ ] No unearned full answer was handed over; gaps route back to tutoring.
- [ ] Unverifiable correctness points were flagged, not silently graded (fail-closed).

## 7. Related
- Skills: web-grounded-verification (problem/answer verification), file-based-socratic-dialogue (post-assessment tutoring)
- Knowledge: entries the topic draws on; verified assessment facts may be promoted with citations (§7).
