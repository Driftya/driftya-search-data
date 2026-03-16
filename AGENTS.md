# AI Curation Agent Guide

This file defines how AI agents should curate contributions in this data repo.

## Primary Objective

Improve search quality for human-made, small-web content while minimizing false positives.

## Decision Principles

- Do not ban broad generic words (`ai`, `marketing`, `revenue`, `promotion`).
- Prefer targeted phrase patterns for known SEO/tool-directory templates.
- Prefer domain-level blocks for repeat offender farms.
- Favor scoring signals over hard bans when uncertainty exists.
- Keep policy explainable and auditable.

## Review Workflow

1. Identify contribution type:
   - seed addition
   - blocklist domain
   - phrase pattern
   - classification signal
2. Validate specificity:
   - Is the entry precise?
   - Could it block legitimate personal writing?
3. Classify confidence:
   - `high`: clear spam/farm pattern
   - `medium`: likely low quality but possible edge cases
   - `low`: uncertain, needs human review
4. Recommend action:
   - accept
   - accept with edits
   - reject with reason
5. Document rationale in PR comments.

## Heuristic Examples

- High-confidence negative patterns:
  - `submit your ai tool`
  - `top ai tools`
  - `buy followers`
  - `casino bonus`
- Risky broad patterns (avoid):
  - `ai`
  - `marketing`
  - `tools`

## Output Format For Reviews

When AI reviews a PR, provide:

- `Decision`: accept / edit / reject
- `Confidence`: high / medium / low
- `Reason`: short explanation
- `Risk`: possible false positives
- `Suggested patch`: optional line edits

## Safety Rules

- Never add discriminatory or protected-class targeting rules.
- Never include private personal data.
- Avoid political censorship rules unrelated to quality/spam.
- Escalate uncertain policy changes for human maintainer approval.
