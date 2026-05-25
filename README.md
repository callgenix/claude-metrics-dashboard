# Claude Metrics Dashboard

![Claude Metrics Dashboard](screenshots/dashboard-main.jpg)

A lightweight Claude usage dashboard powered by MCP filesystem access and browser automation through the Claude Chrome extension.

This small weekend project started as a simple convenience experiment: creating a persistent, at-a-glance dashboard showing Claude session usage, weekly plan limits, API credits, and related metrics in one place.

For experienced MCP users, none of this will feel particularly new. The goal here is different: helping Claude Pro users who have never touched MCP before understand, through a practical real-world project, how Claude Desktop can interact with local files and browser sessions outside the chat window.

---

# What This Dashboard Tracks

## Session Window

Tracks the current Claude session usage window and estimated reset time.

## Weekly Plan Usage

Displays weekly plan consumption and remaining capacity.

## API Budget

Reads Anthropic developer API credit balance directly from the billing page.

## Routines and Claude Design

Displays additional usage metrics available inside Claude usage pages.

---

# Why I Built This

Claude already exposes usage information through its interface, but I wanted a faster and more visual “control panel” I could leave open on a second monitor during long work sessions.

The project also became a practical learning exercise around two MCP capabilities:

* Filesystem access
* Browser interaction through the Claude Chrome extension

Together, these capabilities reveal a much broader picture of what the Claude ecosystem can do outside the traditional chat interface.

---

# MCP Concepts Demonstrated

## Filesystem MCP Server

The filesystem server allows Claude Desktop to:

* read local files,
* update local files,
* write dashboard data directly into HTML files.

Example configuration file location:

```text
C:\Users\[YOUR WINDOWS USERNAME]\AppData\Roaming\Claude\claude_desktop_config.json
```

Example MCP configuration:

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

---

## Browser Access Through Claude Chrome Extension

The Claude Chrome extension allows Claude Desktop to:

* open web pages,
* navigate Claude usage pages,
* read live browser data,
* update the dashboard automatically.

![MCP Browser Tabs](screenshots/mcp-browser-tabs.jpg)

---

# Browser Automation in Action

When Claude begins interacting with Chrome, you will see browser automation indicators such as:

![Chrome Notification](screenshots/chrome-notification-band.jpg)

Claude then navigates to:

* `claude.ai/settings/usage`
* `platform.claude.com/settings/billing`

and reads the required metrics directly from the browser DOM.

![Usage Page](screenshots/usage-page.jpg)

---

# Architecture Overview

The automation flow currently works as follows:

![Architecture Overview](screenshots/architecture-table.jpg)

---

# Installation Guide

## 1. Install Node.js

Download and install Node.js:

https://nodejs.org/

This also installs `npx`, which Claude Desktop uses to launch MCP servers.

---

## 2. Verify Node.js Installation

Open a Windows command prompt:

```text
WINDOWS + R
cmd
```

Then verify:

```bash
node -v
npx -v
```

If both commands return version numbers successfully, Claude Desktop should be able to launch MCP servers correctly.

---

## 3. Install Claude Desktop

Download:

https://claude.ai/download

Important:
This project requires Claude Desktop, not only the browser version of Claude.

---

## 4. Install the Claude Chrome Extension

Install the official Claude extension published by Anthropic from the Chrome Web Store.

This extension enables browser interaction between Claude Desktop and Chrome.

---

## 5. Create a Working Folder

Example:

```text
C:\CODE
```

Save the dashboard HTML file inside this folder.

---

## 6. Configure MCP Filesystem Access

Navigate to:

```text
C:\Users\[YOUR WINDOWS USERNAME]\AppData\Roaming\Claude\
```

Locate or create:

```text
claude_desktop_config.json
```

Paste the MCP configuration shown earlier in this README.

---

## 7. Restart Claude Desktop

Completely close and reopen Claude Desktop.

The filesystem MCP server activates during startup.

---

## 8. Ask Claude to Update the Dashboard

Inside Claude Desktop, type something natural such as:

```text
Fetch my dashboard data and update C:\CODE\claude-usage.html
```

or:

```text
Refresh my Claude usage dashboard
```

Claude will:

* open your usage pages,
* read current metrics,
* update the local dashboard HTML file automatically.

---

# Final Dashboard

![Final Dashboard](screenshots/dashboard-main.jpg)

---

# Security Notes

This project does not use:

* unofficial browser scraping tools,
* third-party automation frameworks,
* external APIs,
* or credential storage.

Browser interaction happens through the official Claude Chrome extension and Claude Desktop permissions.

Always review any MCP configuration before granting filesystem access.

---

# Important Disclaimer

This project was built through experimentation, documentation reading, trial-and-error, and practical exploration of MCP capabilities.

It is not an official Anthropic project, nor an authoritative implementation reference for MCP architecture or security practices.

The goal is educational and exploratory: helping newer users better understand how Claude Desktop, MCP servers, browser access, and local file interaction can work together in practical workflows.

---

# Related Links

* CallGenix: https://www.callgenix.com
* Claude Desktop: https://claude.ai/download
* MCP Documentation: https://modelcontextprotocol.io
