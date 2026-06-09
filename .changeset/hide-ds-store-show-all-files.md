---
"@inkeep/open-knowledge": patch
---

Stop surfacing macOS Finder metadata files (`.DS_Store`, `.localized`) in the file sidebar's "Show All Files" mode.

These files were already hidden in the normal sidebar (they're seeded into `.gitignore` on `ok init`), but "Show All Files" deliberately bypasses `.gitignore` / `.okignore` to surface gitignored content like `dist/` and `build/` — which re-surfaced `.DS_Store` as a sidebar asset row. They are now pruned by an always-on junk-file floor, the file-level analogue of the existing directory floor that keeps `.git/`, `node_modules/`, and `.ok/` hidden even under Show All Files. Legitimate gitignored content still shows.
