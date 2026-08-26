# mcp-boi-il

Bank of Israel public API MCP. Keyless.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1476+ live data sources.

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

### What this endpoint actually serves

`tools/list` at `https://gateway.pipeworx.io/boi-il/mcp` returns the tools in the table
above **plus the shared Pipeworx meta-tools** — `ask_pipeworx`,
`discover_tools`, `search_within`, `remember`/`recall` and the rest of the
gateway-wide set. So the tool count you see is larger than this table: a
single-pack endpoint currently lists roughly 30 shared tools alongside the
pack's own. The connection's `initialize` response states its exact scope, and
is the authoritative answer for a given day.

This is deliberate, not multiplexing by accident. The meta-tools are what let a
scoped connection answer a question this pack does not cover — via
`ask_pipeworx`, which routes across the whole catalog — without you adding a
second MCP server. There is currently no way to mount a pack endpoint without
them; if the extra schemas cost you more context than the routing is worth,
connect to the full gateway once rather than to several pack endpoints.

Or connect to the full Pipeworx gateway to get every pack's tools listed
directly, instead of just this one's:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

Both URLs reach the same gateway and the same 1476+ data sources. The
only difference is which pack's tools are listed **directly**; `ask_pipeworx`
reaches all of them from either one.

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English —
this works on the pack endpoint above as well as on the full gateway:

```
ask_pipeworx({ question: "your question about Boi Il data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
