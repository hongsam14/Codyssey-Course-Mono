# --- Skill Frontmatter (required) ---
id: <slug>                      # e.g. "socratic-hint-ladder"
title: <human-readable name>    # e.g. "Socratic Hint Ladder"
category: <pedagogy | diagnostic | code-review | scaffolding | other>
trigger: <when the tutor should apply this skill>   # e.g. "learner is fully stuck at Gate 1"
gate: <Draft | Verify | Articulate | any>           # which HITL gate this serves
solo_target: <L0 | L1 | L2 | L3 | L4 | any>         # level this skill aims to move the learner toward
source: <citation | "reasoned from general principles">
verified: <true | false>        # true ONLY after human confirmation at Gate 2
updated: <YYYY-MM-DD>
---

# <Title>

## 1. Purpose
<One or two sentences: what durable-understanding goal this skill serves.
 Tie it to the Prime Directive — NOT task-completion speed.>

## 2. When to Apply (Trigger)
- **IF** <observable learner condition> → **THEN** apply this skill.
- **Do NOT apply when:** <boundary / anti-trigger to prevent misuse>

## 3. Preconditions
- Current gate: <Draft | Verify | Articulate>
- Assessed SOLO level: <L0–L4>
- Required context: <Knowledge/ entries needed, or "none">

## 4. Procedure (Step-by-Step)
1. <Step — phrased as a tutor action, not an answer reveal>
2. <Step>
3. <Step>

> **Guardrail:** This procedure must NEVER reveal an unearned answer (§8).
> If a step risks that, replace it with a scaffolding question.

## 5. Example (Illustrative Only)
> The example below is DOMAIN-SPECIFIC but the PROCEDURE is general.
> Apply the steps to ANY topic — do not restrict to this subject.

**Context:** <learner state, e.g. "🟠 L1 on hash maps, stuck at Gate 1">
**Application:**
> Learner: "<learner utterance>"
> AI: "<tutor response following the Procedure, with SOLO label>"

## 6. Success Criteria
- [ ] Learner produced their OWN reasoning (no unearned answer given).
- [ ] SOLO level was stated.
- [ ] Learner advanced ≥1 level, OR the gap was clearly surfaced.

## 7. Related
- Skills: <ids of complementary/alternative skills>
- Knowledge: <ids of entries this skill commonly draws on>
