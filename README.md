# Chewable Foodie for Codex, Claude and ChatGPT

Use your [Foodie](https://foodie.chewable.fit) recipes, your family's meal plan
and your shared shopping list from your AI assistant. Everything you change
shows up at once in the Foodie app, for everyone in your family.

Ask things like:

- "Plan dinners for this week from my Foodie recipes"
- "I have eggs, spinach and feta. What can I make?"
- "Add the ingredients for my lasagne to the shopping list"
- "Save this recipe to Foodie: https://…" (recipe sites, Instagram, TikTok, YouTube)
- "Walk me through the carbonara, step by step"
- "What did we eat last week?"

**Before you start:** you need a Foodie account. Sign in once in the Foodie
app on iPhone. When the assistant asks you to connect Foodie, sign in with the
same Apple ID.

## Codex

In the Codex app, or the Codex tab of the ChatGPT desktop app:

1. Open **Plugins → Add → Add a marketplace**.
2. Paste `https://github.com/chewablefit/foodie-plugin` as the source. Leave
   Git ref and Sparse paths empty.
3. Install **Chewable Foodie** and sign in with Apple.

In Codex CLI, `/plugins` opens the same plugin browser.

## Claude

**Claude Code:**

```
/plugin marketplace add chewablefit/foodie-plugin
/plugin install chewable-foodie@chewable
```

From your shell, the same is `claude plugin marketplace add chewablefit/foodie-plugin`
and `claude plugin install chewable-foodie@chewable`. Sign in with Apple when
Claude asks to connect the Foodie server.

**claude.ai and the Claude desktop app:** Settings → Connectors → Add custom
connector. Paste `https://foodieapi.chewable.fit/mcp` and sign in with Apple.

## ChatGPT

A plugin from this repo does not reach ordinary ChatGPT chats yet; that comes
with the listing in ChatGPT's plugin directory. Until then, connect the server
yourself (needs a paid plan):

1. Settings → Security and login → turn on **Developer mode**.
2. Open **Plugins**, press **+**, and enter `https://foodieapi.chewable.fit/mcp`
   with OAuth. Sign in with Apple.

## What works where

| | Codex | Claude Code | claude.ai, Claude desktop | ChatGPT |
|---|---|---|---|---|
| All Foodie tools | ✓ | ✓ | ✓ | ✓ |
| The Foodie skill (how to use the tools well) | ✓ | ✓ | connector instructions | connector instructions |
| Recipe cards, cook mode with timers, ticking off the list | | | ✓ | ✓ |

Clients that connect the server without the plugin get the same rules in a
shorter form, from the server's own instructions.

## What's inside

| Path | For | What it is |
|---|---|---|
| `plugins/chewable-foodie/skills/foodie/SKILL.md` | both | How the assistant should use the Foodie tools |
| `plugins/chewable-foodie/assets/` | both | Icon and logo |
| `.agents/plugins/marketplace.json` | Codex | Makes this repo a plugin marketplace |
| `plugins/chewable-foodie/plugin.json` | Codex | Name, description and links for the plugin directory |
| `plugins/chewable-foodie/mcp.json` | Codex | The Foodie server, `https://foodieapi.chewable.fit/mcp` |
| `.claude-plugin/marketplace.json` | Claude | Makes this repo a plugin marketplace |
| `plugins/chewable-foodie/.claude-plugin/plugin.json` | Claude | The plugin's manifest |
| `plugins/chewable-foodie/.mcp.json` | Claude | The same server, in Claude's format |

There is one skill for both. When you change it, bump `version` in both
`plugin.json` files so installed copies update.

## Privacy

[Privacy policy](https://foodie.chewable.fit/privacy) ·
[Terms](https://foodie.chewable.fit/terms) ·
[Connection guide](https://foodie.chewable.fit/connect). See and disconnect
connected assistants at any time in the Foodie app under Settings → ChatGPT &
Claude.
