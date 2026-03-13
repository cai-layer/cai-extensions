# Cai Extensions

Community-contributed shortcuts and output destinations for [Cai](https://getcai.app), the macOS clipboard manager.

## Browse Extensions

Extensions are available directly in Cai via **Settings > Extensions** (coming soon). You can also browse the [`extensions/`](extensions/) directory.

## Create an Extension

Each extension is a single YAML file. There are two types:

### Shortcut: LLM Prompt

Sends clipboard text to the LLM with your instruction:

```yaml
name: Professional Email
description: Rewrite text as a polished professional email
author: your-github-username
version: "1.0"
tags: [writing, email]
icon: envelope.fill
type: shortcut
shortcut:
  kind: prompt
  value: |
    Rewrite the following text as a professional email.
    Keep the core message but make it polished and clear.
    Include a greeting and sign-off.
```

### Shortcut: URL Template

Opens a URL with `%s` replaced by the clipboard text:

```yaml
name: Search StackOverflow
description: Search StackOverflow for the selected text
author: your-github-username
version: "1.0"
tags: [developer, search]
icon: magnifyingglass
type: shortcut
shortcut:
  kind: url
  value: "https://stackoverflow.com/search?q=%s"
```

### Output Destination

Sends LLM results (or clipboard text directly) to an external service:

```yaml
name: Send to Slack
description: Post text to a Slack channel via webhook
author: your-github-username
version: "1.0"
tags: [productivity, slack]
icon: bubble.left.fill
type: destination
destination:
  kind: webhook
  show_in_action_list: true
  webhook:
    url: "{{slack_webhook_url}}"
    method: POST
    headers:
      Content-Type: application/json
    body: '{"text": "{{result}}"}'
setup:
  - key: slack_webhook_url
    label: Slack Webhook URL
    secret: false
```

Destination kinds: `webhook`, `applescript`, `url_scheme`, `shell`.

See [`schema.yaml`](schema.yaml) for the full format reference.

## Submit an Extension

1. Fork this repo
2. Create a folder under `extensions/` with a kebab-case name (e.g. `professional-email`)
3. Add an `extension.yaml` file inside it
4. Open a pull request

CI will validate your YAML automatically. Once merged, the extension appears in Cai's extension browser.

### Guidelines

- **One extension per folder** -- keep it focused
- **Test your extension** in Cai before submitting
- **Use SF Symbol names** for icons ([browse symbols](https://developer.apple.com/sf-symbols/))
- **Write a clear description** -- this is what users see when browsing
- **No API keys in YAML** -- use `setup` fields for secrets, which Cai stores in the user's Keychain

## Required Fields

| Field | Description |
|-------|-------------|
| `name` | Display name shown in Cai |
| `description` | One-line summary for the extension browser |
| `author` | Your GitHub username |
| `version` | Version string (e.g. `"1.0"`) |
| `tags` | Array of lowercase tags for search/filtering |
| `icon` | SF Symbol name |
| `type` | `shortcut` or `destination` |

## Template Placeholders

| Placeholder | Used in | Description |
|-------------|---------|-------------|
| `%s` | URL shortcuts | Replaced with clipboard text (URL-encoded) |
| `{{result}}` | Destinations | Replaced with the text to send (auto-escaped per destination type) |
| `{{field_key}}` | Destinations | Replaced with user-configured setup field value |
