# TerriTool for Claude

TerriTool is a field sales CRM. This plugin teaches Claude how to work your TerriTool account through the TerriTool connector: look up saved accounts by city, ZIP or name, open a company's profile and notes, hunt new leads in a US city or ZIP with AI and save them after a credit preview, discover and redeem decision-maker contacts, build and publish optimized driving routes, get the next stop while driving, mark visits and log meetings, calls and activities. Managers also get their team roster, territory coverage, a territory-based proposal for distributing a lead hunt across reps, routes published for a named rep, and period KPIs with a per-rep leaderboard that Claude can render as an Artifact.

One plugin for individual field sales reps and managers. Version 1.0.0.

Use the field-sales skill for your own accounts, leads, routes and visits. Use the managers skill for team assignments, rep routes and performance. The authenticated TerriTool account and server permissions determine access; installing both skills does not grant a manager role. Credit-consuming actions (saving AI leads, redeeming contact details) always show a preview with the exact credit cost and run only after you confirm; credits come from your existing TerriTool plan and no payment details are collected.

What the plugin runs, sends and fetches: it contains skills only, no hooks, scripts or local servers. Every tool call goes to the TerriTool MCP server below over HTTPS with the OAuth token Claude obtains when you sign in. Nothing is sent anywhere else.

Requires an active TerriTool subscription (https://www.territool.com). Manager tools require the TerriTool manager role.

The plugin uses one MCP connection at https://app.territool.com/ai/mcp, the same server as the TerriTool connector in the Claude directory. Sign in with your own TerriTool account when Claude asks. No credentials are included.

Guide: https://app.territool.com/claude-plugin · Privacy: https://app.territool.com/claude-plugin/privacy/ · Terms: https://app.territool.com/claude-plugin/terms/ · Support: support@territool.com

## Install in Claude Code

```
/plugin install territool --marketplace DhruvDave01/territool-plugins
```
