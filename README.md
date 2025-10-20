# alx-project-0x14

## API overview

Collection of information for movies, tv-shows, actors. Includes youtube trailer url, awards, full biography, and many other usefull informations. This api provides complete and updated data for over 9 million titles ( movies, series and episodes) and 11 million actors / crew and cast members.

## Version

v1

## Available Endpoints

### **Titles**

- `GET /titles/series/{seriesId}` — Get all titles in a specific series.  
- `GET /titles/x/upcoming` — Retrieve upcoming movie and show releases.  
- `GET /titles/{id}/ratings` — Fetch rating details for a specific title.  
- `GET /titles/series/{seriesId}/{season}` — Get all episodes for a specific season of a series.  
- `GET /titles/episode/{id}` — Retrieve details about a specific episode.  
- `GET /titles/x/titles-by-ids` — Fetch multiple titles by a list of IDs.  
- `GET /titles/{id}/aka` — Get alternate names or aliases for a title.  
- `GET /titles/random` — Retrieve a random title from the database.  
- `GET /titles/{id}` — Fetch detailed information for a single title.  
- `GET /titles` — Get a list of all available titles.  
- `GET /titles/seasons/{seriesId}` — Retrieve all seasons for a given series.

---

### **Search**

- `GET` — Search by IMDb ID.  
- `GET /titles/search/akas/{aka}` — Search titles by alternate name.  
- `GET /titles/search/keyword/{keyword}` — Search titles by keyword or tag.  
- `GET /titles/search/title/{title}` — Search titles by their official name.

---

### **Actors**

- `GET /actors/random` — Retrieve a random actor profile.  
- `GET /actors/{id}` — Get detailed information about a specific actor.  
- `GET /actors` — Fetch a list of all available actors.

---

### **Utils**

- `GET /titles/utils/genres` — Get a list of all available genres.  
- `GET /titles/utils/lists` — Retrieve predefined title lists (e.g., popular, trending).  
- `GET /titles/utils/titleTypes` — Get supported title types (movie, series, episode, etc.).

---

### **Obsolete**

- `GET /titles/{id}/crew` — (Deprecated) Retrieve crew details for a title.  
- `GET /titles/{id}/main_actors` — (Deprecated) Get main actors for a title.

## Request and Response Format

A typical interaction with the Movies Database API involves sending a structured request and receiving a JSON object as a response.

### Request Structure

An API request is typically an HTTP GET request to a specific endpoint, often including required parameters (such as the API key) and optional parameters (for filtering, sorting, or pagination).

**URL Structure:**

```
https://moviesdatabase.p.rapidapi.com/{endpoint}?{parameter1}={value1}&{parameter2}={value2}
```

**Example Request:**

To get a list of top-rated movies, you might use the `/titles/top_rated` endpoint.

```
GET https://moviesdatabase.p.rapidapi.com/titles/top_rated?list=top_rated_250&limit=10&endYear=2022
```

**Required Headers:**

All requests require specific headers for authentication and identification:

| Header Name | Value (Example) | Description |
| :--- | :--- | :--- |
| `X-RapidAPI-Key` | `YOUR_RAPIDAPI_KEY` | Your unique API key for authentication. |
| `X-RapidAPI-Host` | `moviesdatabase.p.rapidapi.com` | The host URL for the API. |

### Response Object Structure

The API returns a JSON (JavaScript Object Notation) object as the response. A typical successful response will contain a `data` array (or object) with the requested resources, along with metadata like `metadata` or `results`.

**Example Successful Response (Listing Titles):**

A response from the `/titles/top_rated` endpoint will contain an array of title objects under the `results` key, and an array of `next` and `previous` links for pagination, as shown in the metadata.

```json
{
  "results": [
    {
      "_id": "63f7336d36e05d28b12f6f43",
      "id": "tt0111161",
      "primaryImage": {
        "id": "nm0001053",
        "width": 1000,
        "height": 1424,
        "url": "https://m.media-amazon.com/images/M/MV5BNjNhN2NlMGM4N…E0NTkyNWMzXkEyXkFqcGdeQXVyMTA3M…._V1_.jpg",
        "caption": {
          "plainText": "The Shawshank Redemption (1994)",
          "__typename": "Markdown"
        },
        "__typename": "Image"
      },
      "titleType": {
        "text": "Movie",
        "id": "movie",
        "isSeries": false,
        "isEpisode": false,
        "__typename": "TitleType"
      },
      "titleText": {
        "text": "The Shawshank Redemption",
        "__typename": "TitleText"
      },
      "releaseDate": {
        "day": 14,
        "month": 10,
        "year": 1994,
        "__typename": "ReleaseDate"
      },
      "__typename": "Title"
    }
    // ... more title objects
  ],
  "metadata": {
    "operation": "get-titles",
    "requestId": "239b9b00-54a7-47b2-841f-178b8a7b000b",
    "serverTime": "2023-10-27T14:30:00.000Z",
    "queryTime": 0.041,
    "next": "/titles/top_rated?list=top_rated_250&limit=10&page=2&endYear=2022",
    "previous": null
  }
}
```

**Example Error Response:**

If an error occurs (e.g., invalid parameters, missing API key), the response will include an `error` message detailing the problem and an HTTP status code indicating the error type (e.g., 401 for Unauthorized, 404 for Not Found).

```json
{
  "message": "You are not authorized to access this resource. Missing X-RapidAPI-Key header. Check authentication settings.",
  "error": "Unauthorized"
}
```

## Authentication

All requests to the Movies Database API are authenticated using a required API key, which must be passed in the HTTP request headers.

### Required Headers for Authentication

You need to include the following two specific headers in every API request:

1.  **`X-RapidAPI-Key`**: This is your personal key provided by the RapidAPI platform. It grants you access to the API and tracks your usage.
2.  **`X-RapidAPI-Host`**: This specifies the host URL for the API, ensuring the request is routed correctly.

| Header Name | Value (Example) | Purpose |
| :--- | :--- | :--- |
| `X-RapidAPI-Key` | `YOUR_RAPIDAPI_KEY_HERE` | Your unique key for authentication. |
| `X-RapidAPI-Host` | `moviesdatabase.p.rapidapi.com` | The designated host for the API. |

### Example Request with Authentication Headers

Here is an example of an authenticated `GET` request using cURL:

```bash
curl --request GET \
    --url 'https://moviesdatabase.p.rapidapi.com/titles/tt0111161' \
    --header 'X-RapidAPI-Key: YOUR_RAPIDAPI_KEY_HERE' \
    --header 'X-RapidAPI-Host: moviesdatabase.p.rapidapi.com'
```

**Note:** If the `X-RapidAPI-Key` header is missing or invalid, the API will return an HTTP 401 (Unauthorized) error.

## Error Handling

When interacting with the Movies Database API, you must be prepared to handle various HTTP status codes that indicate a problem. A successful request typically returns a status code in the $200$ series (e.g., $200$ OK). Any other status code signifies an error.

Common error responses are returned as a JSON object containing an explanatory `message` and sometimes a brief `error` description.

### Common Error Status Codes

| Status Code | Error Type | Description | Handling Strategy |
| :--- | :--- | :--- | :--- |
| **$400$ Bad Request** | Invalid Input | The request could not be understood or processed due to malformed syntax or invalid parameters (e.g., passing a string where an integer is expected). | Check the request URL, parameters, and body for correctness based on API documentation. |
| **$401$ Unauthorized** | Authentication Failed | The API key is missing or invalid, or the host header is incorrect. This is a common error for unauthenticated requests. | Verify that the `X-RapidAPI-Key` and `X-RapidAPI-Host` headers are present and correct. |
| **$403$ Forbidden** | Access Denied | The key is valid, but the user is forbidden from accessing the specific resource, often due to exceeding subscription limits or attempting to access a premium feature not included in the plan. | Check your subscription usage on the RapidAPI dashboard. Consider upgrading your plan if limits are exceeded. |
| **$404$ Not Found** | Resource Not Found | The requested endpoint or resource (e.g., a specific title ID) does not exist. | Double-check the path of the request URL and the specific ID/identifier used in the query. |
| **$429$ Too Many Requests** | Rate Limit Exceeded | The user has sent too many requests in a given amount of time, exceeding the platform's rate limits. | Implement a **retry mechanism** with an exponential backoff. Wait before sending the next request. |
| **$500$ Internal Server Error** | API Server Issue | A generic error indicating a problem on the API server's side. | This typically requires no change to your code. If the problem persists, wait and retry later, or contact API support. |

### Example Error Handling in Code (Conceptual)

In most programming languages, you should check the HTTP status code of the response before attempting to parse the JSON content.

```pseudocode
function handleAPIResponse(response):
    statusCode = response.getStatusCode()

    if statusCode == 200:
        // Success: Process the 'results' data
        data = parseJSON(response.body)
        processMovieData(data)
    else if statusCode == 401:
        // Handle Unauthorized error
        logError("Authentication Failed: Check API key and host headers.")
        displayErrorMessage("Please check your API configuration.")
    else if statusCode == 404:
        // Handle Not Found error
        logError("Resource Not Found: The movie ID or endpoint is incorrect.")
        displayErrorMessage("The requested movie could not be found.")
    else if statusCode == 429:
        // Handle Rate Limit Exceeded
        logWarning("Rate limit exceeded. Waiting before retrying...")
        wait(5000) // Wait 5 seconds
        retryRequest()
    else:
        // Handle other client/server errors
        errorBody = parseJSON(response.body)
        logError("API Error " + statusCode + ": " + errorBody.message)
        displayErrorMessage("An unexpected error occurred. Please try again.")
```

## Usage Limits and Best Practices

To ensure reliable service and a fair usage environment for all developers, the Movies Database API, like most services hosted on RapidAPI, imposes usage restrictions.

### Usage Limitations (Rate Limits)

The primary limitation is the **Rate Limit**, which restricts the number of requests you can make within a specific time window. Exceeding these limits will result in an HTTP **$429$ Too Many Requests** error.

* **Plan-Specific Limits:** Rate limits are tied to your chosen subscription plan (e.g., Basic, Pro, Ultra) on the RapidAPI platform. These limits are usually defined as a total number of requests per month (hard quota) and a maximum number of requests per second/minute (rate limit).
* **Response Headers:** Successful responses often include headers (e.g., `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`) that allow you to track your consumption and know exactly how many requests you have left and when the counter will reset.

### Best Practices for Effective API Use

Adhering to these best practices will help you avoid rate limiting, reduce latency, and ensure your application runs efficiently.

#### 1. Implement Caching

* **Cache Static Data:** Data that doesn't change frequently (like a movie's release date, plot summary, or fixed cast list) should be cached on your server or client application. Avoid making repeat API calls for the same data within a short period.
* **Use Stale-While-Revalidate:** A common caching strategy is to serve cached data immediately while an asynchronous request is made to the API to update the data for the *next* time.

#### 2. Optimize Request Size and Frequency

* **Use Specific Endpoints:** When possible, use specific endpoints like `/titles/{id}` to fetch only the required information for a single title rather than broad search or list endpoints that return more data than needed.
* **Utilize Query Parameters:** The API often provides `info` or similar query parameters that allow you to specify exactly which fields you want in the response. Requesting only the necessary data reduces payload size and improves response time.

#### 3. Handle Rate Limits Gracefully

* **Monitor Response Headers:** Use the rate-limit headers in the successful response to dynamically adjust the speed of your requests.
* **Implement Backoff:** When you receive a **$429$ Too Many Requests** error, do not immediately retry the request. Implement an **exponential backoff** strategy, where you wait for a progressively longer period (e.g., $1$ second, then $2$ seconds, then $4$ seconds) before retrying the call. This is crucial for avoiding a persistent ban and preventing a load spike on the API server.

#### 4. Secure Your Key

* **Server-Side Access Only:** **Never expose your `X-RapidAPI-Key` in client-side code** (HTML, JavaScript, mobile app code). All API calls should be routed through your own secure backend server to keep the key hidden and protect your account from unauthorized use.

This tutorial gives a step-by-step guide to making API calls using a popular movie database API.

