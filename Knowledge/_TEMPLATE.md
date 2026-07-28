---
# Knowledge Frontmatter (required)
id: <slug>                      # e.g. "tcp-reliability"
title: <human-readable name>    # e.g. "TCP Reliability Guarantees"
category: <concept | fact | pattern | pitfall | reference | other>
mastery_level: <L0 | L1 | L2 | L3 | L4>   # SOLO depth at which this was verified
source: <citation | "reasoned from general principles">
verified: <true | false>        # true ONLY after human confirmation at Gate 2
authored_by: <learner | tutor>  # prefer "learner" at L4 (§7: deepens retention)
updated: <YYYY-MM-DD>
related_skills: [<skill-id>, ...]   # Skills that draw on this entry
provenance: <dialogue/<topic>.md | none>   # back-link to the dialogue that produced it (§12)
---

# <Title>

## 1. Claim (Verified Fact)
<The single core fact/concept, stated precisely in ONE or TWO sentences.
 This is the citable "source of truth" (§4, highest authority).>

## 2. Why It's True (Grounding)
<The reasoning or mechanism behind the claim.
 IF source is a citation → summarize what the source establishes.
 IF "reasoned from general principles" → make that flag EXPLICIT here (§4).>

## 3. Boundary Conditions
- **Holds when:** <context where this claim is valid>
- **Breaks when:** <edge cases / exceptions / trade-off situations>

## 4. Connections (Relational)
<How this concept links to others — cause/effect, trade-off, sequence.
 This section is what separates L3+ understanding from L2 lists (§6).>
- Relates to: <other Knowledge id> — <nature of the link>

## 5. Transfer (L4 Marker)
<Only filled when mastery_level: L4.
 A generalization or cross-domain analogy showing the principle transfers.>
> Example: "reliability-vs-latency is a general trade-off, like RAID mirroring."

## 6. Provenance
- **Reached via:** Gate 3 (Articulate) on <YYYY-MM-DD>
- **Verified at:** Gate 2 by <human | pending>
- **Dialogue:** <dialogue/<topic>.md | none>
- **Original learner articulation:** "<quote, if authored_by: learner>"
