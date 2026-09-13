# Pi Setup

Install the CLI from [pi.dev](https://pi.dev/), then add extensions. Global config stays near-default — only the model/theme defaults and the extension list are changed.

```bash
curl -fsSL https://pi.dev/install.sh | sh
```

## Global config (`~/.pi/agent/settings.json`)

Near-default: model/thinking/theme defaults plus the extension list.

```json
{
  "theme": "dark",
  "defaultProvider": "anthropic",
  "defaultModel": "claude-opus-5",
  "defaultThinkingLevel": "high",
  "packages": [
    "npm:pi-subagents",
    "npm:pi-web-access",
    "npm:@juicesharp/rpiv-ask-user-question",
    "npm:pi-prompt-toggle"
  ]
}
```

Provider endpoints and API keys or login credentials live in `~/.pi/agent/models.json`, not here — never commit that file.

## Extensions

| Tool | Why | Install |
| --- | --- | --- |
| [pi-subagents](https://github.com/nicobailon/pi-subagents) | Delegate work to parallel subagents and scripted multi-agent workflows instead of doing everything in one context. | `pi install npm:pi-subagents` |
| [pi-web-access](https://github.com/nicobailon/pi-web-access) | Gives the agent web search, URL/PDF fetching and GitHub repo reading, so it verifies facts instead of guessing. | `pi install npm:pi-web-access` |
| [rpiv-ask-user-question](https://github.com/juicesharp/rpiv-mono/tree/main/packages/rpiv-ask-user-question) | Lets the agent ask structured multiple-choice questions instead of silently guessing on ambiguous requirements. | `pi install npm:@juicesharp/rpiv-ask-user-question` |
| [pi-prompt-toggle](https://github.com/ai-setups/pi-prompt-toggle) | Toggle stackable prompt instructions on/off mid-session without editing config files. | `pi install npm:pi-prompt-toggle` |

Verify with `pi list`; update everything with `pi update --all`.
