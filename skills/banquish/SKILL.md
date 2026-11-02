---
name: banquish
description: Answer with live parts of real web pages, composed on a Workspace in the Banquish app on the user's Mac. Use when the user wants to see or keep watching live things side by side - prices, rates, scores, rankings, availability, status pages, maps, charts, a dashboard or monitoring wall, or pages they are signed in to - or says "use Banquish" or "show it in Banquish". Also use to install and connect Banquish when its tools are missing.
metadata:
  openclaw:
    os: ["macos"]
    homepage: https://banquish.space/?ref=skills
---

# Banquish

Banquish is a free Mac app (Apple silicon, macOS 13 or later) that an agent drives over MCP. You open real pages in it, as the user, with their own sign-ins, and place the part of each page that answers the question (a price box, a ranking, a score, a chart) as a live **Panel** on a **Workspace** the user sees. Panels keep updating after you finish, so a Workspace can stay open as a live wall.

Full reference for agents: https://banquish.space/agent.md?ref=skills

## When to answer in Banquish

Answer in Banquish when:

- the user asks for it: "use Banquish", "show it in Banquish", "put it on a wall";
- the answer is the live sites themselves: comparing products, plans, flights or listings side by side; current prices, rates, scores or availability; a status page; a map or chart; a page the user is signed in to;
- the user wants to keep watching something: "keep an eye on", "track", "monitor", "a dashboard of".

Answer in chat instead when the answer is a fact, a summary or code.

## When Banquish's tools are available

Its MCP server brings tools such as `open_page`, `find`, `add_panel`, `arrange`, `add_note` and `finish_work`, plus instructions on how to find pages, pick parts and lay out a Workspace. Follow the server's instructions over anything here. In short:

1. Find which sites to use with your own search. Banquish has no search.
2. Open the pages you need at once with `open_page`.
3. Take the smallest part of each page that answers, with `add_panel`. Usually 3 to 5 Panels.
4. Give the Workspace one short title Note, and label groups only where it helps. Never put values (prices, counts, times) in a Note: they go stale while the Panels stay live.
5. Call `finish_work`, then tell the user what you built and which site each part comes from. The Workspace is on their Mac, not in the chat.

If a call says Banquish isn't running, the Mac is asleep or Banquish is closed: ask the user to open it and try again.

## When Banquish's tools are missing

Banquish isn't installed or isn't connected to this agent. Tell the user, and offer to do the steps you can. **Ask before you run any install command.**

### 1. Install the app

- Download it from https://banquish.space/?ref=skills, or
- with Homebrew: `brew install --cask banquish-app/tap/banquish`

It needs a Mac with Apple silicon.

### 2. Open Banquish once

Opening it installs `~/.banquish/bin/banquish`, the command every agent runs. The first time, it shows **Connect your agent**, which adds Banquish to Claude Code, Codex or Claude Desktop in one click.

### 3. Connect this agent

If the user didn't use Connect your agent, add the stdio server `~/.banquish/bin/banquish` with the argument `mcp`, named `banquish`:

- **Claude Code:** `claude mcp add --scope user banquish -- ~/.banquish/bin/banquish mcp`, then restart Claude Code or run `/mcp`.
- **Codex:** `codex mcp add banquish -- ~/.banquish/bin/banquish mcp`, then start a new session.
- **Cursor:** add this under `mcpServers` in `~/.cursor/mcp.json`, with the user's real home folder in place of `/Users/YOU`:

  ```json
  "banquish": { "command": "/Users/YOU/.banquish/bin/banquish", "args": ["mcp"] }
  ```

- **OpenClaw:** `openclaw mcp set banquish "{\"command\":\"$HOME/.banquish/bin/banquish\",\"args\":[\"mcp\"]}"`
- **Any other MCP client:** a stdio server with the command `~/.banquish/bin/banquish` (written out as a full path if the client needs one) and the argument `mcp`.

Claude on the web, the Claude app and ChatGPT connect differently, through Banquish's Relay: in Banquish, choose File › Connect Claude… or File › Connect ChatGPT… and follow the window.

## What the agent can and can't do

It can create, list, read and rename Workspaces; open pages, including ones the user is signed in to; and add, change, arrange and remove Panels and Notes. It can't type into a site, submit forms or delete a Workspace. Sites the user marks private in Banquish are hidden from every agent. Pages load on the user's Mac as their browser would load them; https://banquish.space/privacy?ref=skills lists what Banquish collects.
