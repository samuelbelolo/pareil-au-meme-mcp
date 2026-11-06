# Pareil au même MCP server

Check whether a brand name is already registered as a trademark in France, by spelling and by sound.

Pareil au même is a hosted, read-only MCP server. It compares a name with more than 1.4 million French trademarks in force, from the public data of INPI, the French trademark office. It is free, needs no account or API key, and has nothing to install: you add one address to your agent.

```
https://pareil-au-meme.fr/mcp
```

Transport: Streamable HTTP. Authentication: none.

## What it does

The server ranks the trademarks close to a name by level of similarity, from the most to the least serious:

1. **Identical**: the same name, or an element of the trademark identical to it.
2. **Sounds the same**: written differently, pronounced the same (Quelvo and Quelveau).
3. **Similar**: one or two letters apart when spoken.
4. **Contains the name**: a longer trademark that includes it.
5. **Shares an element**: one of the words of the name is an existing trademark.

Tell your agent what you sell, and the trademarks in your line of business come first. The others stay listed, because a well-known trademark is protected beyond its classes.

Every answer gives the date of the data and a sentence on the search's limits.

## Tools

Both tools are read-only and idempotent. Their texts are in French.

| Tool                | Input                                                                                                       | Output                                                                                                                                                                        |
| ------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `search_trademarks` | `nom`, the name to check (1 to 100 characters). `classes`, optional Nice classes of the business (1 to 45). | The five levels above, each with its total and up to 25 trademarks (number, name, status, classes, filing date, link to data.inpi.fr), the data's dates, the limits sentence. |
| `list_nice_classes` | None.                                                                                                       | The 45 Nice classes, each with a short plain-language label, to pick the classes of a business.                                                                               |

## Add it to your agent

### VS Code (GitHub Copilot)

[Install in VS Code](https://vscode.dev/redirect/mcp/install?name=pareil-au-meme&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fpareil-au-meme.fr%2Fmcp%22%7D), or add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "pareil-au-meme": {
      "type": "http",
      "url": "https://pareil-au-meme.fr/mcp"
    }
  }
}
```

### Claude

On claude.ai and Claude Desktop, open the [Pareil au même listing](https://claude.ai/directory/connectors/pareil-au-meme) in Claude's connectors directory and connect it.

In Claude Code:

```sh
claude mcp add --transport http pareil-au-meme https://pareil-au-meme.fr/mcp
```

Add `--scope user` to have it in every project.

### Cursor

[Install in Cursor](https://cursor.com/install-mcp?name=pareil-au-meme&config=eyJ1cmwiOiJodHRwczovL3BhcmVpbC1hdS1tZW1lLmZyL21jcCJ9), or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "pareil-au-meme": {
      "url": "https://pareil-au-meme.fr/mcp"
    }
  }
}
```

### Codex

```sh
codex mcp add pareil-au-meme --url https://pareil-au-meme.fr/mcp
```

### ChatGPT

On paid plans, on the web: turn on developer mode in ChatGPT's settings, then create an app with the address `https://pareil-au-meme.fr/mcp`.

### Any other agent

Add a remote MCP server at `https://pareil-au-meme.fr/mcp`, over Streamable HTTP, with no authentication. Most agents read the same configuration as Cursor.

## Try it

- "Is the name Brivane already registered as a trademark in France?"
- "Which trademarks look like Quelvo for a clothing brand?"
- "In which Nice class should I register a coffee brand?"

The agent can call `list_nice_classes` first to find the classes of the business, then `search_trademarks` with the name and those classes.

## Limits

- French trademarks only. The search sees neither logos, nor European Union or international trademarks, nor filings not yet published, nor company names.
- It is a risk signal, not legal advice. A search with no close trademark does not mean the name can be registered or used safely. For a specific case, ask a trademark attorney.
- The data follow INPI's weekly publications.
- Searches are limited to 20 a minute per IP address. Past that, the tool answers with an error in French.

## Privacy

The server reads and never writes. It keeps neither the name nor the classes it receives.

## Links

- Documentation, in French: https://pareil-au-meme.fr/serveur-mcp
- Official MCP Registry: `fr.pareil-au-meme/mcp`
- Claude connectors directory: https://claude.ai/directory/connectors/pareil-au-meme
- Website, which also checks domain names: https://pareil-au-meme.fr
- Contact: contact@pareil-au-meme.fr

## About this repository

The server's source code is not published. This repository describes the hosted server for the MCP Registry and GitHub's MCP catalogue.
