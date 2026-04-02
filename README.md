# driftya-search-data

Public data package for Driftya Search.

## Purpose

This repository contains curation data used by the crawler and indexing policy:

- seed websites to bootstrap discovery
- retention inputs for intentionally kept hosts
- domain blocklists
- spam, tool-directory, and SEO phrase patterns
- quality scoring signals

This data package is the policy layer behind Driftya Search. It shapes discovery, scoring, classification, extraction, retained-site behavior, and bounded crawl behavior.

It also provides the knobs for generic low-value external-page exclusion and hard backstops for major social/profile hosts when discovery would otherwise bring in shallow bio pages, link hubs, or similar weak pages.

See [docs/capabilities.md](./docs/capabilities.md) for a higher-level summary of what this repository enables in the engine.

## Layout

- `seed-sites/`: seed URL/domain lists used to bootstrap crawler discovery.
- `seed-sites/locales/<lang>/`: locale-specific seed URL/domain lists.
- `seed-sites/freshness/`: recurring freshness seeds used to refresh timely entry points.
- `seed-sites/freshness/locales/<lang>/`: locale-specific freshness seed overlays.
- `crawler/domain-crawl-policies.json`: default and per-domain crawl page caps, ranking penalties, path/query restrictions, canonical route templates, host fairness batch limits, and host politeness settings.
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
- `classification/domain-priors.json`: domain-level classifier priors for labels and topics.
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
  - `crawler/domain-crawl-policies.json` defines the default host page cap, ranking penalty, per-domain overrides, path allowlists, path blocklists, blocked query keys, canonical route templates for entity pages, host fairness batch limits, and host politeness settings
  - canonical route templates let discovery/listing pages be crawled as feeders while excluding non-canonical utility pages from indexing
  - host politeness settings support per-host delay, jitter, max concurrency, robots crawl-delay honoring, and explicit cooldowns for status codes like `403` and `429`
  - The engine uses this together with host rotation so capped domains stay bounded over time
  - The engine can also distinguish intentionally retained hosts from link-discovered hosts so stale discoveries can be cleaned up without deleting seeded or manually requested sites
- Classification policy:
  - `classification/domain-priors.json` lets trusted domains strongly bias structural classifications such as `WIKIS` or `FORUMS`
  - `classification/negative-signals.json` lets one strong classification demote weaker competing ones such as `WIKIS -> blog`
  - `classification/topic-thresholds.json` prevents topic labels from being emitted on one weak token alone

## Add Seed Sites

Contributions are welcome for small websites, personal blogs, indie projects, niche communities, and other human-made sites that deserve discovery.

If you know a good small site that should help bootstrap search coverage, add it to the seed lists instead of waiting for the crawler to discover it indirectly.

Use the seed folders like this:

- `seed-sites/*.txt`: general seeds that are useful regardless of language or region.
- `seed-sites/locales/<lang>/*.txt`: locale-specific seeds for sites that mainly serve one language or market.
- `seed-sites/freshness/*.txt`: timely sources worth revisiting regularly because they publish new content often.
- `seed-sites/freshness/locales/<lang>/*.txt`: timely sources that are both locale-specific and worth regular refresh.

Freshness and locale solve different problems:

- `freshness` answers "should this source be revisited often because it changes frequently?"
- `locales/<lang>` answers "is this source primarily relevant to a specific language?"

Examples:

- A Swedish personal blog with evergreen posts belongs in `seed-sites/locales/sv/`.
- A global news-style blog that updates often belongs in `seed-sites/freshness/`.
- A Swedish tech news site that publishes frequently belongs in `seed-sites/freshness/locales/sv/`.

## Contributing

Typical flow for seed contributions:

1. Clone the `driftya-search-data` repository.
2. Add or update the relevant seed file under `seed-sites/`.
3. Keep entries lowercase, one per line, and add comments only when they help review.
4. Open a pull request describing why the site should be seeded.

See [CONTRIBUTING.md](CONTRIBUTING.md) for:

- accepted contribution types
- formatting rules for list files
- curation standards and review checks

If you are using AI assistance for curation, follow [AGENTS.md](AGENTS.md).
