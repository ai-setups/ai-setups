# Pi 安装配置

从 [pi.dev](https://pi.dev/) 安装 CLI，再装扩展。全局配置基本保持默认，只改了模型/主题默认值和扩展列表。

```bash
curl -fsSL https://pi.dev/install.sh | sh
```

## 全局配置（`~/.pi/agent/settings.json`）

大部分保持默认，只改了模型、思考等级、主题这几个默认值，加上扩展列表。

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

provider 地址、API key 和登录信息都在 `~/.pi/agent/models.json`，不在这个文件里，那个文件一律不进仓库。

## 扩展

| 工具 | 为什么装 | 安装命令 |
| --- | --- | --- |
| [pi-subagents](https://github.com/nicobailon/pi-subagents) | 把任务拆给并行子 agent 和脚本化多 agent 流程，不用把所有事塞进同一个上下文。 | `pi install npm:pi-subagents` |
| [pi-web-access](https://github.com/nicobailon/pi-web-access) | 提供联网搜索、URL/PDF 抓取和 GitHub 仓库读取，让 agent 去查证而不是凭记忆猜。 | `pi install npm:pi-web-access` |
| [rpiv-ask-user-question](https://github.com/juicesharp/rpiv-mono/tree/main/packages/rpiv-ask-user-question) | 需求不明确时让 agent 用结构化选项反问，而不是自行假设。 | `pi install npm:@juicesharp/rpiv-ask-user-question` |
| [pi-prompt-toggle](https://github.com/ai-setups/pi-prompt-toggle) | 会话中随时开关叠加的 prompt 指令，不用改配置文件。 | `pi install npm:pi-prompt-toggle` |

用 `pi list` 确认，用 `pi update --all` 统一升级。
