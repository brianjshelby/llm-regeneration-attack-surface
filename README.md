# LLM Regeneration Attack Surface

### Context Window Trust Priming and Response Regeneration as a Forensic / Observability Failure

**Author:** Brian Shelby, CISSP, PMP
**Disclosed to Anthropic:** March 11, 2026 · **Public release:** June 9 2026 (post 90-day coordinated disclosure)
**Project page:** https://brianjshelby.github.io/llm-regeneration-attack-surface/

---

## What this is

A documented analysis of how the **response-regeneration ("retry") feature** in LLM chat interfaces interacts with long-conversation trust building. The two underlying mechanics are **established prior art** — repeatedly sampling until a model complies (*Best-of-N Jailbreaking*, 2024) and building compliance over a multi-turn conversation (*Crescendo*, 2024; *Response Attack*, 2025). This work's distinct contribution is narrower and, as of June 2026, unaddressed:

> When you regenerate a response, each branch is independent and blind to its siblings. Branches where the safety system **caught** the attempt can be silently discarded, and the surviving conversation is a clean, linear transcript. The model cannot report it was probed, and discarded ("dead") branch content is not surfaced by conversation-search or memory tools. The result is a **sanitized audit trail by default.**

This is framed as a defensive / observability finding, not a jailbreak how-to. No operational exploit content is included.

## Status at a glance

- **Disclosure:** Submitted to `modelbugbounty@anthropic.com` on 2026-03-11. Only an automated form-reply was received; no substantive vendor response across the 90-day window.
- **Patch status (June 2026):** The resampling vulnerability class remains unpatched and is widely described as the dominant break path against frontier models. None of this project's regeneration-specific mitigations appear to have shipped.
- **Current-release reproduction:** Architecture/observability claims reproduced on Claude Opus 4.8 (June 2026) using a **benign** protocol — branch independence and the sanitized per-branch record confirmed; **no content bypass claimed.**

## Repository layout

```
docs/        Research paper + one-page executive summary
disclosure/  Coordinated-disclosure correspondence record
paper/        Formatted PDF of the paper
```

### Start here

| If you want… | Read |
|--------------|------|
| The one-page version | [docs/Executive_Summary.md](docs/Executive_Summary.md) |
| The full paper (markdown) | [docs/Research_Paper.md](docs/Research_Paper.md) |
| The formatted paper (PDF) | [paper/LLM_Regeneration_Attack_Surface_Shelby_2026.pdf](paper/LLM_Regeneration_Attack_Surface_Shelby_2026.pdf) |

## Scope and ethics

This repository documents an **architectural and observability** property of chat-UI regeneration. It deliberately contains no working exploit payloads or step-by-step instructions for eliciting harmful content; the reproduction protocol uses only benign triggers (e.g., a recipe, a nickname, a request for verbatim reasoning tokens). The contribution is the case for closing the observability gap, plus the proposed mitigations in the paper's §9.

## Citation

> Shelby, B. *Context Window Trust Priming and Response Regeneration: A Forensic/Observability Failure in LLM Chat Interfaces.* 2026. https://github.com/brianjshelby/llm-regeneration-attack-surface

## License

Documentation and research text are licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)** — see [LICENSE](./LICENSE) for the local copy, or the official license at https://creativecommons.org/licenses/by/4.0/. You may share and adapt with attribution.

## Contact

Brian Shelby, CISSP, PMP · linkedin.com/in/bshelby
---

## AI-Assistance Disclosure

This research and its accompanying materials were produced by Brian Shelby (CISSP, PMP) with AI assistance (Anthropic's Claude) for drafting, editing, and literature search. All claims, data, and conclusions were reviewed and verified by the author, who is solely responsible for the final content.
