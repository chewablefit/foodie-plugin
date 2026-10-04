# Chewable Foodie for ChatGPT, Codex and Claude

Use your [Foodie](https://foodie.chewable.fit) recipes, your family's meal plan
and your shared shopping list from ChatGPT, Codex or Claude.

Ask things like:

- "Plan dinners for this week from my Foodie recipes"
- "What's on my shopping list?"
- "Add the ingredients for my lasagne to the shopping list"
- "Save this recipe to Foodie: https://…" (recipe sites, Instagram, TikTok, YouTube)
- "What did we eat last week?"

Changes show up at once in the Foodie app, for everyone in your family.

## Install

1. In ChatGPT or Codex, open **Plugins → Add → Add a marketplace**.
2. Paste `https://github.com/chewablefit/foodie-plugin` as the source. Leave
   Git ref and Sparse paths empty.
3. Install **Chewable Foodie** and sign in with Apple, using the same Apple ID
   as in the Foodie app.

You need a Foodie account first: sign in once in the iPhone app.

## Install in Claude

In Claude Code:

```
/plugin marketplace add chewablefit/foodie-plugin
/plugin install chewable-foodie@chewable
```

Or from your shell: `claude plugin marketplace add chewablefit/foodie-plugin`,
then `claude plugin install chewable-foodie@chewable`. Sign in with Apple when
Claude asks to connect the Foodie server.

In claude.ai or the Claude desktop app you can also skip the plugin: Settings →
Connectors → Add custom connector, paste `https://foodieapi.chewable.fit/mcp`
and sign in with Apple.

## What's inside

| Path | What it is |
|---|---|
| `plugins/chewable-foodie/plugin.json` | Name, description and links for the plugin directory |
| `plugins/chewable-foodie/mcp.json` | The Foodie MCP server, `https://foodieapi.chewable.fit/mcp` |
| `plugins/chewable-foodie/skills/foodie/SKILL.md` | How the assistant should use the Foodie tools |
| `plugins/chewable-foodie/.mcp.json` | The same server, in Claude's format |
| `plugins/chewable-foodie/.claude-plugin/plugin.json` | The plugin's manifest for Claude |
| `.agents/plugins/marketplace.json` | Makes this repo installable as a marketplace in ChatGPT and Codex |
| `.claude-plugin/marketplace.json` | Makes this repo installable as a marketplace in Claude |

## Without the plugin

Any MCP client can connect to `https://foodieapi.chewable.fit/mcp` directly.
See the [connection guide](https://foodie.chewable.fit/connect).

## Privacy

[Privacy policy](https://foodie.chewable.fit/privacy) ·
[Terms](https://foodie.chewable.fit/terms). Disconnect at any time in the
Foodie app under Settings → ChatGPT & Claude.
