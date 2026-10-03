# Chewable Foodie for ChatGPT and Codex

Use your [Foodie](https://foodie.chewable.fit) recipes, your family's meal plan
and your shared shopping list from ChatGPT or Codex.

Ask things like:

- "Plan dinners for this week from my Foodie recipes"
- "What's on my shopping list?"
- "Add the ingredients for my lasagne to the shopping list"
- "Save this recipe to Foodie"

Changes show up at once in the Foodie app, for everyone in your family.

## Install

1. In ChatGPT or Codex, open **Plugins → Add → Add a marketplace**.
2. Paste `https://github.com/chewablefit/foodie-plugin` as the source. Leave
   Git ref and Sparse paths empty.
3. Install **Chewable Foodie** and sign in with Apple, using the same Apple ID
   as in the Foodie app.

You need a Foodie account first: sign in once in the iPhone app.

## What's inside

| Path | What it is |
|---|---|
| `plugins/chewable-foodie/plugin.json` | Name, description and links for the plugin directory |
| `plugins/chewable-foodie/mcp.json` | The Foodie MCP server, `https://foodieapi.chewable.fit/mcp` |
| `plugins/chewable-foodie/skills/foodie/SKILL.md` | How the assistant should use the Foodie tools |
| `.agents/plugins/marketplace.json` | Makes this repo installable as a marketplace |

## Without the plugin

Any MCP client can connect to `https://foodieapi.chewable.fit/mcp` directly.
See the [connection guide](https://foodie.chewable.fit/connect).

## Privacy

[Privacy policy](https://foodie.chewable.fit/privacy) ·
[Terms](https://foodie.chewable.fit/terms). Disconnect at any time in the
Foodie app under Settings → ChatGPT & Claude.
