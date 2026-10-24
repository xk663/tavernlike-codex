# Focused regression scenarios

Select scenarios relevant to the changed behavior. Use existing test infrastructure when present; for plain HTML a small isolated function harness is appropriate. Do not add a large toolchain just to check a minor UI edit.

## Prompt and lorebooks

- A distinctive character description and matched lore entry appear in the actual outbound messages when a custom preset block is enabled.
- User input appears exactly once; disabled blocks and disabled lore entries remain absent.
- Imported block roles/order/depth retain supported semantics. Unsupported fields produce an honest compatibility result.
- Test primary/secondary keyword truth tables and A → B → C recursion, cycles, disabled B, and budget limits.
- Long history stays within the chosen context policy with reply capacity reserved; explain estimation limitations.

## Generation

- Split UTF-8 characters, SSE frames, and content tags across every relevant boundary. Exercise CRLF, data fields with or without a space, DONE, API error payloads, and trailing partial frames.
- Accumulated visible text equals the intended reply, including untagged/plain text.
- Stop while connecting and while waiting for the next chunk: no fallback request, no late state commit, UI becomes usable.
- Switch chats, reset, or delete a session during generation; an old completion cannot overwrite a new turn or revive a deleted chat.
- Retry/regenerate preserves one user input and applies state updates once; failures retain a recoverable draft or incomplete turn.

## Persistence and imports

- Reload a saved chat and compare messages, variables, selected character/preset/world books, and world state where supported.
- Export/import round-trip excludes credentials and preserves supported data. Malformed/oversized JSON and PNG metadata fail clearly.
- Names containing quotes or HTML remain inert text in settings and lists; prototype keys cannot alter merge targets.
- Simulate quota/transaction/upload failure: no success message or premature deletion of the previous backup.
- Branch/rollback restores the chosen chat's own snapshot without aliasing future mutations.

## UI

Verify empty/loading/error states, keyboard send with IME composition, stop behavior, long message scrolling, settings persistence, and relevant mobile layout. Record which checks ran and which require a browser or authorized live provider.
