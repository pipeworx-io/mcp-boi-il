# mcp-boi-il

Bank of Israel public API MCP. Keyless.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1394+ live data sources.

## Tools

| Tool | Description |
|------|-------------|
| `boi_exchange_rates` | All current Bank of Israel representative exchange rates vs the Israeli Shekel (ILS). Returns one entry per currency with currentExchangeRate (shekels per `unit` of the foreign currency), currentChange (% vs previous), unit (1 for most, 100 for some like JPY — per-1 rate = currentExchangeRate / unit), and lastUpdate. Use this for a snapshot of all available currencies. |
| `boi_exchange_rate` | Current Bank of Israel representative exchange rate for a single currency vs the Israeli Shekel (ILS), by 3-letter ISO code. Returns currentExchangeRate (shekels per `unit`), currentChange (%), unit, and lastUpdate. Note `unit` (e.g. JPY is per 100). Example keys: USD, EUR, GBP, JPY, CHF, CAD, AUD. |
| `boi_interest_rate` | The current Bank of Israel (BOI) policy interest rate for ISRAEL — the Israeli benchmark rate set by the Bank of Israel Monetary Committee, in % per annum. Returns currentInterest (the Israeli policy rate), nextInterestDate (next Israeli rate decision), and lastPublishedDate. Scope: Israel only. |

## Quick Start

Add to your MCP client (Claude Desktop, Cursor, Windsurf, etc.):

```json
{
  "mcpServers": {
    "boi-il": {
      "url": "https://gateway.pipeworx.io/boi-il/mcp"
    }
  }
}
```

Or connect to the full Pipeworx gateway for access to all 1394+ data sources:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English:

```
ask_pipeworx({ question: "your question about Boi Il data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
