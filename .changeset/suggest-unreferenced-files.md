---
"@inkeep/open-knowledge-app": patch
---

Fix: files that no document links yet now appear in the composer `@`-mention and `[[` wiki-link suggestions. The pickers previously offered only assets already referenced by a doc, so a freshly-added file stayed invisible in autocomplete even though it showed in the sidebar — circular, since those pickers are how you create that first reference. This surfaces every linkable file the sidebar shows (images, GPX, video, CSV, and also source/config), not just media; hidden files stay excluded via the same `isHiddenDocName` rule the sidebar uses (dot-path entries plus OK-managed configs like `opencode.json`).
