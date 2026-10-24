# Integration and resource map

Upstream: https://github.com/ariespo/tavernlike
Pinned source: 9d93c5367d9570aa2da9522adb63bfb99156d227.

## React

`templates/react/sillytavern/` contains types, Dexie persistence, lorebook matching, prompt assembly, JSON imports, variables, content tag parsing, API routing, and editor helpers. `templates/react/hooks/` contains React adapters. `templates/react/components/SillyTavern/` contains game view and settings/lorebook/preset/variable editors.

Use the existing app state owner or context/provider. Calling a hook with independent useState in several sibling components does not create a shared store. Check default settings, component props, exports, and dependencies together before wiring an entry point. The upstream inline examples mention Chat, ChatModal and VariablePanel that are not standalone bundled files; do not generate imports to missing files.

## Vue and vanilla

The original inline Vue composable and vanilla store are preserved in `upstream-skill.md` under `Vue Integration` and `Vanilla JS Integration`. These are older v2 examples; they do not establish v3 streaming/game/multi-API support. Port needed pure logic to the host's data model and runtime. For static HTML use JavaScript modules or the established inline organization; do not require a framework conversion.

## Template limitations requiring attention during integration

The bundled templates retain upstream behavior, including known gaps; adapting the skill does not certify or repair every template:

- `useApiRouter.ts` creates an AbortController but `api-router.ts` does not pass its signal to fetch. Carry cancellation through the transport and exclude cancellation from secondary fallback.
- Its SSE splitter assumes LF blank lines and can drop EOF remainder. Validate CRLF, event boundaries and incomplete final frames with fixtures.
- `prompt-assembler.ts` estimates tokens from character length and models only a subset of preset schemas. Normalize actual imported `prompt_order` variants and roles before use.
- `StreamTagParser` is an XML-like content parser, not an SSE parser. The original inline Vue/vanilla examples and current project may use different output protocols. Define an adapter rather than mixing formats.
- `useSillytavern.ts` owns state per hook instance. Review sharing and captured state during asynchronous sends before reusing it across components.
- Secondary API routing does not prove end-to-end summary/variable task orchestration. Verify actual dispatch and commit ordering.

## Compatibility

State what is implemented: particular JSON preset/lorebook shapes, character card versions, macro subset, injection semantics, output formats, and provider protocols. Preserve unknown imported data when safe for round trips. Do not silently treat unsupported files as valid imports. An OpenAI-compatible endpoint does not by itself support native Anthropic, Ollama or Kobold protocols.

For an existing project inspect and extend its storage migration and import adapters first. Do not copy a new database name or defaults over user data. Use local mock responses to verify application behavior without real credentials.
