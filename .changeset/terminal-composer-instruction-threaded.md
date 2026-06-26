---
"@inkeep/open-knowledge-app": patch
---

Fix the bottom "Ask AI" composer dropping the typed instruction when launching a Terminal CLI. A composer dispatch carries its instruction (and `@`-mentions / selection) in `input.compose`, but the docked-terminal launcher only checked the top-level `input.instruction` the toolbar popover uses — so every composer-typed message fell through to the bare "load OK, then stop" prompt and the agent never saw what the user asked. The terminal launcher now routes compose-scope dispatches through the same prompt assembler as the deep-link handoff, so the instruction threads through to the launched CLI exactly as it does to a Claude/Codex/Cursor deep link.
