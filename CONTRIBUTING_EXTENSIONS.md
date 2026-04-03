# Contributing Extensions

This guide explains how to contribute custom story structures to Structurer.

## Goal

Structurer supports curated extension packs so users can expand available structures without increasing built-in defaults.

## JSON Export Type

Custom structure files must use this top-level shape:

```json
{
  "exportType": "structurer.custom-structures",
  "schemaVersion": 2,
  "exportedAt": 0,
  "appVersion": "1.13.1",
  "structures": []
}
```

Use **`schemaVersion`: `2`** for new files in this repository (structure-level `description` / `author` on each entry). Structurer still accepts **`1`** for older exports (same `structures` shape; optional metadata may be absent). The app rejects any other `schemaVersion` value.

## Structure Object Contract

Each item in `structures` must include:

- `id` (string)
- `uid` (string)
- `name` (string)
- `phases` (array, at least 2 entries)
- `updatedAt` (number, unix milliseconds)

Each item in `structures` **in this repository** should also include:

- `description` (string) — what the structure is for, in the **same language** as the structure name and phase titles.
- `author` (string) — short attribution (source model, tradition, or book); same language when possible.

In the Structurer app these two fields are **optional** on import, but **pull requests to this repo should always include them** (non-empty after trim) so the structure-level help introduced in **Structurer 1.13.1** stays useful. The app validates them (max lengths, no raw URLs in description, etc.); exporting from Structurer 1.13.1+ produces compliant values.

### `phases` format

Structurer **1.12.0+** accepts each phase as either:

1. A **non-empty string** (title only), or
2. An object **`{ "title": "…", "description": "…" }`**
   - `title` is required (you may use `name` as an alias for `title`; `title` is preferred).
   - `description` is optional in the app importer, but **extension files in this repository should use the object form with a non-empty `description` for every phase** (same language as the phase title) so the in-app phase help panel is useful.

Example:

```json
"phases": [
  "Plain title only",
  {
    "title": "Title with help",
    "description": "One short sentence: what the writer should do or explore in this phase."
  }
]
```

Constraints:

- `id` must match: `custom_<slug>`
- `uid` must be alphanumeric and may include `_` and `-`
- `name` must be non-empty
- `phases` must have at least 2 entries; each entry must be a non-empty string or a non-empty `title` as above

## Validation Policy

Structurer uses strict import validation:

- If one entry is invalid, the entire import fails.
- No partial imports are applied.
- Duplicate or conflicting entries are rejected.

## Merge Policy

When importing a valid extension file:

1. Merge by `uid` first.
2. Fallback to normalized fingerprint (`name` + **phase titles**, ignoring descriptions) when needed.
3. Apply Last-Write-Wins by `updatedAt`.

## PR Checklist

- Ensure no conflicts with built-in structure IDs.
- Ensure no duplicate IDs or UIDs in your file.
- Keep names and phases clear and consistent.
- Use the original language/script for the structure name when relevant, and add a transliteration in parentheses if helpful.
- Add your extension to `EXTENSIONS.md` under the correct language section.
- If your language section does not exist yet, add it in language order.
- Place JSON files in `extensions/structures/<language-code>/`.

## Recommended Workflow

To minimize formatting errors:

1. Create the structure directly inside Structurer.
2. Use `Export custom structures` from Dashboard Actions.
3. Keep only the structure(s) you want to contribute in the exported JSON file.
4. Add that JSON file to your PR and update `EXTENSIONS.md`.

## Contributing without GitHub

If you are not comfortable using GitHub, you can still propose an extension:

1. Prepare your JSON file(s) using Structurer (create the structure in the app, then **Export custom structures** and keep only what you want to share).
2. Zip the JSON file(s).
3. In your email, include for each structure: **structure name**, **language** (or language code), and a **short description** of what it is for.
4. Send everything to **francesco@sullo.co**.

A maintainer can review your files and, if they fit the catalog rules, add them to this repository and `EXTENSIONS.md` on your behalf.

## Language Organization Rule

`EXTENSIONS.md` is organized by language:

- English section first
- then other languages (Spanish, Chinese, Arabic, etc.)
- add a language section only if at least one extension exists in that language
- if a new language is introduced, add the section title and include at least one linked extension entry

## Rollout checklist: phase descriptions in more languages

After the English + Italian pilot, use this checklist for `es`, `ar`, `zh`, `ja`, `sa`, and any new locale:

1. **Inventory** — List JSON files under `extensions/structures/<lang>/`.
2. **Convert** — Replace string-only `phases` with `{ "title": "…", "description": "…" }` (descriptions in the **same language** as the titles).
3. **Validate** — Ensure valid JSON; each phase has non-empty `title` and `description`; `id` / `uid` rules unchanged.
4. **Import test** — In Structurer **1.13.1+**, use **Import custom structure** on at least one file from that folder to confirm strict validation passes (including structure `description` / `author` if present).
5. **Docs** — No change to `EXTENSIONS.md` links unless filenames change; update this guide if the contract evolves.

### Maintainer validation (optional)

You can sanity-check files against Structurer’s importer by opening the app and importing a sample file. For structure-level `description` / `author` strings, you can also run the same validators the app uses: `validateStructureDescription` and `validateStructureAuthor` in the main app (`structurer` repo, `src/structure-metadata.js`).
