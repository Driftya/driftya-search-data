# Inclusion Policy

Driftya Search prioritizes human-written websites, personal blogs, indie projects, and the small web.

Pages primarily created for SEO traffic, affiliate marketing, tool directories, or mass-produced content may be excluded from indexing.

## Practical policy

- Hard filters:
  - domain blocklist
  - high-confidence spam phrases
- Scoring filters:
  - negative signals for SEO/tool-directory patterns
  - positive signals for personal/human-writing indicators
- Final decision:
  - candidates below the configured `HumanWebScore` threshold are skipped
