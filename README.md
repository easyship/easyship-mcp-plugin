<!-- mcp-name: com.easyship/mcp -->
# Easyship MCP — AI Agent Plugin For Shipping & Logistics Automation

Connect all your AI tools to Easyship’s global shipping platform and manage your entire shipping operation through natural language.

The plugin gives your agent access to shipping rates, shipment creation, label purchasing, package tracking, pickup scheduling, address validation, billing, and analytics. For more info, see the [API docs](https://developers.easyship.com/docs/easyship-mcp-server).

Access 550+ courier services across 200+ countries — including UPS, FedEx, DHL Express, USPS, Canada Post, Australia Post, and Royal Mail — directly from Cursor, Claude, Gemini, Codex, and more.

## Install

* **For Cursor**: Search for "easyship" in **Settings -> Marketplace**, or add manually via **Settings -> Tools & MCP**."

* **For Claude Code**: Run these two commands in a chat:
    ```
    /plugin marketplace add easyship/easyship-mcp-plugin
    /plugin install easyship@easyship-mcp-plugin
    ```

* **For Gemini CLI**: Run this command in your terminal:
    ```
    gemini extensions install https://github.com/easyship/easyship-mcp-plugin
    ```

* **For OpenAI Codex**: In the Codex CLI,
    Add to `~/.codex/config.toml`:

    ```toml
    [mcp_servers.easyship]
    url = "https://mcp.easyship.com/mcp"
    http_headers = { "Authorization" = "Bearer YOUR_TOKEN" }
    ```

* **For VS Code**: Open the Command Palette (`CMD+SHIFT+P`) and run **Chat: Install Plugin From Source**.
  Then paste:
    ```
    https://github.com/easyship/easyship-mcp-plugin
    ```

## What you get

- **Rate comparison**: Compare 550+ courier options with discounted rates, estimated delivery times, and tax and duty estimates
- **Shipment management**: Create, update, track, cancel, and manage shipments end-to-end including label purchase and document retrieval
- **Pickup scheduling**: Check available slots, schedule courier pickups, and manage existing pickups
- **Address validation**: Validate shipping addresses for US domestic and international destinations
- **Billing**: View transactions and billing documents
- **Analytics**: Shipment volume trends, top destinations, courier usage, status breakdowns, and sales channel performance

## Other install methods

If your platform doesn't support plugins, you can install the MCP server directly.

Get your API token from [Easyship Dashboard → Connect → API](https://app.easyship.com/connect/api).

> **Tip:** Copy `.env.example` to `.env` and add your API token. Some local setups will read from this file automatically.

⚠️ Security Note: Never share your API token in the chat window. If you accidentally paste it in a prompt, revoke and rotate your API key immediately in the Easyship Dashboard.

Note: There is no separate test environment for MCP actions. Any action that consumes credits (such as generating labels) will incur real charges. We recommend using a test API token with limited scopes for your first run.

Each client below offers two connection methods:

| Method | How it works | Requires Python? |
|--------|-------------|-----------------|
| **Remote** | Connects to `mcp.easyship.com` via Streamable HTTP | No |
| **Local** | Runs the `easyship-mcp` package on your machine via `uvx` | Yes |



---

### Claude Desktop

**Quit Claude Desktop** before editing config, then restart after saving.

| OS | Config file |
|----|----------------|
| **macOS** | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| **Windows** | `%APPDATA%\Claude\claude_desktop_config.json` |

Merge into the top-level `mcpServers` object (create it if missing).

**Remote:**

```json
{
  "mcpServers": {
    "easyship": {
      "url": "https://mcp.easyship.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN"
      }
    }
  }
}
```

**Local (uvx):**

```json
{
  "mcpServers": {
    "easyship": {
      "command": "uvx",
      "args": ["easyship-mcp"],
      "env": {
        "EASYSHIP_API_ACCESS_TOKEN": "YOUR_TOKEN"
      }
    }
  }
}
```

> Requires [uv](https://docs.astral.sh/uv/) installed on your machine.

---

### Claude Code

**Remote:**

```bash
claude mcp add --transport http easyship \
  https://mcp.easyship.com/mcp \
  --header 'Authorization: Bearer YOUR_TOKEN'
```

**Local (uvx):**

```bash
export EASYSHIP_API_ACCESS_TOKEN="YOUR_TOKEN"
claude mcp add easyship -- uvx easyship-mcp
```

---

### Cursor

Add to `.cursor/mcp.json` in your project (or `~/.cursor/mcp.json` for global):

**Remote:**

```json
{
  "mcpServers": {
    "easyship": {
      "url": "https://mcp.easyship.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN"
      }
    }
  }
}
```

**Local (uvx):**

```json
{
  "mcpServers": {
    "easyship": {
      "command": "uvx",
      "args": ["easyship-mcp"],
      "env": {
        "EASYSHIP_API_ACCESS_TOKEN": "YOUR_TOKEN"
      }
    }
  }
}
```

---

### VS Code

Add to `.vscode/mcp.json` in your project:

**Remote:**

```json
{
  "servers": {
    "easyship": {
      "type": "http",
      "url": "https://mcp.easyship.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_TOKEN"
      }
    }
  }
}
```

**Local (uvx):**

```json
{
  "servers": {
    "easyship": {
      "type": "stdio",
      "command": "uvx",
      "args": ["easyship-mcp"],
      "env": {
        "EASYSHIP_API_ACCESS_TOKEN": "YOUR_TOKEN"
      }
    }
  }
}
```

---

### Gemini CLI

```bash
gemini mcp add --transport http easyship \
  https://mcp.easyship.com/mcp \
  --header 'Authorization: Bearer YOUR_TOKEN'
```

---

### Codex CLI

Add to `~/.codex/config.toml`:

```toml
[mcp_servers.easyship]
url = "https://mcp.easyship.com/mcp"
http_headers = { "Authorization" = "Bearer YOUR_TOKEN" }
```

---

### Other clients

For any MCP client that supports Streamable HTTP, point it at:

```
URL:    https://mcp.easyship.com/mcp
Header: Authorization: Bearer YOUR_TOKEN
```

For stdio-based clients, run `uvx easyship-mcp` with `EASYSHIP_API_ACCESS_TOKEN` set in the environment.

## Usage examples

**Get shipping rates:**
> "What are the shipping options for a 1.5kg package (30×20×15 cm) from Hong Kong to New York?"

**Track a shipment:**
> "Track shipment ESSG10006001"

**Schedule a pickup:**
> "Schedule a pickup for shipment ESSG10006001 on the earliest available date"

**Validate an address:**
> "Validate this address: 215 Clayton St, San Francisco, CA 94117"

**Analyze shipping data:**
> "What are my top shipping destinations this quarter?"

> "Which courier do I use the most?"

## Need help?

- [Easyship API Docs](https://developers.easyship.com)
- [Easyship MCP Docs](https://developers.easyship.com/docs/easyship-mcp-server)
- [Easyship Support](https://www.easyship.com/contact)
- [GitHub Issues](https://github.com/easyship/easyship-mcp-plugin/issues)

## API version

This server targets the Easyship API **v2024-09**.

## License

MIT
