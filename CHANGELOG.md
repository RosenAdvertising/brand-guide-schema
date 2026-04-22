# Changelog

## [Unreleased]

### Added
- `voice.examples` — sample on-brand sentences for copy agents
- `audience` — primary persona, pain_points, motivations
- `differentiation` — one-sentence brand differentiator
- `restrictions` — off-limits language for regulated industries
- `imagery_style` — art direction for visual agents
- `accessible_pairs` — approved color combinations
- `legal_name`, `locale` — entity and language metadata
- `logo.logo_style` — enum (wordmark, lettermark, pictorial, abstract, combination)
- `version` field (semver) for brand guide files
- `$id` URI for external schema referencing

### Changed
- `colors` restructured: each role is now `{ hex, usage }` instead of a plain hex string
- `colors` now requires `primary` and `background` roles
- `positioning` restructured: now an object with `statement`, `for`, `category`, `benefit`
- `typography` roles now accept optional `weight`, `size`, `line_height` alongside `stack`
- `contact.phone` renamed to `telephone` (schema.org alignment)
- Hex color validation now rejects invalid lengths (5, 7 chars)
- `ajv-cli` validation command updated to include `--spec=draft2020`

### Removed
- `contact` block — not a brand concern; belongs in CRM or site config
- `typography.family` — removed in favor of `stack` only (eliminates drift risk)

---

*Format: [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). Versioning: [Semantic Versioning](https://semver.org/).*
