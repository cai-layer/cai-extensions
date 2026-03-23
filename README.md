# Cai Extensions

Community-contributed extensions for [Cai](https://getcai.app), the macOS clipboard manager.

## Install an Extension

Open **Settings > Community Extensions** in Cai to browse and install extensions with one click.

<img src="assets/extension-browser.png.png" alt="Extension Browser" width="400">

You can also install manually: copy the YAML content of any `extension.yaml` (including the `# cai-extension` header), press **Option+C** — Cai detects it and offers to install.

## Extension Types

| Type          | What it does                                                 | Installs as   | Needs LLM? |
| ------------- | ------------------------------------------------------------ | ------------- | ---------- |
| `prompt`      | Sends clipboard text to the LLM with a custom instruction    | Custom Action | Yes        |
| `url`         | Opens a URL with `%s` replaced by clipboard text             | Custom Action | No         |
| `shell`       | Runs a shell command with the text and renders result in Cai | Custom Action | No         |
| `webhook`     | Sends text to an HTTP endpoint (Slack, Discord, etc.)        | Destination   | No         |
| `deeplink`    | Opens a URL scheme / deep link (Bear, Things, etc.)          | Destination   | No         |
| `applescript` | Runs an AppleScript with the text                            | Destination   | No         |
| `shell`       | Runs a shell command with the text                           | Destination   | No         |

> **Custom Actions** appear as actions in the Cai action window. **Destinations** are output targets that receive text after an action runs. See the [docs](https://getcai.app/docs/usage/extensions) for details.

## Submit an Extension

The easiest way to share an extension you've built:

1. Open **Settings > Custom Actions** (or **Output Destinations**)
2. Click the **share icon** on any custom action or destination
3. Cai copies the extension YAML to your clipboard and opens this repo
4. Fork, create a folder under `extensions/`, paste the YAML as `extension.yaml`, and open a PR

Or create the YAML manually — see the [extension creation guide](https://getcai.app/docs/usage/extensions#creating-an-extension) for the full format reference.

## Security

- Webhook URLs must use HTTPS and `{{setup_field}}` placeholders — never hardcode endpoints
- No API keys in YAML — use `setup` fields with `secret: true`
