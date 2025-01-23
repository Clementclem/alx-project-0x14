# MoviesDatabase API Documentation Overview

## API Overview
The MoviesDatabase API is a comprehensive platform that allows users to retrieve information about movies, TV shows, actors, and related media. It offers rich metadata, including titles, genres, release dates, ratings, cast details, and more. The API supports search functionality, trending media, and detailed information about specific items, making it ideal for developers building entertainment-focused applications.

## Version
The current version of the API is v1.0, as stated in the API documentation.

## Available Endpoints
- **/search**: Retrieve a list of movies, TV shows, or people matching a query string.
- **/movie/{id}**: Get detailed information about a specific movie by its unique ID.
- **/tv/{id}**: Fetch detailed information about a TV show by its unique ID.
- **/person/{id}**: Retrieve details about a specific actor or crew member by their unique ID.
- **/trending**: List trending movies or TV shows based on user activity.
- **/genres**: Fetch a list of available genres for movies and TV shows.
- **/discover**: Get a curated list of movies or TV shows based on filters like genre, release year, and more.

## Request and Response Format
### Request Format
All requests to the API must be made over HTTPS and include a valid API key for authentication. The base URL for requests is:
```
https://api.moviesdatabase.com/v1
```

Example GET Request:
```
GET https://api.moviesdatabase.com/v1/movie/12345
Headers:
  Authorization: Bearer <API_KEY>
```

### Response Format
Responses are returned in JSON format. Below is an example of a typical response for a movie:
```json
{
  "id": 12345,
  "title": "Inception",
  "release_date": "2010-07-16",
  "genres": [
    { "id": 1, "name": "Action" },
    { "id": 2, "name": "Sci-Fi" }
  ],
  "overview": "A thief who steals corporate secrets through the use of dream-sharing technology is given the inverse task of planting an idea into the mind of a C.E.O.",
  "rating": 8.8,
  "cast": [
    { "id": 100, "name": "Leonardo DiCaprio", "character": "Cobb" },
    { "id": 101, "name": "Joseph Gordon-Levitt", "character": "Arthur" }
  ]
}
```

## Authentication
To authenticate requests, you need to provide an API key. The API key can be obtained by signing up on the MoviesDatabase developer portal.

### Authentication Methods
1. **Query Parameter**: Add the API key as a query parameter:
   ```
   GET https://api.moviesdatabase.com/v1/movie/12345?api_key=YOUR_API_KEY
   ```

2. **Authorization Header**: Include the API key in the headers:
   ```
   Authorization: Bearer YOUR_API_KEY
   ```

## Error Handling
### Common Error Responses
- **401 Unauthorized**: Invalid or missing API key.
  ```json
  {
    "status_code": 401,
    "status_message": "Invalid API key."
  }
  ```

- **404 Not Found**: Resource does not exist.
  ```json
  {
    "status_code": 404,
    "status_message": "Resource not found."
  }
  ```

- **429 Too Many Requests**: Exceeded rate limits.
  ```json
  {
    "status_code": 429,
    "status_message": "You have exceeded the allowed rate limit."
  }
  ```

- **500 Internal Server Error**: Server encountered an unexpected condition.
  ```json
  {
    "status_code": 500,
    "status_message": "An error occurred. Please try again later."
  }
  ```

### Handling Errors in Code
- Check the status code of each response.
- Retry failed requests with exponential backoff for 500-level errors.
- Log errors for debugging purposes.

## Usage Limits and Best Practices
### Usage Limits
- The API has a rate limit of 100 requests per minute. Exceeding this limit will result in a 429 error.
- Some endpoints may have additional limitations based on data sensitivity.

### Best Practices
- Cache frequently accessed data to reduce API calls and improve performance.
- Use appropriate filters and pagination to minimize data retrieval.
- Secure your API key by storing it in environment variables or secure vaults.
- Respect the rate limits to avoid being temporarily blocked.
- Regularly review the API documentation for updates and changes.
