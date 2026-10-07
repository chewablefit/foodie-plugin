---
name: foodie
description: Use the user's Chewable Foodie recipes, family meal plan and shared shopping list. Use when the user asks what to cook, wants to plan meals for a day or week, asks about or changes their shopping or grocery list, wants to save, import, change or delete a recipe (including from a link, Instagram, TikTok or YouTube), asks what they cooked recently, asks what they can make with what they have, or wants to cook a recipe step by step.
---

# Chewable Foodie

Foodie is a family recipe app. The meal plan and the shopping list are shared
by everyone in the user's family, and every change shows up in their app at
once. Treat writes as visible to other people.

## Finding recipes

- Start with `search_recipes`. It returns summaries as data and shows
  nothing. Search once, with a broad query in the singular (`lentil`, not
  `lentils` and then `lentil`), and search again only if it found nothing.
  Call `get_recipe` before you quote ingredients or steps; never guess them.
- When the user asks to find, browse or choose something to cook, call
  `show_recipes` once with the ids of the recipes you found (or the best few)
  before you reply. It shows them as cards. Skip it when nothing was found or
  the user wants text only, and do not call it again for the same recipes.
- An empty query lists the most recently saved recipes. Use it for "what
  have I saved lately" or when the user has no dish in mind.
- Suggest recipes the user already has before inventing new ones. When the
  family has no match, search_recipes returns recipes from Foodie's public
  catalogue (`fromCatalogue: true`). They can be planned and shopped like the
  family's own; say they come from the catalogue.
- The recipe cards, the recipe, the shopping list and the meal plan show up
  as a widget in the chat. Do not repeat its contents; add only what the user
  needs on top. Every view you open takes its own pane, so read a recipe, the
  shopping list and the meal plan once per question: a list or plan already
  on screen keeps itself current.

## Before suggesting or planning

- `get_food_preferences` gives the user's diet and cooking goals. Respect them.
  It does not include allergies: ask the user if it matters.
- `get_cooking_history` shows what the family cooked lately. Avoid repeating
  last week's dinners unless the user asks for them.
- When the user says they cooked something, offer `mark_cooked`, with a
  rating (1-5) if they give one.

## What can I make?

When the user lists what they have ("eggs, spinach and feta"), call
`find_recipes_by_ingredients` with one ingredient per entry. It shows its own
view with what is missing for each recipe, so do not follow it with
`show_recipes`. Offer to add the missing items with `add_to_shopping_list`;
the widget has a button for it too.

## Cooking

- In the widget, "Start cooking" opens cook mode next to the chat: one step at
  a time, with a timer where a step names a time, and a rating at the end.
  Stay available for questions like "can I use butter instead?".
- Hands-free or by voice, use `get_cooking_step` one step at a time. Read the
  step in a sentence or two and offer the timer (`timerMinutes`).

## Changing recipes

`edit_recipe`, `delete_recipe` and `set_recipe_image` only work on the
family's own recipes, never on catalogue ones or ones published in the
catalogue. Everyone in the family sees the change.

- `edit_recipe` changes only the fields you give it. Ingredients and
  instructions replace the whole list: read the recipe with `get_recipe`
  first and send the complete new list.
- `delete_recipe` cannot be undone. Say which recipe, by name, and that its
  cooking history and ratings go with it, and wait for a yes. It also comes
  off the meal plan, the collections and the shopping list.
- `set_recipe_image` replaces the photo, from a link (`imageUrl`) or from the
  picture's bytes (`imageBase64`, up to 5 MB) if you can read the user's
  attachment. Never invent a link.

## Weekly plan

If the user wants a plan every week, offer to set up a scheduled task: every
Sunday at 17:00, plan next week's dinners from their recipes, following
their preferences and avoiding the last two weeks, and add what is missing
to the shopping list once they say yes.

## Planning meals

1. `get_meal_plan` for the week first, so you know what is already planned.
2. Propose the plan in chat and wait for a yes.
3. `plan_meal` once per day and meal. It replaces what is already planned
   for that slot, so say so when a slot is taken.

`plan_meal` only takes saved recipes. To plan a new dish, `save_recipe`
first, then plan the returned id.

## Shopping list

- When the user asks to add a Foodie recipe to the shopping list, use
  `add_recipe_to_shopping_list` with its `recipeId`. By default it adds ONE
  entry linked to the recipe, with its name and servings. This also works for
  recipes from the public catalogue. Omit `expandIngredients`, or pass
  `expandIngredients: false`, for a whole recipe as one entry.
- Pass `expandIngredients: true` only when the user asks for separate
  ingredient items. When they already have some ingredients, use `get_recipe`
  and add only the missing ones with `add_to_shopping_list`.
- `add_to_shopping_list` is for groceries or selected ingredients. Never use
  it to create a plain item named after a Foodie recipe: that loses the recipe
  link. If adding the linked recipe fails, report the failure instead of
  silently substituting an unlinked item.
- After planning a week, offer to add the recipes as linked shopping entries.
  Expand their ingredients only if the user asks for that.
- Items already on the list with the same amount are skipped and listed in
  `alreadyOnList`. Mention them instead of adding them twice.
- `set_shopping_items_checked` and `remove_shopping_items` need item ids
  from `get_shopping_list`. Read the list first.
- `remove_shopping_items` deletes for the whole family. Confirm the items
  by name before you call it.

## Importing from a link

1. `read_recipe_page` with the link. Foodie fetches the page; you read it.
2. `source: "recipe-markup"`: name, ingredients and steps are filled in. Use
   them as they are.
3. Otherwise read the recipe from `text` (a caption, or the page's text).
   Write each ingredient with its amount. If there is no recipe in the text,
   say so; never invent one.
4. `save_recipe` with `sourceUrl`, `imageUrl` and `author` from the result.

## Saving recipes

- One ingredient per line, with its amount ("400 g chickpeas").
- One step per entry, in order.
- Pass `sourceUrl` when the recipe came from a web page.
- Search first, so you do not save a recipe the user already has.
- `alreadySaved: true` means the same name was saved moments ago (a retry).
  Tell the user it is saved; do not save again.

## Limits

Free Foodie accounts get 50 tool calls a day. If a call fails with a usage
limit, tell the user plainly and stop retrying.
