# StockMind AI — Grok + Questrade MCP

A Grok-powered research and order-preparation project using Questrade's official remote MCP server.

## Capabilities
- Read account, positions, balances, watchlists, quotes and order history through authorized Questrade MCP tools.
- Research securities and produce trade ideas.
- Prepare an order proposal and risk summary.
- Send a specific order instruction to Questrade Push Approval only after the user explicitly requests that exact order.
- Require the user to approve every order in Questrade's mobile app.

## Connect Grok to Questrade
The project MCP configuration is in `.grok/config.toml`:

```toml
[mcp_servers.questrade]
url = "https://mcp.questrade.com/v1/brokerage/mcp"
startup_timeout_sec = 30
tool_timeout_sec = 120
```

Use Grok's supported remote MCP connector or CLI to add the Questrade server. Complete authorization only on Questrade's official sign-in/consent page. Never paste passwords, OAuth codes, access tokens, or refresh tokens into chat or source files.

Official server: `https://mcp.questrade.com/v1/brokerage/mcp`

## Trading mode and critical limitation
This repository is configured for **AI research and order preparation with mandatory Questrade Push Approval**. Questrade's order-instruction tools send a push notification; the order is not submitted to the market until the customer approves it on an enrolled trusted device. This cannot be bypassed by Grok, Python, GitHub Actions, or this repository. Fully unattended trading is therefore not implemented.

See [TRADING_POLICY.md](TRADING_POLICY.md) for mandatory controls.

## Safe first prompts
- "List my Questrade accounts. Read-only; do not prepare or submit any order."
- "Show my positions, balances and open orders. Do not trade."
- "Analyse [ticker] using current market data. Give risks and possible scenarios; do not place an order."
- "Prepare a preview-only proposal for [side] [quantity] shares of [ticker] in [account]. Do not send it for approval."

## Security
- `.gitignore` excludes common secret and local credential files.
- Never commit credentials, keys, OAuth tokens, account numbers or personal data.
- Use least-privilege connector permissions and revoke access in Questrade if no longer needed.

## Official references
- [Questrade: Connect your account to AI](https://www.questrade.com/learning/using-questrade/connect-your-questrade-account-to-ai)
- [Questrade MCP technical reference](https://www.questrade.com/learning/using-questrade/questrade-mcp-technical-reference)
- [xAI remote MCP tools](https://docs.x.ai/developers/tools/remote-mcp)

For research and educational use only; not financial advice. Markets involve risk and losses are possible.
