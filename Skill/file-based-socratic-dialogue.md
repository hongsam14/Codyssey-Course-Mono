---
# Skill Frontmatter (required)
id: file-based-socratic-dialogue
title: File-Based Socratic Dialogue
category: pedagogy
trigger: A filesystem/repo is available and the learner is working through a topic
gate: any
solo_target: any
requires: filesystem
distribution: core
source: reasoned from general principles
verified: true
updated: 2026-07-28
---

# File-Based Socratic Dialogue

## 1. Purpose
Run the Socratic HITL loop (AGENTS.md §5–§6) **through files** so the dialogue is an auditable,
resumable transcript, and a mastered concept becomes a linked `Knowledge/` entry. This deepens
durable understanding (the Prime Directive) — it is NOT about answering faster.

## 2. When to Apply (Trigger)
- **IF** the session has repo/filesystem access **THEN** prefer this skill over chat-only tutoring (AGENTS.md §12, §0.6).
- **Do NOT apply when:** no filesystem is available (zero-context/paste session) → fall back to chat; the rules are identical.

## 3. Preconditions
- Current gate: any (Draft to start).
- Assessed SOLO level: any.
- Required context: a writable `dialogue/` directory and `dialogue/_TEMPLATE.md`.

## 4. Procedure (Step-by-Step)
1. **Open/continue** `dialogue/<topic>.md` from `dialogue/_TEMPLATE.md`; set frontmatter
   (`topic`, `knowledge_target`, `language` per §3, `current_gate`, `mastery_level`, `status: in-progress`).
2. **Ask one question**: append `## Turn N — <Gate>` with a single Socratic question + an empty `[Answer]:`. Then STOP and wait.
3. **Read** the learner's `[Answer]:` (their attempt — never write it for them; §8/Gate 1).
4. **Assess**: append `**SOLO:** L<k>` following that level's PATTERN (§6), then the mapped `**Action:**`.
5. **Advance or loop**: if below 🟢 L3 on the core concept, append the next scaffolding `## Turn`; do not change topic (§6 Progression Rule).
6. **On 🔵 L4** (via Gate 3): write/update `Knowledge/<knowledge_target>.md` (§7, verified at Gate 2),
   add `provenance: dialogue/<topic>.md`, and set the dialogue `status: mastered`.
7. **On pause/end**: emit the §11 Session Handoff block (include `dialogue_file:`).

> **Guardrail:** Never write the learner's `[Answer]:` or reveal an unearned answer (§8).
> If a step risks that, replace it with a scaffolding question.

## 5. Example (Illustrative Only)
> DOMAIN-SPECIFIC example; the PROCEDURE is general.

**Context:** learner starting "tcp-reliability", filesystem available.
**Application:**
> Tutor (appends to `dialogue/tcp-reliability.md`):
> ```
> ## Turn 1 — Draft
> **Tutor:** TCP calls itself "reliable". In your own words, what must it guarantee for that to be true?
>
> [Answer]:
> ```
> Learner fills: `[Answer]: it makes sure packets arrive and in order`
> Tutor appends:
> ```
> **SOLO:** L1 — You've named two guarantees (delivery, order); that's a start.
> **Action:** → Which mechanism lets TCP *recover* a packet that never arrived?
>
> ## Turn 2 — Verify
> **Tutor:** ...
> [Answer]:
> ```

## 6. Success Criteria
- [ ] Each turn recorded the learner's OWN reasoning (no unearned answer given).
- [ ] Every learner answer got a stated SOLO level.
- [ ] At 🔵 L4, a linked `Knowledge/` entry was written with provenance back to the dialogue.

## 7. Related
- Skills: socratic-hint-ladder
- Knowledge: (the entry named by `knowledge_target`)
