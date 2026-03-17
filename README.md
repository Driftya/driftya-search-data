# driftya-search-data

Public data package for Driftya Search.

## Purpose

This repository contains curation data used by the crawler and indexing policy:

- seed websites to bootstrap discovery
- domain blocklists
- spam, tool-directory, and SEO phrase patterns
- quality scoring signals

This data package is the policy layer behind Driftya Search. It shapes discovery, scoring, classification, extraction, and bounded crawl behavior.

See [docs/capabilities.md](./docs/capabilities.md) for a higher-level summary of what this repository enables in the engine.

## Layout

- `seed-sites/`: seed URL/domain lists used to bootstrap crawler discovery.
- `seed-sites/locales/<lang>/`: locale-specific seed URL/domain lists.
- `seed-sites/freshness/`: recurring freshness seeds used to refresh timely entry points.
- `seed-sites/freshness/locales/<lang>/`: locale-specific freshness seed overlays.
- `crawler/domain-crawl-policies.json`: default and per-domain crawl page caps, ranking penalties, path/query restrictions, canonical route templates, and host politeness settings.
- `blocklists/domains.txt`: domains to hard-block from indexing.
- `blocklists/spam-phrases.txt`: high-confidence spam phrase rules.
- `blocklists/adult-content-patterns.txt`: high-confidence adult-content phrases (hard exclusion).
- `blocklists/tool-directory-patterns.txt`: phrases correlated with AI/tool directory SEO farms.
- `blocklists/seo-patterns.txt`: generic SEO-farm phrase patterns.
- `blocklists/locales/<lang>/`: locale-specific overlays for domain and phrase blocklists.
- `blocklists/custom-patterns/*.txt`: user-contributed extra negative patterns.
- `blocklists/locales/<lang>/custom-patterns/*.txt`: locale-specific custom negative patterns.
- `classification/human-writing-signals.txt`: positive human-web signals.
- `classification/personal-tone-signals.txt`: positive personal/conversational writing hints.
- `classification/synthetic-style-signals.txt`: combination signals for generic synthetic writing style risk.
- `classification/seo-signals.txt`: negative SEO signals.
- `classification/ad-signals.txt`: ad/adtech detection hints.
- `classification/analytics-signals.txt`: analytics/tracking detection hints.
- `classification/affiliate-signals.txt`: affiliate/referral detection hints.
- `classification/blog-signals.txt`: blog classification hints.
- `classification/smallweb-signals.txt`: small-web classification hints.
- `classification/academia-signals.txt`: academia classification hints.
- `classification/recipe-signals.txt`: recipe classification hints.
- `classification/forum-signals.txt`: forum classification hints.
- `classification/wiki-signals.txt`: wiki classification hints.
- `classification/vintage-signals.txt`: vintage web classification hints.
- `classification/topics/index.txt`: index of contributor-defined topic ids.
- `classification/topics/<topic>.txt`: base patterns for contributor-defined topic labels.
- `classification/languages/<lang>/topics/<topic>.txt`: locale overlays for topic patterns.
- `classification/classification-settings.json`: classification thresholds.
- `classification/domain-priors.json`: domain-level classifier priors for search sets and topics.
- `classification/negative-signals.json`: negative classifier adjustments that suppress weak competing classifications.
- `classification/topic-thresholds.json`: minimum score and distinct-evidence requirements for topic labels.
- `classification/label-groups.json`: canonical label groups and aliases emitted during crawl/classification.
- `classification/scoring.json`: policy scoring weights/thresholds.
- `classification/synthetic-style-settings.json`: length-aware thresholds for synthetic-style combination penalties.
- `classification/languages/<lang>/language-signals.txt`: language inference hints (used when page language is missing).
- `classification/languages/<lang>/personal-tone-signals.txt`: locale-specific first-person and conversational writing hints.
- `classification/languages/<lang>/synthetic-style-signals.txt`: locale-specific synthetic-style writing hints.
- `extraction/rules/index.txt`: grouped rule file manifest.
- `extraction/rules/*.yaml`: grouped extraction rule files (for example `movie-rules.yaml`).
- `docs/extraction-rules.md`: extraction rule schema and examples.
- `docs/capabilities.md`: summary of search-engine capabilities enabled by this data package.
- `docs/inclusion-policy.md`: inclusion/exclusion philosophy.
- `CONTRIBUTING.md`: how to submit changes.
- `AGENTS.md`: AI curator workflow and review rules.

## Notes

- Keep entries lowercase when possible.
- One entry per line.
- Lines starting with `#` are comments.
- Localized variants should be added in language folders:
  - `classification/languages/<lang>/<base>`
  - Example: `classification/languages/sv/blog-signals.txt`
- Topic signals:
  - Add topic id to `classification/topics/index.txt`
  - Add patterns in `classification/topics/<topic>.txt`
  - Optional locale overlays in `classification/languages/<lang>/topics/<topic>.txt`
- Locale site/blocklist overlays:
  - `seed-sites/locales/<lang>/*.txt`
  - `blocklists/locales/<lang>/*.txt`
  - `blocklists/locales/<lang>/custom-patterns/*.txt`
- Structured extraction rules:
  - Prefer grouped files in `extraction/rules/*.yaml` and list them in `extraction/rules/index.txt`
  - Use `role: "score"` to map site-specific ratings to generic `score`
  - Use `role: "category"` to emit filterable categories
- Crawl policy:
  - `crawler/domain-crawl-policies.json` defines the default host page cap, ranking penalty, per-domain overrides, path allowlists, path blocklists, blocked query keys, canonical route templates for entity pages, and host politeness settings
  - canonical route templates let discovery/listing pages be crawled as feeders while excluding non-canonical utility pages from indexing
  - host politeness settings support per-host delay, jitter, max concurrency, robots crawl-delay honoring, and explicit cooldowns for status codes like `403` and `429`
  - The engine uses this together with host rotation so capped domains stay bounded over time
- Classification policy:
  - `classification/domain-priors.json` lets trusted domains strongly bias structural classifications such as `WIKIS` or `FORUMS`
  - `classification/negative-signals.json` lets one strong classification demote weaker competing ones such as `WIKIS -> blog`
  - `classification/topic-thresholds.json` prevents topic labels from being emitted on one weak token alone

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:

- accepted contribution types
- formatting rules for list files
- curation standards and review checks

If you are using AI assistance for curation, follow [AGENTS.md](AGENTS.md).
