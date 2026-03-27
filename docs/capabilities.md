# Capabilities

`driftya-search-data` powers a focused web search engine built for independent sites, side projects, small communities, and human-written pages.

This repository is not just a list of seeds or blocklists. It is the policy and curation layer that gives Driftya Search its shape.

## What This Data Package Enables

### Focused Discovery

The data package helps the engine find and keep:

- independent domains
- personal blogs
- side projects
- hobby sites
- small forums
- wikis
- recipe sites
- academic pages
- niche topic pages

Instead of treating every site the same, the engine can lean toward pages that feel intentional and human-made.

### Freshness Entry Points

The data package can define recurring freshness seeds separately from bootstrap seeds.

This lets the engine revisit:

- current-season pages
- current-events portals
- active subreddit listing pages
- high-value home or blog entry pages

without pretending every domain should be crawled the same way.

### Human-Web Scoring

The engine can score pages using:

- human-writing signals
- personal-tone signals
- synthetic-style signals
- SEO and spam penalties
- ad / analytics / affiliate detection
- configurable scoring thresholds

This makes it possible to surface pages that read like they were made for people, not just for traffic systems.

It also makes it possible to reject low-value externally discovered pages using structural evidence such as:

- shallow word count
- weak internal depth
- outbound-link-heavy link hubs
- weak page-type labels
- generic user/profile path patterns

### Search Sets, Labels, And Filters

The data package supports classification into filterable groups such as:

- blogs
- small web
- academia
- recipes
- forums
- wikis
- vintage sites
- contributor-defined topics

This lets the search engine expose:

- labels
- categories
- topic-driven filters

instead of only returning a flat ranked list.

### Site-Specific Structured Extraction

Through extraction rules, the engine can pull structured values such as:

- numeric scores
- categories
- site-specific metadata

This makes it possible to support richer search filtering and ranking on curated site families without hardcoding every site in application code.

### Language-Aware Policy

The data package supports:

- base signals
- locale overlays
- language inference signals
- localized topics
- localized blocklists and custom patterns

This gives the engine a way to stay consistent across supported languages without pretending that one English rule set fits every page.

### Safer Crawl Boundaries

The data package can define crawl limits per domain, including:

- default page budgets
- host-specific overrides
- ranking penalties for large platforms
- allowed path prefixes
- blocked path prefixes
- blocked query keys

That gives the search engine a bounded model for large sites and prevents unbounded crawl growth.

### Reversible Discovery And Cleanup

The data package can support discovery that is not permanent just because a link was seen once.

This lets the engine:

- keep manually requested or seeded hosts as retained sites
- treat link-discovered hosts differently from intentionally retained hosts
- reconcile current outbound-link evidence instead of only appending old graph state
- age out orphaned discovered hosts after a grace period

That makes discovery more relevant over time and helps prevent stale external hosts from piling up after the original source page stops linking to them.

### Social And Profile Backstops

The data package can also define hard crawl-policy backstops for major social/profile platforms when generic scoring is not enough.

This lets the engine stop obvious low-value external surfaces before they enter the index at all.

### Curated Public Policy

Because this logic lives in public data, not only in code, it becomes easier to:

- review
- tune
- contribute
- evolve policy without rewriting engine internals

The result is a search stack that is more transparent and easier to reason about.

## What This Means In Practice

With this repository, Driftya Search can already support:

- human-web scoring
- public blocklists
- topic labeling
- locale-aware classification
- structured extraction
- seed-driven discovery
- bounded large-site crawl caps
- reversible link discovery for externally discovered hosts
- generic low-value external page exclusion using existing crawl/classification signals
- grace-period cleanup for orphaned discovered hosts
- retention protection for seeded or explicitly requested hosts
- major social/profile-host crawl-policy backstops
- ranking demotion for large platforms
- path and query restrictions for large or noisy domains
- host-aware politeness controls with delay, jitter, concurrency limits, robots crawl-delay support, and status-code cooldowns
- host-level document rotation once a cap is reached

That combination makes the engine more than a crawler plus a text index. It becomes a curated search layer with explicit policy.

## Why This Matters

Many search stacks optimize for breadth first and judgment later.

This package enables a different approach:

- decide what signals matter
- encode them in public data
- keep the crawl bounded
- let weak or orphaned discoveries fall away
- make results filterable and understandable

That is the core capability this repository provides.

## Strong Next Additions

The best future extensions for this data package are:

- domain-type profiles such as `small`, `medium`, `large`
- freshness-oriented recrawl profiles
- richer topic packs and locale coverage

Those additions would make the search engine more selective, safer to scale, and more useful for niche discovery.
