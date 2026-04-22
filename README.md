# Brand Guide Schema

![Status](https://img.shields.io/badge/status-early%20development-orange)
![JSON Schema](https://img.shields.io/badge/JSON%20Schema-2020--12-blue)
![License](https://img.shields.io/badge/license-MIT-green)

> **Status:** Early development. Schema and templates are functional but the format is actively evolving. Field additions and breaking changes are possible before v1.0.

A lightweight, machine-readable format for brand identity — built so AI agents can reliably access and apply brand context.

## The problem

AI agents working on design, copy, and content tasks need brand context: colors, typography, voice, positioning. Without a standard format, that context lives in PDFs, style guides, and someone's memory. Agents either get it wrong or you paste it into every prompt.

## The format

Two files per brand:

**`brand.json`** — machine-readable. Designed for agents, scripts, and tooling. Validate it against `schema.json`.

**`brand-guide.md`** — human-readable companion. Same data, markdown format. Easy to attach to a system prompt.

## Usage

Give an agent your brand context at session start:

```
Read brand.json and brand-guide.md before proceeding. 
Apply the brand voice, colors, and typography to all outputs.
```

Or load it programmatically:

```python
import json

with open("brand.json") as f:
    brand = json.load(f)

primary_color = brand["colors"]["primary"]["hex"]
voice_tone = brand["voice"]["tone"]
voice_examples = brand["voice"]["examples"]
audience = brand["audience"]["primary"]
```

## Fields

### Required

| Field | Type | Description |
|-------|------|-------------|
| `brand` | string | Full brand name |
| `website` | string | Primary domain (no protocol) |
| `category` | string | Industry and subcategory, e.g. `"Legal — Family Law"` |
| `last_updated` | string (date) | ISO 8601 date last reviewed |
| `positioning` | string | One or two sentence positioning statement |
| `markets` | string[] | Geographic or demographic markets served |
| `colors` | object | Named color roles — each with `hex` and optional `usage` note |
| `typography` | object | Named type roles with CSS `stack` and optional `weight`, `size`, `line_height` |
| `voice` | object | `tone`, `avoid`, and optional `examples` (sample on-brand sentences) |

### Optional

| Field | Type | Description |
|-------|------|-------------|
| `version` | string (semver) | Brand guide version, e.g. `"1.0.0"` |
| `taglines` | string[] | Brand taglines, priority order |
| `differentiation` | string | One sentence: what this brand is not or how it differs |
| `audience` | object | `primary` (who the customer is), `pain_points`, `motivations` |
| `services` | string[] | Products or services offered |
| `restrictions` | string[] | Off-limits language or claims (important for regulated industries) |
| `accessible_pairs` | array | Approved color combinations, referencing color role names |
| `color_mode` | `"light"` or `"dark"` | Default rendering mode |
| `logo` | object | `description`, `has_icon_variant`, `color`, `white`, `monogram`, `wordmark`, `icon_file`, `wordmark_file` |
| `contact` | object | `email`, `phone` |
| `social` | object | Arbitrary key→value pairs, keyed by platform name |

## Validation

Validate any `brand.json` against the included `schema.json`:

```bash
npx ajv-cli validate --spec=draft2020 -s schema.json -d brand.json
```

## File structure

```
your-brand/
  brand.json        # machine-readable (use this with agents)
  brand-guide.md    # human-readable (attach to prompts)
```

## Templates

`brand.json` and `brand-guide.md` in this repo are blank templates. Copy, fill in, validate.
