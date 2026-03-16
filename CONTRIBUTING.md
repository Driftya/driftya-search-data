# Contributing To driftya-search-data

Thank you for helping curate Driftya Search data.

## What To Contribute

- `seed-sites/*.txt`
  - Add small-web, indie, personal blog, and human-made project seeds.
- `blocklists/domains.txt`
  - Add domains that are clearly low-quality SEO/tool farms.
- `blocklists/*.txt` phrase files
  - Add high-confidence patterns for spam or tool-directory SEO content.
- `classification/*.txt`
  - Add quality signals for human-writing or SEO detection.
- `docs/*.md`
  - Improve curation policy clarity.

## What Not To Contribute

- Generic word bans like `ai`, `marketing`, `revenue`, `promotion`.
- Personal disagreements with normal content categories.
- Political/ideological filtering unrelated to search quality.
- Copyrighted content dumps.

## File Rules

- One entry per line.
- Use lowercase where practical.
- Keep lines concise and specific.
- Use `#` for comments.
- Avoid duplicates.
- For domains:
  - `example.com` for exact/parent domain matching.
  - `*.example.com` for wildcard intent.

## Quality Standard

Contributions should improve precision:

- Prefer phrase-pattern targeting over broad keyword bans.
- Prefer domain-level blocks for proven farm behavior.
- Use scoring signals to reduce false positives.
- Keep changes minimal and justified.

## Pull Request Checklist

- Describe why this change is needed.
- Include examples of pages/domains that motivated the change.
- State possible false-positive risks.
- Confirm that entries are specific and non-generic.
- Update docs when policy intent changes.

## Review Criteria

Maintainers and AI curators evaluate:

- Precision: does this avoid blocking legitimate small-web writing?
- Coverage: does this address the spam pattern effectively?
- Transparency: is intent clear from file placement and wording?
- Maintainability: is the rule understandable in 6+ months?
