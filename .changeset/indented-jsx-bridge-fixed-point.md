---
"@inkeep/open-knowledge-core": patch
---

Editing a document that contains an indented MDX component block (fumadocs `<Steps>`/`<Step>`, `<Tabs>`/`<Tab>`, or any component authored with indented markdown children) no longer corrupts the document. The serializer used to rewrite an edited block's children flush-left with extra blank lines, a shape the collaboration bridge could not reconcile with the on-disk source, so under concurrent editing the document could grow without bound until it crossed the open-size limit and refused to reopen. Edited blocks now preserve the canonical two-spaces-per-level indentation (the fumadocs/Obsidian convention) exactly, and an unchanged structured attribute such as `items={["npm", "bun"]}` is no longer rewritten with different whitespace. Blocks authored with a different indentation width normalize to the two-space form on the first edit and then stay stable — a one-time change, not the previous unbounded growth.
