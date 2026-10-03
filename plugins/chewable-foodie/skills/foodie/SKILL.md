---
name: foodie
description: Use the user's Chewable Foodie recipes, family meal plan and shared shopping list. Use when the user asks what to cook, wants to plan meals for a day or week, asks about or changes their shopping or grocery list, or wants to save a recipe to Foodie.
---

# Chewable Foodie

Foodie is a family recipe app. The meal plan and the shopping list are shared
by everyone in the user's family, and every change shows up in their app at
once. Treat writes as visible to other people.

## Finding recipes

- Start with `search_recipes`. It returns summaries only. Call `get_recipe`
  before you quote ingredients or steps; never guess them.
- An empty query lists the most recently saved recipes. Use it for "what
  have I saved lately" or when the user has no dish in mind.
- Suggest recipes the user already has before inventing new ones.

## Planning meals

1. `get_meal_plan` for the week first, so you know what is already planned.
2. Propose the plan in chat and wait for a yes.
3. `plan_meal` once per day and meal. It replaces what is already planned
   for that slot, so say so when a slot is taken.

`plan_meal` only takes saved recipes. To plan a new dish, `save_recipe`
first, then plan the returned id.

## Shopping list

- `add_recipe_to_shopping_list` adds every ingredient. When the user says
  they have some items already, use `get_recipe` and add only the rest with
  `add_to_shopping_list`.
- After planning a week, offer to add the ingredients in one go.
- `set_shopping_items_checked` and `remove_shopping_items` need item ids
  from `get_shopping_list`. Read the list first.
- `remove_shopping_items` deletes for the whole family. Confirm the items
  by name before you call it.

## Saving recipes

- One ingredient per line, with its amount ("400 g chickpeas").
- One step per entry, in order.
- Pass `sourceUrl` when the recipe came from a web page.
- Search first, so you do not save a recipe the user already has.

## Limits

Free Foodie accounts get 50 tool calls a day. If a call fails with a usage
limit, tell the user plainly and stop retrying.
