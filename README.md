# 🍽️ Recipe Book

A lightweight, client-side recipe search app built with vanilla HTML, CSS, and JavaScript. It uses [TheMealDB API](https://www.themealdb.com/api.php) to search for recipes by name and view full recipe details, including ingredients, instructions, and a linked video tutorial.

## Features

- 🔍 Search recipes by name (button click or `Enter` key)
- 🖼️ Responsive grid of recipe result cards with image, title, and category
- 📖 Detailed recipe view with:
  - Full ingredient list with measurements
  - Step-by-step instructions
  - Direct link to the YouTube tutorial (when available)
- ⚠️ User-friendly error and empty-state handling
- 📱 Responsive layout for mobile and desktop
- 🎨 Themeable design via CSS custom properties

## Tech Stack

| Layer      | Technology |
|------------|------------|
| Markup     | HTML5 |
| Styling    | CSS3 (custom properties, Flexbox, CSS Grid) |
| Logic      | Vanilla JavaScript (ES6+, `fetch`, `async/await`) |
| Icons      | [Font Awesome 7.3.0](https://fontawesome.com/) (via CDN) |
| Data       | [TheMealDB API](https://www.themealdb.com/api.php) (free tier, test API key `1`) |

No build tools, frameworks, or dependencies to install — it's a static site.

## Project Structure

```
.
├── index.html      # App markup and layout
├── style.css       # Styling, theming, and responsive rules
├── script.js       # Search logic, API calls, and DOM rendering
└── README.md
```

## Getting Started

### Prerequisites

- A modern web browser
- An internet connection (required for the CDN icon library and the TheMealDB API)

### Run Locally

Since the app makes `fetch` requests, it's best served over HTTP rather than opened directly as a `file://` URL (to avoid CORS/security restrictions in some browsers).

**Option 1: VS Code Live Server**
Open the folder in VS Code and launch it with the Live Server extension.

**Option 2: Python's built-in server**
```bash
# From the project directory
python3 -m http.server 8000
```
Then visit `http://localhost:8000`.

**Option 3: Node's `http-server`**
```bash
npx http-server .
```

No environment variables, API keys, or build steps are required.

## How It Works

### Search Flow (`script.js`)

1. The user types a search term and clicks **Search** (or presses `Enter`).
2. `searchMeals()` sends a `GET` request to:
   ```
   https://www.themealdb.com/api/json/v1/1/search.php?s={searchTerm}
   ```
3. If no meals are returned, an error message is shown in `#error-container`.
4. If meals are found, `displayMeals()` renders each result as a `.meal` card inside `#meals`, showing the recipe's thumbnail, title, and category.

### Recipe Detail Flow

1. Clicking a recipe card triggers `handleMealClick()` via event delegation on the `#meals` container.
2. The app fetches full recipe data from:
   ```
   https://www.themealdb.com/api/json/v1/1/lookup.php?i={mealId}
   ```
3. Ingredients and measurements are extracted by looping through the API's `strIngredient1`–`strIngredient20` / `strMeasure1`–`strMeasure20` fields, skipping empty entries.
4. The `#meal-details` section is populated and revealed, and the page scrolls smoothly into view.
5. The **Back to recipes** button hides the detail view and returns to the search results.

## API Reference

This project uses the [TheMealDB](https://www.themealdb.com/api.php) free test API (key `1`, rate-limited, intended for development use). Endpoints used:

| Purpose         | Endpoint                                      |
|------------------|------------------------------------------------|
| Search by name   | `GET /search.php?s={query}`                    |
| Lookup by ID     | `GET /lookup.php?i={id}`                       |

For production use, consider [registering for a paid API key](https://www.themealdb.com/api.php) to avoid rate limits.

## Customization

Colors, spacing, and other design tokens are centralized as CSS custom properties in `style.css`:

```css
:root {
  --primary: #ff7e5f;
  --primary-dark: #eb5e41;
  --primary-light: #ffb199;
  --secondary: #0ba360;
  --text-dark: #333333;
  --text-light: #f8f9fa;
  --background: #ffffff;
  --background-light: #f8f9fa;
  --border-radius: 8px;
  --shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
```
Update these values to re-theme the entire app.

## Known Limitations / Possible Improvements

- No loading spinner during fetch requests (only text status updates)
- No debouncing on search input for live/type-ahead search
- No pagination or "load more" for large result sets
- No client-side caching of previously viewed recipes
- Minor bug: ingredient filtering checks `.trim !== ""` (a function reference) instead of `.trim() !== ""`, so ingredients with only whitespace are not filtered out
- No unit or integration tests

## License

No license specified. Recipe data is provided by [TheMealDB](https://www.themealdb.com/api.php) under their own terms of use.
