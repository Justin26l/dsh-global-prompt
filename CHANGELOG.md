# Changelog

All notable changes to this project are documented in this file.

## [0.1.2] - 2026-08-25

### Added
- Two-way sync between `AGENTS.md` and the settings panel. Editing the file outside the plugin updates the panel; saving from the panel rewrites the file. A content guard prevents write loops.

### Fixed
- Enabled=false no longer wipes a user-maintained `AGENTS.md`; the disabled state is handled by the prompt assembly filter instead.
- On startup, an existing `AGENTS.md` is read back into settings instead of being overwritten by the default empty value.
- File watcher now ignores the plugin's own writes, so a UI save does not echo back into settings.
- Watch events with a lower-case or `null` filename are handled (Windows rename events).
- Oversized `AGENTS.md` files are not written back into settings (matches the 1 MiB PUT validation).

## [0.1.1] - 2026-08-21

- Initial standalone release: global and project `AGENTS.md` editors, identity/persona injection, runtime-context suppression, result notifications, `agent-instructions` re-enabled via bundle patch.
