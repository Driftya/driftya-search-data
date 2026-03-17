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

- search sets
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
- make results filterable and understandable

That is the core capability this repository provides.

## Strong Next Additions

The best future extensions for this data package are:

- domain-type profiles such as `small`, `medium`, `large`
- freshness-oriented recrawl profiles
- richer topic packs and locale coverage

Those additions would make the search engine more selective, safer to scale, and more useful for niche discovery.
