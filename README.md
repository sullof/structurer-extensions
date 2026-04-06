# Structurer Extensions

This repository contains extension packs for [Structurer](https://github.com/sullof/structurer), a privacy-first story planning app for writers.

Structurer helps you design stories with visual phases and notes. This repo keeps extra/custom structures separate from the main app so the core project stays clean and lightweight.

## What You Will Find Here

- `EXTENSIONS.md` - Curated catalog of available extension packs
- `CONTRIBUTING_EXTENSIONS.md` - Rules and workflow for contributors
- `extensions/structures/<language-code>/` - JSON files you can import into Structurer

## How To Use Extensions

1. Open the catalog in `EXTENSIONS.md`.
2. Download a JSON file from one of the listed raw links.
3. In Structurer, open Dashboard `... Actions`.
4. Use `Import custom structure` (file) or `Import custom structure (paste JSON)`.
5. The imported structure will appear in the structure selector for new stories.

## Version Compatibility

- JSON files use **`schemaVersion`: `2`** and **`appVersion`**: **`1.13.1`** (custom-structures format with structure-level `description` and `author`). Use Structurer **`1.13.1+`**, which accepts **`schemaVersion` 1 or 2** on import and shows structure metadata from 1.13.1 onward.
- Per-phase `title` + `description` remain compatible with Structurer **1.12.0+** phase help; structure-level metadata is honored on import and shown in the app from **1.13.1** onward.
- Import is strict-validated in the app: invalid files are fully rejected (no partial import).

## History

Project history is tracked in [`HISTORY.md`](HISTORY.md).

## Main App

- Structurer repository: <https://github.com/sullof/structurer>
- Live app: <https://structurer.sullo.co/>
