# TerriTool plugins

Generated plugin kits for the TerriTool field sales CRM (https://www.territool.com). Every kit talks to the same remote MCP server, `https://app.territool.com/ai/mcp`, and contains skills and manifests only: no application code, no credentials.

- `territool-claude/`: the TerriTool plugin for Claude (claude.ai, Claude Desktop, Cowork, Claude Code), submitted to the Claude directory.
- `territool-chatgpt/`: the unified TerriTool plugin kit for ChatGPT and Codex.

## Install in Claude Code

    /plugin install territool --marketplace DhruvDave01/territool-plugins

Setup guide: https://app.territool.com/claude-plugin
Privacy policy: https://app.territool.com/claude-plugin/privacy/
Terms: https://app.territool.com/claude-plugin/terms/
Support: support@territool.com

This repository is generated from the private TerriTool application repository by `scripts/export_claude_directory_repo.py`; edit the sources there, not here.
