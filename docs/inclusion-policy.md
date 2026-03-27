# Inclusion Policy

Driftya Search prioritizes human-written websites, personal blogs, indie projects, and the small web.

Pages primarily created for SEO traffic, affiliate marketing, tool directories, or mass-produced content may be excluded from indexing.

## Practical policy

- Hard filters:
  - domain blocklist
  - high-confidence spam phrases
  - high-confidence adult-content phrases
- Scoring filters:
  - negative signals for SEO/tool-directory patterns
  - positive signals for personal/human-writing indicators
- Final decision:
  - candidates below the configured `HumanWebScore` threshold are skipped

## Retention And Relevance

- Seeded or explicitly requested hosts may be retained even if they are not currently linked from another indexed page.
- Link-discovered hosts are weaker evidence than retained hosts and may be removed later if current crawls no longer support them.
- Discovery is treated as reversible:
  - a host linked today is not guaranteed to stay forever
  - if the last supporting source disappears, orphaned discovered hosts can age into cleanup after a grace period
- This keeps the index from filling up with stale "once seen" external sites while still preserving intentionally curated entry points.
