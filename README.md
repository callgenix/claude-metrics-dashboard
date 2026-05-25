# Claude Metrics Dashboard

![Claude Metrics Dashboard](screenshots/dashboard-main.jpg)

A single HTML file that gives you a persistent, visual layer over Claude's built-in usage data — session window, weekly plan, API credits, and a live fetch that pulls numbers directly from your account pages.

---

## Download

**One file. No install. No dependencies.**

👉 [Download claude-usage.html](https://github.com/callgenix/claude-metrics-dashboard/raw/main/claude-usage.html)

Save it anywhere on your machine — `C:\CODE\` works well. Open it in Chrome. That's it.

Live data fetch requires two additional things already covered in the setup section below.

---

## What it tracks

| Metric | Resets |
|---|---|
| Session window | Every ~5 hours (rolling) |
| Weekly plan | Every Tuesday at 9 AM |
| API credit balance | Never — only depletes with API calls |
| Routines and Design usage | Daily / weekly |

Claude measures session and weekly capacity in a proprietary unit. Anthropic does not publish the exact token equivalence. The percentages shown here come directly from your account page.

---

## What's in the repository

```
claude-metrics-dashboard/
├── README.md
├── claude-usage.html        ← the dashboard (this is the file you need)
└── screenshots/
    ├── dashboard-main.jpg
    ├── usage-page.jpg
    ├── architecture-table.jpg
    ├── chrome-notification-band.jpg
    └── mcp-browser-tabs.jpg
```

The dashboard is entirely self-contained. All styles are inline. There are no external dependencies beyond Google Fonts, which loads automatically.

---

## Requirements

| What | Why |
|---|---|
| Node.js (any recent version) | Claude Desktop uses `npx` to start the filesystem MCP server |
| Claude Desktop | The desktop app is the MCP host — the browser version alone won't work |
| Claude for Chrome | The official Anthropic extension that lets Claude read your usage pages |
| A paid Claude plan | Pro, Max, Team, or Enterprise — free tier does not expose the same usage data |

---

## How it works

Two MCP capabilities combine to make this possible.

**Filesystem MCP** — a one-line config tells Claude Desktop which local folder to access. Claude reads the dashboard HTML and writes updated values back automatically.

**Claude for Chrome** — the official Chrome extension lets Claude Desktop open browser tabs, navigate to your usage and billing pages, and read live data from the DOM.

### Data sources

| Data | Source | Method |
|---|---|---|
| Session %, Weekly %, Routines, Design | `claude.ai/settings/usage` | Claude in Chrome reads DOM |
| API credit balance | `platform.claude.com/settings/billing` | Claude in Chrome reads DOM |

---

## Setup

### Requirements check

Open a command window and confirm both commands return version numbers:

```bash
node -v
npx -v
```

If either fails, Node.js is not properly registered in your system PATH. Reinstall from [nodejs.org](https://nodejs.org) and retry.

### Configure filesystem access

Locate or create this file:

```
C:\Users\[YOUR USERNAME]\AppData\Roaming\Claude\claude_desktop_config.json
```

Paste the following, replacing the path if needed:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\CODE"
      ]
    }
  }
}
```

Windows paths inside JSON require double backslashes.

### Start the dashboard

1. Restart Claude Desktop completely
2. Make sure you are logged into `claude.ai` in Chrome
3. Open an **established** Claude Desktop conversation (not a fresh tab, not a Project)
4. Say something like: *"fetch my dashboard data"*
5. Approve the one-time browser permission prompts for `claude.ai` and `platform.claude.com`
6. Open `claude-usage.html` in Chrome and press F5

The fetch phrase is flexible — Claude understands the intent, not a specific keyword.

> **Important:** The fetch only works from an established conversation with confirmed active MCP tools. Fresh conversations and Project conversations do not have the MCP context loaded.

---

## Architecture overview

![Architecture](screenshots/architecture-table.jpg)

Claude navigates to your usage pages, reads the DOM, and writes the values into your local HTML file. No third-party tools. No external APIs. No credential storage of any kind.

Browser interaction happens through Claude Desktop and the official Claude Chrome extension, using permissions you explicitly approve.

---

## Compatibility

Tested on:
- Windows 11 with Chrome
- Claude Pro plan

Should work on macOS with the same setup. The filesystem path in the config will need to use forward slashes or macOS-style paths.

---

## A note on scope

This is a personal learning project — a practical experiment in combining MCP filesystem access with browser automation through Claude Desktop.

It uses only official tools published by Anthropic. It does not scrape, reverse-engineer, or circumvent anything. It reads the same usage data you can see manually by visiting your settings page.

The dashboard works today. Claude's interfaces and usage page structures may change over time, and the fetch logic may need occasional adjustments if they do.

---

## Related

- [Callgenix.com](https://www.callgenix.com) — the AI demo catalog where this project lives
- [Claude Desktop](https://claude.ai/download)
- [MCP Documentation](https://modelcontextprotocol.io)
- [Claude Chrome Extension](https://chrome.google.com/webstore)

---

*Not affiliated with or endorsed by Anthropic.*
