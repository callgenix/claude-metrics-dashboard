# A Weekend-Long Pet Project: MCP 101

## Building a Claude Usage Dashboard in **8 Beginner-Friendly Steps**

Before I could bring Claude and MCP into my day-to-day work, I needed to understand how their components actually fit together. That was my first priority for this weekend project.

The second need lined up nicely with the first: my Pro plan kept catching me off guard, having to wait 4+ hours for Claude to release a new allowance. So I set out to create a standalone, visually clean HTML dashboard into which Claude would insert its metered usage information.

The end result: just tell Claude to update the dashboard, and it navigates to the Settings page, reads the numbers, and updates the HTML file automatically. No manual copying and no third-party tools.

And in the process, I've built a working mental model of how Claude Desktop and MCP work together, which is exactly what I needed before taking this further at work.

> Note: you need a paid Claude plan to follow these steps.

---

![Claude Usage Dashboard — light background](https://raw.githubusercontent.com/callgenix/claude-metrics-dashboard/main/assets/LINKEDIN-carroussel-00-LB-vGold.png)

---

# Quick Start

## What you need

- Node.js
- Claude Desktop
- Claude for Chrome
- Paid Claude plan

## Configure MCP Filesystem

Locate or create:

`C:/Users/[YOUR USERNAME]/AppData/Roaming/Claude/claude_desktop_config.json`

Replace `C:/CODE` with your own folder.

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:/CODE"
      ]
    }
  }
}
```

Restart Claude Desktop completely.

## Download the dashboard file

Download `claude-usage.html` from the [releases page](https://github.com/callgenix/claude-metrics-dashboard/releases/download/v1.0.0/claude-usage.html) and place it inside the same folder you configured above (e.g. `C:/CODE`).

This is the file Claude will read and update during each fetch.

## Ask Claude to update the dashboard

Once Claude Desktop, Claude for Chrome, and the MCP Filesystem are connected properly, prompts like:

> "Update my Claude usage dashboard"

or

> "Fetch my dashboard data"

are often enough for Claude to infer the workflow automatically.

In some situations, especially after reconnecting tools or starting a fresh conversation, a more explicit instruction may help:

> "Open my Claude usage pages, extract the visible metrics, then update claude-usage.html in my MCP filesystem folder."

Approve any browser or connector permissions if prompted.

---

# What Actually Happens

Claude navigates to the Claude usage pages, extracts the visible usage values, then updates the local HTML dashboard file through the MCP Filesystem.

MCP (Model Context Protocol) is an open standard, not exclusive to Claude, that allows AI models to connect to external tools and services. This project uses two MCP capabilities: filesystem access and browser control via the Chrome extension.

The workflow relies on:

- Claude Desktop
- Claude for Chrome
- MCP Filesystem access
- Your active logged-in browser session

No APIs.
No credential storage.
No manual copy-and-paste.

---

# Hurdles I've Encountered Along the Way

Even after successfully setting everything up and running multiple fetch cycles, I still occasionally hit situations where Claude does not immediately execute the workflow as expected.

What I learned is that MCP orchestration is surprisingly powerful, but also dependent on several moving parts being aligned simultaneously.

For example, if:

- Claude Desktop is already configured with the Filesystem MCP
- the MCP folder is accessible
- `claude-usage.html` already exists
- Claude for Chrome is installed and connected
- browser permissions were previously granted
- the current conversation has tool access enabled

...then even a completely cold conversation can often handle prompts like:

> "Update my Claude usage dashboard"

or

> "Fetch my dashboard data"

At that point, Claude is usually capable of inferring the entire workflow automatically:

1. Open the Claude usage pages
2. Read the visible metrics
3. Locate the dashboard HTML file inside the MCP-mounted folder
4. Update the file with the latest values

When one of the components above is missing, disconnected, expired, or blocked, Claude may partially fail the chain or require more explicit instructions.

Some examples I've personally encountered:

- Claude for Chrome silently disconnected
- Browser permissions needing reapproval
- MCP filesystem folder path mismatch
- Conversation opened without tool access enabled
- Chrome tabs already open but inaccessible to Claude
- Claude Desktop requiring a full restart after MCP changes
- HTML file moved or renamed outside the mounted folder
- Prompts too vague during a fresh conversation

What I found is that MCP workflows behave much more like coordinating distributed components than issuing a single AI command.

Debugging those small hurdles ended up teaching me far more about MCP architecture than the dashboard itself.

---

# Optional Reading

| Metric | Reset Behavior |
|---|---|
| Session window | Approximately every 5 hours |
| Weekly plan | Based on the schedule displayed in your Claude account |
| API credit balance | Does not reset automatically |
| Routines and Design usage | Sub-features visible in the usage page. Reset cadence varies; check your account for the current schedule. |

---

# A Note on Scope

This started as a personal experiment to better understand how Claude Desktop, MCP, browser automation, and filesystem access work together in practice.

It uses Claude Desktop, Claude for Chrome, and the MCP filesystem server working together.

The dashboard simply reads the same information already visible in your Claude account pages.

---

# Contributing

Contributions are welcome for specific features. The next planned addition is an 80% session alert, a browser notification that fires when your current session reaches 80% of its allowance, giving you enough time to wrap up before Claude cuts you off. If you'd like to build it, open an issue first to avoid duplicate work.

---

# Dark Background Version

This dashboard uses a light theme. A dark background version was built during development. If you would like to see it published, leave a comment on the LinkedIn post: posted on May 27 as "Building a Claude usage dashboard in 8 beginner-friendly steps, a weekend-long MCP 101 project." Alternatively, open an issue on this repo with the title "Dark version please" and if there is enough interest, it goes live.

---

*Not affiliated with or endorsed by Anthropic.*

*Always review MCP configurations before granting filesystem or browser access.*
