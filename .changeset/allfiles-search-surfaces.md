---
"@inkeep/open-knowledge": minor
---

Search and the ⌘K omnibar now surface **every file in your project**, not just markdown notes. Part 1 made the sidebar tree show all files; this extends that to search so the two agree.

- Type part of any filename or folder path in ⌘K to jump to it — `data.csv`, `FileTree.tsx`, an image, a config file — regardless of type. Markdown is still ranked first; non-markdown files match by name and path.
- Folders that contain only non-markdown files are now searchable, and partial folder-path queries (e.g. `server/src`) resolve.
- Tracked dot-path files (`.changeset/`, `.github/`) are searchable (rank-deprioritized) without being sent to the embeddings provider.
- A link to an existing non-markdown file no longer renders dead; a genuinely missing target still does.
- The move/rename and new-file destination pickers list the same all-files set the tree shows.
- The omnibar shows a one-line hint when a query matches only file names (no content), and an empty-results note pointing to the file tree when a query matches nothing.
- MCP `search` returns all files by name/path and points agents at `exec` `grep` for exhaustive content search.
- Intentional hardening: secret-bearing files and directories (`.env*`, SSH private keys including `id_ed25519`/`id_ecdsa`/`id_dsa`, `.netrc`/`.npmrc`/`.pgpass`/`.git-credentials`, `*.pem`/`*.key`/`*.p12`/`*.pfx`/`*.keystore`/`*.jks`/`*.ppk`, and the `.ssh`/`.aws`/`.gnupg`/`.kube`/`.docker` directories) are excluded from **all** surfaces — the Part 1 "Show All Files" tree as well as search and `/api/documents`. The unauthenticated local HTTP API is bindable to non-loopback hosts; closing this name-egress channel is the floor whether or not `.gitignore` covers the path.

The file index now indexes names/paths for all files and full content for markdown only, with ContentFilter kept on (gitignored/build content stays out of search) and a 50,000-entry cap on the name-only tier (`OK_SEARCH_MAX_ENTRIES`).
