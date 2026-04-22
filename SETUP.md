# Easyship Plugin Setup

This plugin connects to the Easyship MCP server and requires an API access token.

⚠️ Security Note: Never share your API token in the chat window. If you accidentally paste it in a prompt, revoke and rotate your API key immediately in the Easyship Dashboard.

## Get your API token

1. Log in to the [Easyship Dashboard](https://app.easyship.com)
2. Go to **Connect** → **API** ([direct link](https://app.easyship.com/connect/api))
3. Create or copy your API access token

## Configure the token

Set the `EASYSHIP_API_ACCESS_TOKEN` environment variable:

```bash
export EASYSHIP_API_ACCESS_TOKEN="your_token_here"
```

Or add it to your shell profile (`.bashrc`, `.zshrc`, etc.) for persistence.

## Verify the connection

After setting your token, try one of these prompts to confirm everything works:

- "What are the shipping options for a 1 kg package from Hong Kong to New York?"
- "Track shipment ESSG10006001"
- "What are my top shipping destinations this quarter?"

If you see rate results or tracking data, the plugin is connected successfully.

For more info, see the [API docs](https://developers.easyship.com/docs/easyship-mcp-server).

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "Unauthorized" or 401 errors | Double-check your API token is set correctly and hasn't expired |
| "No rates found" | Verify origin/destination countries and parcel dimensions are valid |
| Token not recognized | Restart your IDE or terminal session after setting the env variable |

## Need help?

- [Easyship API Docs](https://developers.easyship.com)
- [Easyship MCP Docs](https://developers.easyship.com/docs/easyship-mcp-server)
- [Easyship Support](https://www.easyship.com/contact)
- [GitHub Issues](https://github.com/easyship/easyship-mcp-plugin/issues)
