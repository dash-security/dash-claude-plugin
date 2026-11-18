# Dash Security

Dash secures the full agentic estate across discovery, posture, runtime detection, and governance. The Dash plugin connects Claude to the **Dash MCP** and includes skills that turn your Dash Security data into first-class agent workflows: discover your AI estate, assess supply-chain and shadow AI risk, investigate agent sessions, and track AI spend and usage.

## Install

### claude.ai and Cowork

1. Open **Customize -> Plugins**.
2. Search for **Dash Security** and click **Add**.
3. Open the plugin's **Connectors** tab, connect **Dash**, and complete the Dash sign-in prompt.

### Claude Code

```
/plugin marketplace add dash-security/dash-claude-plugin
/plugin install dash-security@dash-security
```

Skills are namespaced by the plugin, for example `/dash-security:ai-spend`. Run `/mcp` to sign in to Dash.

## MCP

```json
{
  "mcpServers": {
    "dash": {
      "type": "http",
      "url": "https://mcp.dash.security/mcp"
    }
  }
}
```

Auth is OAuth 2.0 against Dash. Claude prompts for Dash sign-in when you connect the plugin's connector - no token needs to be placed in any config file. If your account belongs to multiple Dash tenants, Claude will ask which tenant to use (via the MCP `list_tenants` tool).

## Skills

| Skill                         | Use it for                                                                                                                                                                                                                                                                                            |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `agentic-estate-discovery`    | Discover every agent, harness, platform, extension, MCP, skill, hook and plugin installed and running in your environment. Observe all AI activity and usage trends, uncovering who is using agents and what they are using them for.                                                                 |
| `supply-chain-risk`           | Surface the risky tools used by agents in your organization. Scan MCP servers, skills, plugins, and hooks to reveal their capabilities, access, and suspicious behavior. Get an evidence-backed risk assessment and blast radius for each one.                                                         |
| `shadow-ai-risk`              | Uncover the agentic platforms in use across your organization, on the endpoint and in the browser. Get a full registry of every shadow platform accessed or installed, attributed to specific users and devices, including users authenticating to AI platforms with personal or private identities. |
| `agent-session-investigation` | Investigate agent sessions and security detections in depth. Review the full reconstructed agent flow - from user intent and agent reasoning, to tool calls, commands, and file access.                                                                                                               |
| `ai-spend`                    | Understand how AI is being used and what it is costing your organization. Analyze spend, token consumption, model usage, and adoption trends across teams, platforms, and users to identify top consumers, high-cost activity, and optimization opportunities.                                        |

Each skill orchestrates the Dash MCP tools. Claude selects a skill automatically from your request, or you can name one explicitly.

## Data and privacy

The plugin contains only Markdown skills and one MCP server reference. It runs no local scripts, hooks, or package installs, and stores nothing on your machine.

- The only network destination is the Dash MCP server at `https://mcp.dash.security/mcp`, plus the Dash OAuth sign-in it starts.
- When a skill runs, Claude sends MCP tool calls (search filters, IDs, date ranges, and tenant selection) to Dash and receives data from your Dash tenant: agents, platforms, MCP servers, skills, devices, users, sessions, findings, detections, and AI spend.
- Access is scoped to the Dash tenants and permissions of the signed-in user.

See the [Dash Security privacy policy](https://dash.security/privacy-policy).

## Requirements

- A Dash Security account with access to the developer API.
- Claude (claude.ai, Cowork, or Claude Code).

## License

MIT
