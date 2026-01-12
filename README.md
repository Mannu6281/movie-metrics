# Movie Metrics 🎬

Movie Metrics is a frontend web application that allows users to search for movies, explore popular titles, and view trending movies based on user interest.

It integrates the TMDB API for movie data and uses Appwrite to track and rank trending searches.

---

## Features

- Search movies in real time using the TMDB API
- Debounced search to minimize unnecessary API calls
- Display trending movies based on search frequency
- Responsive and clean UI
- Environment-based configuration for API keys
- Deployed as a production-ready frontend application

---

## Tech Stack

- React.js
- Vite
- Tailwind CSS
- TMDB API
- Appwrite (Databases)
- Native Fetch API

---

## Project Structure

``` movie-metrics/
├── public/
├── src/
│ ├── assets/
│ ├── components/
│ │ ├── MovieCard.jsx
│ │ ├── Search.jsx
│ │ └── Spinner.jsx
│ ├── appwrite.js
│ ├── App.jsx
│ ├── main.jsx
│ └── index.css
├── README.md
└── PROJECT_NOTES.md
```


---

## How It Works

### Movie Search
- Movies are fetched from the TMDB API using the native `fetch` API
- Search input is debounced using `react-use` to reduce API calls
- Popular movies are fetched when no search query is provided

### Trending Movies
- Each successful search updates a counter in Appwrite
- Searches are ranked based on frequency
- Top searched movies are displayed in the Trending Movies section

---

## Environment Variables

VITE_TMDB_API_KEY=your_tmdb_bearer_token

VITE_APPWRITE_PROJECT_ID=your_appwrite_project_id

VITE_APPWRITE_DATABASE_ID=your_database_id

VITE_APPWRITE_COLLECTION_ID=your_collection_id



---

## What This Project Demonstrates

- Integrating third-party APIs in a frontend application
- Optimizing API usage with debouncing
- Using Appwrite as a backend-as-a-service
- Tracking and ranking user interactions
- Managing environment variables in a Vite project
- Building and deploying modern React applications

---

## Future Improvements

- Movie detail pages
- Genre-based filtering
- Watchlist or favorites feature
- Improved error handling and loading states

---

## Author

**Mannu Nandan Jha**  
GitHub: https://github.com/Mannu6281  
LinkedIn: https://www.linkedin.com/in/mannu-nandan-jha-a05567317




