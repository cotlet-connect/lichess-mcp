# How to connect Lichess to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Lichess account.** Cotlet.dev connects your own signed-in Lichess account to any AI agent, so you can ask in plain words and the AI accepts team join requests and sends updates to your team for you.

## What you can ask

> Accept the join requests from tom_k and anna_plays to my "Riverside Chess Club" team.

> Show me all pending join requests for my team and who sent them this week.

> Send a message to all members of "Riverside Chess Club": our blitz arena starts Thursday at 7 pm.

> Accept every join request from today, then tell the team that 4 new players joined.

> Message my team that Saturday's lesson with coach Maria moves to 10 am.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Lichess tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"lichess":{"command":"uvx","args":["lichess-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t lichess-mcp .
docker run -i --rm -e COTLET_API_KEY lichess-mcp
```

Tools: `lichess_guide`, `lichess_status`, `lichess_open`, `lichess_read`, `lichess_click`, `lichess_type`, `lichess_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install lichess-mcp        # or run it once: uvx lichess-mcp connect
lichess-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 lichess_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 lichess_agent.py status    # is Lichess ready in your Cotlet.dev account
python3 lichess_agent.py guide     # Lichess screens and sign-in link
python3 lichess_agent.py read      # open Lichess, read the page, close the browser
python3 lichess_agent.py tools     # list Cotlet.dev tools
python3 lichess_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Lichess users

**Does Lichess have an API?**

Lichess has a full, free REST API with personal and OAuth tokens, but no official MCP server (checked 17 Oct 2026). The API covers teams, Arena and Swiss tournaments, studies, broadcasts, challenges and game export, so the gap is a hosted, maintained MCP with no token to create, scope or revoke. Cotlet.dev works in your own signed-in Lichess account, so your AI agent can accept team join requests and message your team with no API key and no code.

**How do I connect Lichess to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Lichess once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Lichess API key.

**Is there a way to use Claude with Lichess?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Lichess account.

**Is there a Lichess MCP server?**

We found no official Lichess app in the ChatGPT or Claude directories. Cotlet.dev is a hosted MCP server that works in Lichess for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Lichess on Cotlet.dev](https://cotlet.dev/integrations/lichess-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=lichess&utm_content=find)
- [PyPI package lichess-mcp](https://pypi.org/project/lichess-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-lichess-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/lichess-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=lichess

Start free: https://cotlet.dev/signup?app=lichess&utm_source=github&utm_medium=readme&utm_campaign=lichess
