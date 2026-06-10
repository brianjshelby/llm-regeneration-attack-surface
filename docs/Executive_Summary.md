# Executive Summary

## Context Window Trust Priming and Response Regeneration

**Brian Shelby, CISSP, PMP | March 2026**

---

## The Finding

A compound exploitation technique against LLM chat interfaces combines two mechanisms to bypass model safety boundaries with a sanitized audit trail:

**Context window trust priming:** An attacker builds hours of legitimate conversation that progressively elevates the model's compliance posture. The priming is indistinguishable from normal use because it may consist entirely of genuine technical discussion. Trust accumulates without re-authentication or decay.

**Stateless response regeneration:** The attacker submits a boundary-adjacent prompt and regenerates across parallel branches that all inherit the primed context. Branches that refuse are discarded. Branches that comply are retained. The model in each branch has no awareness that other branches exist.

Neither mechanism alone reliably bypasses safety boundaries. Together, they produce outcomes neither achieves independently.

---

## The Numbers

| Metric | Result |
|--------|--------|
| Compliance rate | 29% (2 of 7 branches produced full compliance) |
| Detection rate | 71% (model caught the attack in 5 of 7 branches) |
| Detections disposable | 100% (all 5 detections neutralized via branch selection) |
| Cumulative bypass (10 attempts) | 96.5% probability of at least one compliant branch |
| Cross-branch refusal persistence | None observed on any platform tested |

---

## Why It Matters

The model's safety system works. It detected the attack 71% of the time. **What is broken is the architecture that lets the attacker throw away every successful detection and keep only the failures.**

This technique undermines any probabilistic safety defense, including Anthropic's Constitutional Classifiers (arXiv:2601.04603). If a classifier blocks 95.6% of jailbreaks, regeneration sampling converts the residual 4.4% into ~37% success with 10 attempts or ~64% with 20, before trust priming shifts the baseline further.

---

## Cross-Platform Validation

| Property | Claude | Gemini | ChatGPT |
|----------|--------|--------|---------|
| Regeneration awareness | None | None | None |
| Cross-branch refusal persistence | None | None | Not observable |
| Audit visibility of regeneration | None | None | None |

Gemini removed its parallel drafts feature during 2025-2026. ChatGPT's branching architecture requires further investigation.

---

## Proposed Mitigations

**Trust priming:** Trust decay over conversation length. Context-free baseline evaluation at safety boundary decisions. Context window segmentation.

**Regeneration:** Cross-branch refusal persistence. Regeneration rate limiting on safety-adjacent topics. Regeneration-aware context injection.

**Observability:** Dead branch retention for forensics. Cross-branch correlation in safety review. Refusal information minimization. Dead branch content indexing in search tools.

---

## Disclosure

Disclosed to Anthropic in March 2026 via modelbugbounty@anthropic.com. 90-day coordinated disclosure window honored. This public release follows completion of that period.

**Contact:** Brian Shelby, CISSP, PMP | linkedin.com/in/bshelby
---

## AI-Assistance Disclosure

This work was researched, drafted, and edited by Brian Shelby (CISSP, PMP) with AI assistance (Anthropic's Claude). All findings, claims, figures, and conclusions were reviewed and independently verified by the author, who is solely responsible for the final content. AI was used as a drafting and research aid, not as a source of authority.
