# @dsh-desktop/plugin-global-prompt

[![awesome · DSH plugin](https://awesome-dsh-plugin.com/badge.svg)](https://awesome-dsh-plugin.com)

A settings plugin for DeepSeek Harness (DSH). It manages the global `$DSH_HOME/AGENTS.md` and per-workspace `AGENTS.md` files, lets you inject an identity line and a persona into conversations, and toggles runtime-context injection. Works in DSH Web and the dsh-desktop Electron shell.

## Features

- **Global instructions** — edit `$DSH_HOME/AGENTS.md` from the settings panel. Changes apply to the next conversation turn, no restart needed.
- **Project instructions** — per-workspace `AGENTS.md`, resolved server-side from the DSH workspace registry.
- **Two-way sync** — edit `AGENTS.md` outside the plugin and the panel picks it up; save from the panel and the file is rewritten. Both directions go through a content guard, so there is no write loop.
- **Identity injection** — optional `harness:identity` section.
- **Persona injection** — optional `deployment:persona` override; `{{model}}` and `{{cwd}}` placeholders are expanded by DSH at render time.
- **Runtime context switch** — suppress the DSH runtime-context snapshot when you do not want it.
- **Result notifications** — desktop shell notifications, browser notifications in plain Web.

## Install

```
dsh plugin add @dsh-desktop/plugin-global-prompt
```

Or bundled inside the dsh-desktop installer (enabled by default, toggleable in plugin management).

The bundle patch re-enables `dsh-agent-instructions`, which the web-app bundle disables by default. The plugin-managed `AGENTS.md` files are injected by that mechanism.

## Development

The plugin is plain ESM with no build step. `index.js` is the server side, `client.js` the settings UI, `lib/core.js` holds validation helpers.

Run the test script against a live DSH web service:

```
node _tmp/test-global-prompt-sync.mjs
```

## License

MIT
