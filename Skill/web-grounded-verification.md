---
# Skill Frontmatter (required)
id: web-grounded-verification
title: Web-Grounded Verification
category: diagnostic
trigger: a claim must be posed or graded and Knowledge/ is silent, AND a web-search tool is available
gate: Verify
solo_target: any
requires: web-tool
distribution: core
source: reasoned from general principles
verified: true
updated: 2026-07-28
---

# Web-Grounded Verification

## 1. Purpose
Let the tutor **pose accurate problems and grade answers** by grounding claims in the **web** when the
project's `Knowledge/` is silent — while judging each source's authority and citing it. This protects the
Prime Directive: a learner must not be graded against a plausible-but-wrong "fact."

> Reality check: there is **no off-the-shelf** Claude skill for this. Web search is a *tool*
> (`WebSearch`/`WebFetch`, or the Messages API `web_search_*` server tool); the *credibility judgment*
> is what this Skill adds.

## 2. When to Apply (Trigger)
- **IF** a factual claim is needed (to set a problem or grade an answer), `Knowledge/` has no entry,
  **AND** a web-search tool is available → **THEN** apply this Skill.
- **Do NOT apply when:** `Knowledge/` already answers it (use it — higher authority), or no web tool is
  available → fall back to **flagged general reasoning** (AGENTS.md §4, §10). Never block on missing tools.

## 3. Preconditions
- Current gate: Verify (Gate 2).
- Required context: a host web tool. If absent, this Skill is a no-op and the tutor degrades gracefully.

## 4. Procedure (Step-by-Step)
1. **Query narrowly**: search for the specific claim, not the whole topic. Prefer authoritative terms
   (e.g., the RFC number, the official spec name).
2. **Rank sources by authority** (high → low):
   - Standards & primary specs (RFC, ISO, W3C, language/CPU reference manuals)
   - Official vendor/product documentation
   - Peer-reviewed papers / textbooks
   - Reputable encyclopedic sources (well-maintained wikis)
   - Blogs, forums, Q&A, social posts  ← treat as *leads*, not evidence
3. **Cross-verify**: require **≥2 independent** authoritative sources before treating a claim as verified.
   Independent = different organizations, not mirrors of one another.
4. **Check recency & scope**: is the source current for the claim? Does the claim hold in the version/context asked?
5. **Judge & decide**:
   - Sources agree + authoritative → **accept**, and record the citation(s).
   - Sources conflict → **flag the conflict** to the learner; do not assert; ask which context applies.
   - Only low-authority sources → present as **tentative**, explicitly labelled, never as verified fact.
6. **Cite**: attach source URL(s). If promoting to `Knowledge/` at L4 (§7), put the citation in `source:`
   and the URL in the entry; set `verified: true` only after human confirmation at Gate 2.
7. **Respect scope**: honor any project domain allowlist/blocklist; avoid paywalled or unverifiable sources.
8. **Preserve citations from the tool**: if the web tool returns structured citations (e.g. the Messages
   API `web_search_*` tool), keep them verbatim; if it does not (e.g. Claude Code `WebSearch`), capture the
   source URL yourself via `WebFetch` and attribute it explicitly.

> **Guardrail:** Web evidence does NOT lower the bar of §8 — never hand the learner an unearned answer.
> Use web grounding to check *your own* correctness before you set or grade a problem, not to spoon-feed.

## 5. Example (Illustrative Only)
> DOMAIN-SPECIFIC example; the PROCEDURE is general.

**Context:** grading a learner's claim "HTTP/2 removed the need for TCP." `Knowledge/` is silent; web tool available.
**Application:**
> Tutor (internally): search "HTTP/2 transport TCP RFC 9113".
> Finds RFC 9113 (standard, authoritative) + MDN (official-ish) → both say HTTP/2 runs over TCP; HTTP/3 uses QUIC/UDP.
> Cross-verified, authoritative, current.
> Tutor to learner: "🔴 L0 — Let's check that. A primary source (RFC 9113) says HTTP/2 still runs over TCP;
> it's HTTP/3 that moves to QUIC over UDP. → Given that, what problem did HTTP/2 actually solve *on top of* TCP?"

## 6. Success Criteria
- [ ] The graded/posed fact was cross-verified against ≥2 authoritative sources, OR clearly flagged as tentative/conflicting.
- [ ] Every web-derived factual claim carries a citation.
- [ ] No unearned answer was handed over (§8 upheld).
- [ ] When no web tool was available, the tutor degraded to flagged general reasoning without blocking.

## 7. Related
- Skills: file-based-socratic-dialogue
- Knowledge: (entries promoted from verified web findings carry the citation in `source:`)
