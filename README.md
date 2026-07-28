Recipe Book is a responsive web app that lets users search for recipes and view detailed cooking instructions, powered by TheMealDB API.

  Features:
1- Search recipes by name using a simple search bar (supports both button click and Enter key)
2- Browse results in a clean, responsive grid of recipe cards with images and categories
3- View full details for any recipe — including ingredients with exact measurements, step-by-step instructions, and a direct link to a YouTube tutorial (when available)
4- Seamless navigation between the search results and recipe details using a single-page toggle (no page reloads)
5- Error handling for empty searches, no results found, and failed API requests
6- Fully responsive design that adapts to mobile and smaller screens

  Tech Stack:
1- HTML5 for structure
2- CSS3 with custom properties (CSS variables) for consistent, themeable styling
4- Vanilla JavaScript (no frameworks) using the Fetch API for asynchronous data handling
5- Font Awesome for icons
6- TheMealDB API as the data source

  How It Works:
Users type a dish name into the search bar, which queries the API and dynamically renders matching recipes as cards.
Clicking a card fetches the full recipe details and displays them in a dedicated view — including a formatted ingredients list and instructions — 
with a "Back" button to return to the search results.  

  Project Structure:
├── index.html   # Page structure
├── style.css    # Styling and responsive layout
└── script.js    # API calls, search logic, and UI interactions
