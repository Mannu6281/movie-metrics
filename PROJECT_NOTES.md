## Project-Overview
- Project name: Movie metrics
- Tech stack: React, Vite, Tailwind CSS, Appwrite, TMDB API
- Purpose : Search Movies, Show trending movies based on user searches

## High-Level Flow
1. User opens the app
2. App fetches trending movies from Appwrite database
3. User searches for a movie
4. App calls TMDB API with search query
5. Search term is stored/updated in Appwrite
6. UI updates with search results

## Frontend Flow

- main.jsx initializes react

- searchTerm → updated on every keystroke
- debouncedSearchTerm → updated only after user stops typing
- movieList → movies fetched from TMDB
- trendingMovies → fetched from Appwrite
- isLoading → controls spinner UI
- errorMessage → error handling

- useEffect(()=>{
     fetchMovies(debouncedSearchTerm)
  }, [debouncedSearchTerm])

  useEffect(()=>{
    loadTrendingMovies()
  },[])

  - fetchMovies and LoadTrendingMovies functions run when the App.jsx is first rendered and fetchMovies run whenever debouncedSearchTerm is changed, which changes only when
   useDebounce(()=>{setDebouncedSearchTerm(searchTerm)},500,[searchTerm])
   searchTerm stops changing for .5 seconds(Prevents API calls on every keystroke)

- const endPoint=query?`${API_BASE_URL}/search/movie?query=${encodeURIComponent(query)}`:`${API_BASE_URL}/discover/movie?sort_by=popularity.desc`

      const response = await fetch(endPoint,API_OPTIONS)
      
      if(!response.ok){
        throw new Error('Failed to fetch movies')
        
      }
      const data=await response.json()

      setMovieList(data.results||[])

      if(query&&data.results.length>0){
        await updateSearchCount(query,data.results[0]) 
      }
    - Uses TMDB Search API when user searches
    - Uses Discover API for default movies
    - After successful search → updates Appwrite metrics
    - Loading state handled properly

- Search.jsx: <input type="text" placeholder='Search through thousands of movies' 
            value={searchTerm}
            onChange={(event)=>{setSearchTerm(event.target.value)}}/>

            this method is used to set searchTerm first then display it in the input box, as the setSearchTerm function is passed by reference and only it can change searchTerm permanently hence it is used first, also after it is changed react re-renders the app and then the new searchTerm is displayed in the input, which ensures that the UI and the data are perfectly in sync

- MovieCard.jsx : pure presentational component

- Spinner.jsx : Rendered when isLoading === true, Improves UX during async operations

## Backend Flow
- updateSearchCount Logic:
   - Checks if search term already exists
   - If yes → increments count
   - If no → creates new document
   - Tracks popularity based on searches

- getTrendingMovies:
   - Returns top 5 most searched movies
   - Sorted by search count (descending)

## APIs Used
- TMDB API

   - Base URL: https://api.themoviedb.org/3
   - Authentication: Bearer Token
   - Endpoints:
      - /search/movie
      - /discover/movie
   - Used for:
      - Fetching movies
      - Search results
      - Movie metadata

- Appwrite Database API (document here means rows)
   - listDocuments
   - createDocument
   - updateDocument
   - Used to track and fetch trending search data

## Deployment Flow
- Frontend (Vercel)
   - Code pushed to GitHub
   - Vercel builds app using: npm run build
   - Output directory: dist
   - Environment variables injected at build time
   - Auto redeploy on every git push

- Backend (Appwrite Cloud)
   - Database and collection(table) created
   - Permissions set to allow frontend access
   - Production domain added to Appwrite Platforms
   - API accessed directly from frontend