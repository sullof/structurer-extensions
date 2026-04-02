# Contributing Extensions

This guide explains how to contribute custom story structures to Structurer.

## Goal

Structurer supports curated extension packs so users can expand available structures without increasing built-in defaults.

## JSON Export Type

Custom structure files must use this top-level shape:

```json
{
  "exportType": "structurer.custom-structures",
  "schemaVersion": 1,
  "exportedAt": 0,
  "appVersion": "1.12.0",
  "structures": []
}
```

## Structure Object Contract

Each item in `structures` must include:

- `id` (string)
- `uid` (string)
- `name` (string)
- `phases` (array of strings, at least 2)
- `updatedAt` (number, unix milliseconds)

Constraints:

- `id` must match: `custom_<slug>`
- `uid` must be alphanumeric and may include `_` and `-`
- `name` must be non-empty
- `phases` must contain non-empty strings only

## Validation Policy

Structurer uses strict import validation:

- If one entry is invalid, the entire import fails.
- No partial imports are applied.
- Duplicate or conflicting entries are rejected.

## Merge Policy

When importing a valid extension file:

1. Merge by `uid` first.
2. Fallback to normalized fingerprint (`name + phases`) when needed.
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
3. In your email, include for each structure: **structure name**, **language** (or language code), and a **short description** of what it is for (you may write the description in **Italian** if you prefer).
4. Send everything to **francesco@sullo.co**.

A maintainer can review your files and, if they fit the catalog rules, add them to this repository and `EXTENSIONS.md` on your behalf.

## Language Organization Rule

`EXTENSIONS.md` is organized by language:

- English section first
- then other languages (Spanish, Chinese, Arabic, etc.)
- add a language section only if at least one extension exists in that language
- if a new language is introduced, add the section title and include at least one linked extension entry
