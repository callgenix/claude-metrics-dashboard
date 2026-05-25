# Claude Metrics Dashboard

![Claude Metrics Dashboard](screenshots/dashboard-main.jpg)

One HTML file. Live metrics from your Claude account — session window, weekly plan, and API credits.

---

## Download

👉 **[Download claude-usage.html](https://github.com/callgenix/claude-metrics-dashboard/releases/download/v1.0.0/claude-usage.html)**


Save it anywhere. Open it in Chrome. That is it.

---

## Setup — 4 steps

**What you need first:** Node.js, Claude Desktop, and the Claude for Chrome extension.

**1. Configure filesystem access**

Locate or create:
```
C:\Users\[YOUR USERNAME]\AppData\Roaming\Claude\claude_desktop_config.json
```

Paste:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "C:\\CODE"]
    }
  }
}
```

**2. Restart Claude Desktop** — completely close and reopen it.

**3. Say this** in an established Claude Desktop conversation:

> *"Fetch my dashboard data"*

Approve the one-time browser permissions when prompted.

**4. Open `claude-usage.html` in Chrome and press F5.**

Done.

> Live fetch only works from an established conversation with active MCP tools — not a fresh tab and not a Project conversation.

---

&nbsp;

---

## The Claude product ecosystem

[![Claude Product Ecosystem](ecosystem.svg)](https://github.com/callgenix/claude-metrics-dashboard/blob/main/ecosystem.svg)

Every node is a real product. Read left to right, top to bottom.

---

## Optional reading

<details>
<summary><strong>What it tracks</strong></summary>
<br>

| Metric | Resets |
|---|---|
| Session window | Every ~5 hours (rolling) |
| Weekly plan | Every Tuesday at 9 AM |
| API credit balance | Never — only depletes with direct API calls |
| Routines and Design usage | Daily / weekly |

Claude measures session and weekly capacity in a proprietary unit. Anthropic does not publish the exact token equivalence. The percentages shown here come directly from your account page.

</details>

<details>
<summary><strong>How it works</strong></summary>
<br>

Two MCP capabilities combine to make this possible.

**Filesystem MCP** — a one-line config tells Claude Desktop which local folder to access. Claude reads the dashboard HTML and writes updated values back automatically.

**Claude for Chrome** — the official Chrome extension lets Claude Desktop open browser tabs, navigate to your usage and billing pages, and read live data from the DOM.

| Data | Source | Method |
|---|---|---|
| Session %, Weekly %, Routines, Design | `claude.ai/settings/usage` | Claude in Chrome reads DOM |
| API credit balance | `platform.claude.com/settings/billing` | Claude in Chrome reads DOM |

</details>

<details>
<summary><strong>Understanding the diagram</strong></summary>
<br>

**1 · At the top of everything sits Anthropic**

Anthropic is the company that builds and trains the Claude AI models. When you hear names like Haiku, Sonnet, and Opus, those are the actual AI brains behind every Claude experience. Think of them as engines with different sizes and price points: Haiku is fast and affordable for simple tasks, Sonnet is the everyday workhorse for most people, and Opus is the most capable for complex reasoning. Everything else in this diagram is just a way of reaching one of these engines.

**2 · The Claude API — one gateway for everything**

The Claude API lives at platform.claude.com and is the single gateway that all Claude products go through. It is primarily aimed at developers. The API runs on a pay-as-you-go credit system that is completely separate from any chat subscription. Most regular users never interact with it directly, but understanding it matters because everything in this diagram is sitting on top of it.

**3 · Three very different interfaces, same AI underneath**

Claude.ai is the browser and mobile chat interface — the one most people start with. Claude Desktop is the downloadable application that unlocks MCP, which lets Claude interact with your local files and browser. Claude Code is a command-line tool for developers who want Claude to write, test, and reason about code directly in their environment. Same AI underneath all three — very different experiences on top.

**4 · Extensions and tools that plug into each interface**

From claude.ai: Excel and PowerPoint add-ins. From Claude Desktop: Cowork for automation and Claude for Chrome for browser interaction. From Claude Code: VS Code and JetBrains extensions. These tools are not standalone products — they work because of the interface they are attached to.

**5 · The MCP Protocol layer — what makes automation real**

MCP stands for Model Context Protocol. It is an open standard that allows Claude to connect to external systems — your local file system, a browser, third-party APIs, and more. Without MCP, Claude is a capable conversational partner but nothing more. With MCP, Claude can read a file, navigate a web page, pull live data, and write results back — all in a single conversation. The live fetch that powers this dashboard is MCP in action.

</details>

<details>
<summary><strong>Requirements</strong></summary>
<br>

| What | Why |
|---|---|
| Node.js (any recent version) | Claude Desktop uses `npx` to start the filesystem MCP server |
| Claude Desktop | The desktop app is the MCP host — the browser version alone will not work |
| Claude for Chrome | Official Anthropic extension that lets Claude read your usage pages |
| A paid Claude plan | Pro, Max, Team, or Enterprise |

To verify Node.js is properly installed, open a command window and run:
```bash
node -v
npx -v
```
Both should return version numbers. If either fails, reinstall from [nodejs.org](https://nodejs.org).

</details>

<details>
<summary><strong>Compatibility</strong></summary>
<br>

Tested on Windows 11 with Chrome and Claude Pro.

Should work on macOS with the same setup. The filesystem path in the config will need to use forward slashes or macOS-style paths.

</details>

<details>
<summary><strong>A note on scope</strong></summary>
<br>

This is a personal learning project. It uses only official tools published by Anthropic — Claude Desktop, the Claude Chrome extension, and MCP permissions you explicitly approve. It does not scrape, reverse-engineer, or circumvent anything. It reads the same usage data you can see manually by visiting your settings page.

The dashboard works today. Claude's usage page structure may change over time, and the fetch logic may need occasional adjustments if it does.

Want to customize it? Fork the repo and make it your own. That is what GitHub is for.

</details>

---

## Related

- [Callgenix.com](https://www.callgenix.com) — the AI demo catalog where this project lives
- [Claude Desktop](https://claude.ai/download)
- [MCP Documentation](https://modelcontextprotocol.io)

---

*Not affiliated with or endorsed by Anthropic.*
