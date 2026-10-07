# Chewable Foodie

Chewable Foodie connects your AI assistant to the [Foodie](https://foodie.chewable.fit)
app: your recipe library, your family's weekly meal plan and your shared
shopping list. Everything you change shows up at once in the Foodie app on
iPhone, for everyone in your family.

## What you can do

- Find recipes by name or ingredient, and see which ones you can make with what
  you have at home, and what is missing
- Plan dinners for the week from recipes you already have
- Add a recipe to the shopping list as one linked entry, ask for separate
  ingredients instead, add single items, and tick off what you bought
- Save a recipe from a link: a recipe site, an Instagram or TikTok post, or a
  YouTube video
- Cook step by step, with a timer where a step names a time, and rate what you
  cooked

Adding a recipe uses `add_recipe_to_shopping_list` with its `recipeId`.
By default, it adds one entry linked to the recipe, with its name and
servings. `expandIngredients: true` adds separate ingredient items when
requested. `add_to_shopping_list` adds groceries or selected ingredients;
it must not replace a linked recipe with a plain item bearing its name.

## What it contains

- A skill, `skills/foodie/SKILL.md`, that teaches the assistant how to use the
  Foodie tools well: read the meal plan before planning, confirm before
  deleting, never invent a recipe.
- One remote MCP server, `https://foodieapi.chewable.fit/mcp`, run by Chewable.
  The plugin runs no code on your machine.

## What it sends and fetches

- The plugin connects only to `foodieapi.chewable.fit`, Foodie's own server.
  You sign in with your Foodie account (Sign in with Apple, OAuth). Without
  that sign-in it can do nothing.
- Tool calls read and change your Foodie recipes, meal plan, shopping list and
  cooking history. They do not read your conversations, memory or files.
- When you ask to import a recipe from a link, Foodie's server fetches that one
  page and returns its recipe or text. When you save a recipe with a photo,
  Foodie stores its own copy of the photo.
- Recipe photos shown in the chat load from `images.chewable.fit`, Foodie's
  image server.
- Free Foodie accounts have 50 tool calls a day; Foodie Premium has no limit.

## Requirements

A Foodie account: download Foodie for iPhone and sign in once with Apple.

## Privacy

Read the [privacy policy](https://foodie.chewable.fit/privacy) and the
[terms](https://foodie.chewable.fit/terms). You can see and disconnect connected
assistants at any time in the Foodie app under Settings → ChatGPT & Claude.
Support: [foodie.chewable.fit](https://foodie.chewable.fit).
