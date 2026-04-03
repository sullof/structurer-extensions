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

- JSON files in this repository target Structurer `1.12.0+`.
- Import is strict-validated in the app: invalid files are fully rejected (no partial import).

## Main App

- Structurer repository: <https://github.com/sullof/structurer>
- Live app: <https://structurer.sullo.co/>
