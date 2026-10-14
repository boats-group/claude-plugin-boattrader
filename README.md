# Boat Trader plugin for Claude

Search, compare, and research new and used boats for sale across the U.S. with live Boat Trader inventory, straight from a conversation with Claude.

## What's included

- **Boat Trader connector** (`.mcp.json`): the remote MCP server at `https://boattrader-mcp.live.boatsgroup.com/mcp`, with tools to search listings (`search-boats`), research market inventory and asking-price statistics (`aggregate-search`), and fetch full listing details (`get-boat-details`).
- **`boat-shopping` skill**: tells Claude when to use each tool and how to turn a request like "a trailerable fishing boat under $40k near Tampa" into a well-formed search.

## Use it

Ask Claude things like:

- "Find me a used center console under $60,000 near Fort Lauderdale"
- "How many Sea Ray 270 Sundancers are listed and what's the average asking price?"
- "Compare the market for pontoon boats vs. deck boats in Minnesota"
- "Tell me more about the second listing"

## Data

Search criteria you give Claude (boat type, budget, location and similar) are sent to the Boat Trader MCP server, which returns current listings. The plugin stores nothing itself and needs no API keys.

## Install

**Claude Code**

```
/plugin marketplace add <github-org>/claude-plugin-boattrader
/plugin install boattrader@boattrader
```

**Local testing**

```
claude --plugin-dir ./claude-plugin-boattrader
```

**claude.ai / Cowork**: zip the repo contents and use Customize > Plugins > Add > Upload plugin, then connect the connector from the plugin's Connectors tab.
