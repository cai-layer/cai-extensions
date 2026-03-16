# Cai Extensions

Community-contributed extensions for [Cai](https://getcai.app), the macOS clipboard manager.

## Install an Extension

1. Browse the [`extensions/`](extensions/) directory and open the `extension.yaml` you want
2. Copy the entire YAML content (including the `# cai-extension` header)
3. Press **Option+C** — Cai detects it and shows **Install Extension**
4. Press Enter — done!

## Extension Types

| Type | What it does | Installs as | Needs LLM? |
|------|-------------|-------------|------------|
| `prompt` | Sends clipboard text to the LLM with a custom instruction | Shortcut | Yes |
| `url` | Opens a URL with `%s` replaced by clipboard text | Shortcut | No |
| `shell` | Runs a shell command with the text | Shortcut | No |
| `webhook` | Sends text to an HTTP endpoint (Slack, Discord, etc.) | Destination | No |
| `deeplink` | Opens a URL scheme / deep link (Bear, Things, etc.) | Destination | No |
| `applescript` | Runs an AppleScript with the text | Destination | No |

> **Shortcuts** appear as actions in the Cai action window. **Destinations** are output targets that receive text after an action runs. See the [docs](https://getcai.app/docs/usage/extensions) for details.

## Submit an Extension

1. Fork this repo
2. Create a folder under `extensions/` with a kebab-case name
3. Add an `extension.yaml` inside it
4. Open a pull request

See the [extension creation guide](https://getcai.app/docs/usage/extensions#creating-an-extension) for format reference, examples, and guidelines.

## Security

- `applescript` and `shell` types are **not accepted** from community contributors
- Webhook URLs must use HTTPS and `{{setup_field}}` placeholders — never hardcode endpoints
- No API keys in YAML — use `setup` fields with `secret: true`
