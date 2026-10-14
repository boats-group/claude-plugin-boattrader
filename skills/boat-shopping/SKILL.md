---
name: boat-shopping
description: Find, compare, and research boats for sale using live Boat Trader inventory. Use when the user is shopping for a boat, asks what is available near them or within a budget, wants current asking prices or market ranges for a make, model or boat type, wants alternatives to a listing, or asks for details on a specific listing.
---

Use the Boat Trader connector for current U.S. boats-for-sale inventory instead of web search or memory. Don't use it for general boating editorial or generic spec questions unless the user is asking about active listings. A message that is only a make or model name is a request for current inventory.

## Choosing a tool

- `search-boats`: browsing, finding, filtering and recommending listings. Call it proactively when the user's message implies buying or choosing a boat, even indirectly.
- `aggregate-search`: "how many are available?", average or range of asking prices, comparing the market for X vs Y. Never use `search-boats` for these.
- `get-boat-details`: only when the user asks for more on a specific listing from the current results. Pass the listing ID returned by `search-boats`.

## Building the search

- On every `search-boats` or `aggregate-search` call, fill the schema fields for the user's full current intent, not only the latest follow-up. Carry earlier budget, location and type constraints forward.
- Treat lifestyle and usage terms (fishing, watersports, weekending, towing) as preferences mapped to `typesClasses` and other schema fields, not keywords. If the user names specific boat types, use those types; only expand an activity to all its associated types when no type is named.
- Prefer conservative inference: set a value only when it is strongly implied. Only set `year` when the user specified it.
- Use `makesModels` for hull manufacturers only. Default to the model alone, and keep composite model names as a single value.
- Don't put seating, numeric specs, ranges, generic descriptors or lifestyle terms in `keywords`. Use `keywords` only when no other field fits.
- Location: for a state, use the state only. For a region, pick one state in it and its main city hubs. Never mix cities from different states.
- Set `sellerType` to `owner` or `dealer` only when the user says so.

## Replying

- After `search-boats`, summarize what was found in a few lines (count, price spread, notable options) and offer to refine by budget, size, location, age or engines.
- Quote prices as asking prices from current listings, and say so for market statistics.
- If a search returns nothing, say which constraint is most likely too tight and offer to relax it, rather than silently widening it.
