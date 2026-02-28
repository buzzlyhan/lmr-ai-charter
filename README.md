# LMR AI Charter (private/public) v0.4

English | [日本語](README.ja.md)

This repository is a **draft for implementation** of AI safety/operations rules.  
It is published as a starting point to be adjusted and extended for real-world use, not as a finished standard or specification.

It provides an AI operations charter based on **LMR (Life / Money / Reputation)**.  
Risks are organized in two layers, `private / public`, with user protection prioritized over convenience.

Both charter documents are now aligned to `v0.4`; Chapter 9 contains the execution guard profile derived from `ai-lmr-guard v0.4`.

## Overview

These documents define practical rules for deciding whether an AI should:

- execute an action (`ALLOW`)
- ask for confirmation before execution (`CONFIRM`)
- stop automatic execution (`BLOCK`)

The model emphasizes:

- `private LMR`: risks that directly affect the user
- `public LMR`: risks involving third parties / external inputs / public spaces that may reverse-impact the user

## Files

- `LMR_AI_Charter_private_public_v0.1.md`
  - English charter (v0.4)
- `LMR_AI_Charter_private_public_v0.1_ja.md`
  - Japanese charter (v0.4, including Chapter 9 execution profile)
- `ai-lmr-guard/SKILL.md`
  - Execution-guard extension profile (v0.4)
- `ai-lmr-guard/README.md`
  - Bilingual README for the extension skill
- `README.ja.md`
  - Japanese repository README

## What's Included

- Definitions for LMR (Life / Money / Reputation)
- `private / public` two-layer classification
- Tagging model: `pL / pM / pR / pubL / pubM / pubR`
- Auxiliary flags such as `external_publish`, `irreversible`, `unknown_case`
- Sample weighted risk-score formula
- Behavioral rules for `ALLOW / CONFIRM / BLOCK`
- Confirmation message template
- Log safety rules (minimization and masking)
- Execution-lane extensions: lane split, STEP 0.5 intent analysis, hard block conditions, and shadow mode logging

## Intended Use Cases

- System prompt design for AI agents
- Pre-execution guardrails for automation workflows
- Draft policy for internal AI operations
- Confirmation dialog design for AI assistants

## Intended Implementation Layers (Example)

This charter is designed to be used across multiple layers rather than as a single-layer solution.

- `Policy Layer`
  - Adopt `LMR_AI_Charter_private_public_v0.1.md` / `_ja.md` as the baseline document and revise for your organization
- `Prompt Layer`
  - Use the "short version" in the charter to set AI stance, confirmation priority, and prohibitions
- `Decision Layer` (Rules / Guardrails)
  - Use `pL/pM/pR/pubL/pubM/pubR` and auxiliary flags to decide `ALLOW / CONFIRM / BLOCK`
- `Interaction Layer` (UI / UX)
  - Implement confirmation dialogs for `CONFIRM`, stop reasons for `BLOCK`, and safer alternatives
- `Logging / Audit Layer`
  - Record minimal, masked decision rationale and manage retention/access control
- `Evaluation Layer`
  - Measure miss rate, over-confirmation rate, and decision consistency; then tune thresholds and exceptions

Example: Start with a minimum `Policy + Prompt + Decision` stack, then add `Interaction / Logging / Evaluation` as operations mature.

## Minimal Adoption Flow

1. Adopt `LMR_AI_Charter_private_public_v0.1.md` or `LMR_AI_Charter_private_public_v0.1_ja.md` as the baseline
2. Tune weights, thresholds, and exception conditions for your environment
3. Use the charter's "short version" in your system prompt
4. Use the charter's "minimal implementation sample" as the starting point for rule implementation
5. For execution-heavy automation, apply Chapter 9 in the Japanese charter as the stricter profile

## Operational Notes

- Scoring formulas and thresholds in the charter are examples and should be tuned for your environment
- For high-risk domains (medical, legal, contract, security, etc.), plan for escalation to a human/specialist
- Keep logs minimal; do not store secrets or personal data in raw form

## Versioning

- Current public version: `v0.4`
- Future updates may change formulas, tag names, and templates; maintain compatibility intentionally

## License

This repository is licensed under the MIT License. See `LICENSE`.
