# Shopping List App

## Goal
Make compiling a weekly shopping list quick and easy, with a clean aesthetic.

## Architecture
Single-file vanilla JS app (`shopping_list_app.html`) — no frameworks, no build tools, no dependencies. Just open in a browser.

- **State**: Single global `state` object. Every user action mutates `state`, calls `save()` (localStorage), then `render()` which rebuilds the entire DOM from `state`.
- **Persistence**: localStorage keys prefixed `shoplist8_`. Settings stored separately from data.
- **Rendering**: The `render()` function (~line 859) builds an HTML string based on `state.tab` and sets `innerHTML` on `#root`.

## File structure
- `shopping_list_app.html` — the entire app (CSS ~lines 1-171, HTML/constants ~173-300, JS ~302-1172)
- `how-to.html` — user-facing documentation page

## Key data models

**Item**: `{ id, name, cat, inStock, onList, checked, staple }`
- `cat`: "Cupboard" | "Fridge" | "Freezer"
- Status colors: Brown = in stock, Blue = on list, Yellow = to buy

**Recipe**: `{ id, name, itemIds, open }`
- `itemIds` references item IDs; pie charts show stock status of ingredients

**Meal plan**: `{ Monday: [], Tuesday: [], ... }` — arrays of recipe IDs

## Tabs
1. **Shopping List** — add/check/clear items for the current shop
2. **Staples** — recurring items grouped by category
3. **Meal Plan** — drag recipes into a 7-day grid, bulk-add ingredients to list
4. **Recipes** — create/edit recipes with ingredient lists and status pie charts
5. **Settings** — theme, tab visibility, import/export JSON backup

## Code conventions
- No build step; edit the HTML file directly
- All functions are top-level (no modules/classes)
- SVG generated inline for pie charts and status circles
- Touch drag-and-drop is custom-implemented (~line 1072) for mobile meal plan support
- `DEFAULT_ITEMS` (~100 items, line 180) and `DEFAULT_RECIPES` (line 283) seed first-run state
- ID counters (`nextItemId`, `nextRecipeId`) are in state and increment on creation

## Common tasks
- **Add a new default item**: Add to `DEFAULT_ITEMS` array (~line 180)
- **Add a new tab**: Add to render switch, update `TABS` usage in settings
- **Change styling**: Edit CSS variables at top of file (~line 5) or component styles
- **Modify state shape**: Update `state` object (~line 176), `save()`/`load()`, and `render()`
- **Test locally**: Open `shopping_list_app.html` in a browser — no server needed
