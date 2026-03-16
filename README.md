# driftya-search-data

Public data package for Driftya Search.

## Purpose

This repository contains curation data used by the crawler and indexing policy:

- seed websites to bootstrap discovery
- domain blocklists
- spam, tool-directory, and SEO phrase patterns
- quality scoring signals

## Layout

- `seed-sites/`: seed URL/domain lists used to bootstrap crawler discovery.
- `blocklists/domains.txt`: domains to hard-block from indexing.
- `blocklists/spam-phrases.txt`: high-confidence spam phrase rules.
- `blocklists/tool-directory-patterns.txt`: phrases correlated with AI/tool directory SEO farms.
- `blocklists/seo-patterns.txt`: generic SEO-farm phrase patterns.
- `classification/human-writing-signals.txt`: positive human-web signals.
- `classification/seo-signals.txt`: negative SEO signals.
- `docs/inclusion-policy.md`: inclusion/exclusion philosophy.
- `CONTRIBUTING.md`: how to submit changes.
- `AGENTS.md`: AI curator workflow and review rules.

## Notes

- Keep entries lowercase when possible.
- One entry per line.
- Lines starting with `#` are comments.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for:

- accepted contribution types
- formatting rules for list files
- curation standards and review checks

If you are using AI assistance for curation, follow [AGENTS.md](AGENTS.md).
