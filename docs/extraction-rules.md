# Extraction Rules

Grouped extraction files are preferred:

- `extraction/rules/index.txt` (manifest)
- `extraction/rules/*.yaml` (rule groups, for example `movie-rules.yaml`)

## Rule Shape

```yaml
rules:
  - id: imdb-title-rating
    hostSuffixes: [imdb.com]
    pathPrefixes: [/title/]
    fields:
      - key: imdb_rating
        selector: .rating-selector
        valueKind: number
        pattern: "(?<value>\\d+(?:\\.\\d+)?)"
        role: score
        multiplier: 10.0
        clampMin: 0.0
        clampMax: 100.0
      - key: movie_category
        selector: .genre a
        valueKind: list
        role: category
```

YAML is the supported format for grouped rule files.

## Field Options

- `key`: stable field id.
- `selector`: CSS selector (AngleSharp).
- `valueKind`: `string`, `number`, or `list`.
- `valueSource`: `text` (default) or `attribute`.
- `attributeName`: required when `valueSource` is `attribute`.
- `pattern`: optional regex to extract value (`value` named group is supported).
- `splitOn`: optional separator for list values.
- `role`: optional semantic mapping:
  - `score`: populates generic sortable/filterable `score`.
  - `category`: populates filterable categories and `category:*` labels.
- `multiplier`, `offset`, `clampMin`, `clampMax`: optional numeric normalization for `role=score`.

## Matching Rules

- `hostSuffixes` supports base hosts and subdomains.
- `pathPrefixes` is optional; if provided, request path must match one prefix.
