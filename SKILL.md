---
name: sillytavern-web
description: Integrate or improve browser-based LLM roleplay chat, SillyTavern-style lorebooks, character cards, presets, streaming, and turn state in React, Vue, or vanilla JavaScript projects. Use for tavern chat development and repairs; not for running a roleplay conversation or administering a SillyTavern server.
metadata:
  author: ariespo
  adaptation: Codex
  upstream-version: 3.0.0
---

# SillyTavern Web for Codex

Develop and repair independent roleplay frontends in the user's existing stack. Invoke as `$sillytavern-web` or select automatically for the tasks in the description.

## Choose the integration scope

Inspect applicable AGENTS.md instructions, the current entry points, package and lock files, existing chat pipeline, persistence, and UI conventions. Detect the framework from actual dependencies and source files; a missing package.json does not imply the project needs one.

- Existing application: trace the reported behavior and make targeted changes. Preserve entry points, saved data, visual style, and output formats unless the task requires migration. Do not replace the application with templates.
- New integration: add the requested subset of lorebooks, presets, roleplay chat, and turn state. Reuse the project's package manager and state conventions. Use an existing IndexedDB layer where suitable; add Dexie only when useful.
- Plain HTML/JavaScript: retain a directly runnable static frontend when that is the existing deployment model. TypeScript and React assets are design references, not scripts browsers can load directly.

Infer routine choices from the task and project. Ask only about material unresolved behavior. Secondary model routing is optional and should not be enabled without a need. Do not solicit API keys in chat; use the application's settings UI or existing configuration mechanism.

## Resources

- Read [references/integration.md](references/integration.md) for the framework and resource map, template limitations, and upstream compatibility boundaries.
- Read [references/verification.md](references/verification.md) when implementing chat, prompt, storage, or import changes; select checks relevant to the change.
- React source templates are in [templates/react](templates/react). Inspect imports and public interfaces before adapting individual modules. They are starting points, not a verified drop-in application.
- [references/upstream-skill.md](references/upstream-skill.md) preserves original Vue and vanilla examples. Read only the relevant section when useful. Its slash commands, mandatory questionnaires, copy-all workflow, and blanket dependency installation are historical instructions, superseded by this entry point.

## Implementation invariants

1. Assemble one inspectable request from character/persona, enabled preset blocks and ordering, eligible world information, selected history, and the current input exactly once. Preserve message roles and supported insertion positions. Reserve output capacity in the context budget; do not present character-count estimates as exact token counts.
2. Separate transport framing (SSE/NDJSON/JSON), incremental content parsing, accumulated reply text, and display. Network chunks are not event or tag boundaries. Preserve trailing partial data and explicit protocol errors. A plain text response must remain usable.
3. Own each generation with a request ID, captured chat ID, and AbortController. Pass the signal through all requests, including secondary tasks. Cancellation exits without fallback or retry. Avoid updating another chat after switching sessions, resetting, or starting a newer request. Restore UI state in finally.
4. Treat each turn as a state transition. Retrying or regenerating must not append duplicate user input or apply the previous reply's updates twice. Capture the pre-turn state and commit validated reply/state together; rollback and branches restore the correct snapshot.
5. Lorebook matching must respect disabled entries, primary/secondary selection semantics, recursion exclusions, deduplication, ordering, and bounded depth/budget. Explain unsupported imported fields instead of claiming complete SillyTavern compatibility.
6. Treat imported cards, lorebooks, presets, variables, and model output as untrusted data. Validate shape and size; use textContent/value or framework escaping. Sanitize explicitly supported rich HTML with an allowlist. Parse PNG card metadata as binary chunks rather than file.text(). Reject prototype keys in recursive state merges.
7. Separate credentials from shareable project and session data. Never embed real keys or shared webhooks in generated source. Exclude secrets from exports, backups, diagnostics, and fixtures. Explain browser-origin/CORS requirements when direct provider access is relevant; use an existing authorized proxy if available.
8. Version persistent formats and migrate without silently dropping messages or variables. Report a save as successful only after durable completion. Preserve the previous valid backup until the new one is confirmed.

## Finish

Run the project's relevant checks and focused regression scenarios. For a new UI, verify loading, empty/error states, send/stop, reload persistence, and the selected import path. Use mocked model responses unless live calls are authorized. Distinguish passed checks, static review, and untested behavior. Report changed behavior and remaining limitations without claiming full compatibility or production readiness from a build alone.
