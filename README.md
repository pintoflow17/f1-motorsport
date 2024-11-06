# F1 Motorsport Data

## Introduction

**F1 Motorsport Data API** provides comprehensive access to real-time and historical data from the world of Formula 1 racing. Perfect for developers and motorsport enthusiasts, this API allows for seamless integration of race statistics, driver information, team data, and more into your applications.

### Key Features

- **Live Race Data**: Access real-time updates during races, including lap times and positions.
- **Driver and Team Information**: Retrieve detailed statistics and profiles for drivers and teams, including standings and performance metrics.
- **Race Schedule**: Get information on upcoming races, including dates, locations, and formats.
- **Historical Data**: Access past race results and historical statistics for in-depth analysis.

## Authentication

The URL you need to use is the following: `https://f1-motorsport-data.p.rapidapi.com/`
The API requires the headers listed below:

- **`x-rapidapi-host`**: `f1-motorsport-data.p.rapidapi.com`
- **`x-rapidapi-key`**: `YOUR_API_KEY`

Make sure to replace `YOUR_API_KEY` with your API key. You can register one [here](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/f1-motorsport-data/pricing).
Some frameworks automatically add extra headers, you have to make sure to remove them in order to get a response from the API.

## Caching

- Cached data is stored using a unique key derived from the athlete ID.
- Data is cached for 1 hour (in seconds) to reduce API requests and improve performance.

## Endpoints

The API is configured to accept only **GET** requests. Below are the available endpoints with their descriptions and required parameters.

### 1. **`GET /athlete-info`**

- **Description**: Retrieves information about a specific athlete. The athlete ID can be obtained from other endpoints such as schedule, standings, or the ESPN website.

| Parameter   | Type   | Default | Description                            | Required |
|-------------|--------|---------|----------------------------------------|----------|
| `athleteId` | string | -       | The ID of the athlete                  | Yes      |

- **Conditional Request Headers**
  - `If-None-Match`: Allows conditional retrieval based on the provided entity tag.

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/athlete-info?athleteId=4665', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "id": "4665",
  "uid": "s:2000~a:4665",
  "guid": "a1329d3d-acd6-21b7-e7f6-7b226047f683",
  "alternateId": "4305544",
  "firstName": "Max",
  "middleName": "",
  "lastName": "Verstappen",
  "fullName": "Max Verstappen",
  "displayName": "Max Verstappen",
  "shortName": "M. Verstappen",
  "dateOfBirth": "1997-09-30T07:00Z",
  "link": "https://www.espn.com/racing/driver/_/id/4665/max-verstappen",
  "birthPlace": {
    "city": "Hasselt"
  },
  "slug": "max-verstappen",
  "headshot": "https://a.espncdn.com/i/headshots/f1/players/full/4665.png",
  "vehicles": [
    {
      "number": "1",
      "manufacturer": "Red Bull",
      "chassis": "RB16B",
      "engine": "Honda RA621H",
      "tire": "Pirelli",
      "team": "Red Bull"
    }
  ],
  "flag": {
    "href": "https://a.espncdn.com/i/teamlogos/countries/500/ned.png",
    ...
```

### 2. **`GET /race-results`**

- **Description**: Retrieves race results for a specific driver in a given year. It allows cross-origin requests by setting the appropriate headers. If the requested data is available in the cache, it serves the response from the cache to optimize performance. Otherwise, it fetches the data, caches it for future use, and returns it.

| Parameter  | Type   | Default | Description                            | Required |
|------------|--------|---------|----------------------------------------|----------|
| `driverId` | string | -       | The ID of the driver                   | Yes      |
| `year`     | string | `2024`  | The year of the race (YYYY)            | No       |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/race-results?driverId=4665', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
[
  {
    "date": "10/27",
    "race": "Mexico City Grand Prix",
    "place": 6,
    "start": 2,
    "laps": 71,
    "points": 8
  },
  {
    "date": "10/20",
    "race": "Pirelli United States Grand Prix",
    "place": 3,
    "start": 2,
    "laps": 56,
    "points": 23
  },
  {
    "date": "9/22",
    "race": "Singapore Airlines Singapore Grand Prix",
    "place": 2,
    "start": 2,
    "laps": 62,
    "points": 18
  },
  {
    "date": "9/15",
    "race": "Qatar Airways Azerbaijan Grand Prix",
    "place": 5,
    "start": 6,
    ...
```

### 3. **`GET /stats`**

- **Description**: Retrieves statistics for a specific Formula 1 driver. It enables cross-origin requests by setting the necessary headers. Cached data is utilized if available to optimize response time. Otherwise, it fetches the data from the source, caches it, and returns the response.

| Parameter  | Type   | Default | Description                            | Required |
|------------|--------|---------|----------------------------------------|----------|
| `driverId` | string | -       | The ID of the driver                   | Yes      |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/stats?driverId=4665', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
[
  {
    "year": 2015,
    "rank": 12,
    "starts": 19,
    "wins": 0,
    "poles": 0,
    "top5": 2,
    "top10": 10,
    "points": 49,
    "avgStart": "--",
    "avgFinish": "--"
  },
  {
    "year": 2016,
    "rank": 5,
    "starts": 21,
    "wins": 1,
    "poles": 0,
    "top5": 11,
    "top10": 17,
    "points": 204,
    "avgStart": "--",
    "avgFinish": "--"
  },
  {
    "year": 2017,
    "rank": 6,
    "starts": 20,
    "wins": 2,
    ...
```

### 4. **`GET /news`**

- **Description**: Retrieves current F1 News.

| Parameter | Type   | Default | Description                            | Required |
|-----------|--------|---------|----------------------------------------|----------|
| `limit`   | string | `25`    | Number of news entries to retrieve     | No       |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/news', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
[
  {
    "dataSourceIdentifier": "e8b065c34c038",
    "description": "Red Bull team boss Christian Horner refused to confirm Sergio Pérez would see out the Formula 1 season after the struggling Mexican suffered another miserable afternoon at his home race on Sunday.",
    "headline": "Sergio Pérez's Red Bull, F1 future in doubt beyond Brazil GP",
    "link": "https://www.espn.co.uk/f1/story/_/id/42056463/sergio-perez-red-bull-f1-future-doubt-brazil-gp",
    "images": [
      {
        "dataSourceIdentifier": "77e9f32100344",
        "name": "Sergio Perez F1 sad Mexico [1296x729]",
        "width": 1296,
        "alt": "Sergio Perez of Mexico and Oracle Red Bull Racing in the garage during the F1 Grand Prix of Mexico at Autodromo Hermanos Rodriguez on October 27, 2024 in Mexico City, Mexico.",
        "id": 42056531,
        "credit": "Song Haiyuan/MB Media/Getty Images",
        "type": "header",
        "url": "https://a.espncdn.com/photo/2024/1028/r1407206_1296x729_16-9.jpg",
        "height": 729
      }
    ]
  },
  {
    "dataSourceIdentifier": "7957b1e0e620a",
    "description": "Max Verstappen was awarded 20 seconds' worth of penalties in Mexico, but were they warranted? Laurence Edmondson dives into the rulebook for answers.",
    "headline": "Did F1 stewards get Verstappen decisions right in Mexico?",
    "link": "https://www.espn.com/racing/f1/story/_/id/42054206/did-f1-stewards-get-max-verstappen-lando-norris-sergio-perez-decisions-right-mexico-city",
    "images": [
      {
        "dataSourceIdentifier": "f3de295bde3f4",
        "name": "Max Verstappen and Lando Norris 241027 [1296x729]",
        "width": 1296,
        ...
```

### 5. **`GET /current-scoreboard`**

- **Description**: Retrieves current scoreboard.

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/current-scoreboard', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
  "sports": [
    {
      "id": "2000",
      "uid": "s:2000",
      "guid": "a5f9ac6b-82e3-3891-a17a-ea2d693b8331",
      "name": "Motor Sports",
      "slug": "racing",
      "logos": [
        {
          "href": "https://a.espncdn.com/combiner/i?img=/redesign/assets/img/icons/ESPN-icon-NASCAR.png",
          "alt": "",
          "rel": [
            "full",
            "default"
          ],
          "width": 500,
          "height": 500
        }
      ],
      "leagues": [
        {
          "id": "2030",
          "uid": "s:2000~l:2030",
          "name": "Formula One",
          "abbreviation": "F1",
          "shortName": "F1",
          "slug": "f1",
          "tag": "f1",
          "isTournament": false,
          ...
```

### 6. **`GET /scoreboard`**

- **Description**: Retrieves scoreboards from a variaty of events on a specific date.

| Parameter | Type   | Default | Description                             | Required |
|-----------|--------|---------|-----------------------------------------|----------|
| `year`    | string | -       | The year of the scoreboard (YYYY)       | Yes      |
| `month`   | string | -       | The month of the scoreboard (MM)        | No       |
| `day`     | string | -       | The day of the scoreboard (DD)          | No       |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/scoreboard?year=2024', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "scoreboard": [
    {
      "id": "600041133",
      "uid": "s:2000~l:2030~e:600041133",
      "date": "2024-02-29T11:30Z",
      "endDate": "2024-03-02T15:00Z",
      "name": "Gulf Air Bahrain Grand Prix",
      "shortName": "Gulf Air Bahrain GP",
      "season": {
        "year": 2024,
        "type": 2,
        "slug": "regular-season"
      },
      "competitions": [
        {
          "id": "401622102",
          "uid": "s:2000~l:2030~e:600041133~c:401622102",
          "date": "2024-02-29T11:30Z",
          "type": {
            "id": "1",
            "abbreviation": "FP1"
          },
          "timeValid": true,
          "recent": false,
          "competitors": [
            {
              "id": "4510",
              "uid": "s:2000~a:4510",
              "type": "athlete",
              ...
```

### 7. **`GET /race-report`**

- **Description**: Retrieves F1 Race Report for a specific event.

| Parameter  | Type   | Default | Description                            | Required |
|------------|--------|---------|----------------------------------------|----------|
| `eventId`* | string | -       | The ID of the event                    | Yes      |

*: This eventId is the same as the race id. You can get it on ESPN or make some calls to schedule and get the id.

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/race-report?eventId=600041134', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "report": {
    "racestrip": {
      "name": "STC Saudi Arabian Grand Prix",
      "shortName": "STC Saudi Arabian GP",
      "date": "2024-03-07T13:30Z",
      "endDate": "2024-03-09T17:00Z",
      "season": 2024,
      "circuit": {
        "name": "Jeddah Street Circuit",
        "diagram": {
          "href": "https://a.espncdn.com/i/venues/f1/circuit-info/7104.svg",
          "width": 2000,
          "height": 1125,
          "alt": "",
          "rel": [
            "full",
            "circuit-info"
          ]
        },
        "countryFlag": {
          "href": "https://a.espncdn.com/i/teamlogos/countries/500/ksa.png",
          "alt": "Saudi Arabia",
          "rel": [
            "country-flag"
          ]
        }
      },
      "broadcasts": [
        {
          ...
```

### 8. **`GET /standings-controllers`**

- **Description**: Retrieves standings by controllers for a specific year.

| Parameter | Type   | Default | Description                            | Required |
|-----------|--------|---------|----------------------------------------|----------|
| `year`    | string | -       | The year to search for (YYYY)          | Yes      |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/standings-controllers?year=2024', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "standings": {
    "id": "1",
    "name": "constructor",
    "displayName": "Constructor Standings",
    "season": 2024,
    "seasonType": 2,
    "entries": [
      {
        "team": {
          "id": "106892",
          "name": "McLaren",
          "displayName": "McLaren",
          "abbreviation": "DH",
          "shortDisplayName": "McLaren",
          "color": "FF8700"
        },
        "stats": [
          {
            "name": "rank",
            "displayName": "Rank",
            "shortDisplayName": "RK",
            "description": "Rank",
            "abbreviation": "RK",
            "type": "rank",
            "value": 1,
            "displayValue": "1"
          },
          {
            "name": "points",
            ...
```

### 9. **`GET /standings-drivers`**

- **Description**: Retrieves standings by drivers for a specific year.

| Parameter | Type   | Default | Description                            | Required |
|-----------|--------|---------|----------------------------------------|----------|
| `year`    | string | -       | The year to search for (YYYY)          | Yes      |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/standings-drivers?year=2024', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "standings": {
    "id": "0",
    "name": "Driver",
    "displayName": "Driver Standings",
    "season": 2024,
    "seasonType": 2,
    "entries": [
      {
        "athlete": {
          "id": "4665",
          "uid": "s:2000~a:4665",
          "displayName": "Max Verstappen",
          "abbreviation": "VER",
          "name": "Max Verstappen",
          "shortName": "M. Verstappen",
          "flag": {
            "href": "https://a.espncdn.com/i/teamlogos/countries/500/ned.png",
            "alt": "Netherlands",
            "rel": [
              "country-flag"
            ]
          }
        },
        "stats": [
          {
            "name": "rank",
            "displayName": "Rank",
            "shortDisplayName": "RK",
            "description": "Rank",
            ...
```

### 10. **`GET /schedule`**

- **Description**: Retrieves F1 schedule for a specific year.

| Parameter | Type   | Default | Description                            | Required |
|-----------|--------|---------|----------------------------------------|----------|
| `year`    | string | -       | The year to search for (YYYY)          | Yes      |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/schedule?year=2024', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "20240229": [
    {
      "startDate": "2024-02-29T11:30Z",
      "endDate": "2024-03-02T15:00Z",
      "featuredAthletes": "featuredAthletes",
      "status": {
        "id": "3",
        "state": "post",
        "detail": "Final"
      },
      "completed": true,
      "gPrx": "Gulf Air Bahrain GP",
      "crct": "Bahrain International Circuit",
      "evLink": "/f1/race/_/id/600041133",
      "isPostponedOrCanceled": false,
      "winner": "M. Verstappen"
    }
  ],
  "20240307": [
    {
      "startDate": "2024-03-07T13:30Z",
      "endDate": "2024-03-09T17:00Z",
      "featuredAthletes": "featuredAthletes",
      "status": {
        "id": "3",
        "state": "post",
        "detail": "Final"
      },
      "completed": true,
      ...
```

### 11. **`GET /photos`**

- **Description**: Retrieves photos for a specific Formula 1 driver. It allows cross-origin requests by setting the required headers. Cached data is utilized if available to enhance response efficiency. If the requested data is not cached, it is fetched from the source, cached, and then returned.

| Parameter  | Type   | Default | Description                            | Required |
|------------|--------|---------|----------------------------------------|----------|
| `driverId` | string | -       | The ID of the driver                   | Yes      |
| `page`     | string | `1`     | The page number for paginated results  | No       |

Example request:

```javascript
fetch('https://f1-motorsport-data.p.rapidapi.com/photos?driverId=4665', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'f1-motorsport-data.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
[
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9894978",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F09%2F12%2F1271899792.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9857011",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F09%2F03%2F1270422145.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9857010",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F09%2F03%2F1270422143.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9857009",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F09%2F03%2F1270422144.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9843633",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F08%2F30%2F1269708993.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9843631",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F08%2F30%2F1269708992.jpg"
  },
  {
    "href": "https://www.espn.com/racing/driver/photos?id=4665&photoId=9843574",
    "imgSrc": "https://a.espncdn.com/combiner/i?img=media%2Fgettyphoto%2F2020%2F08%2F30%2F1269706217.jpg"
  },
  {
    ...
```

## Error Handling

The  API returns standard HTTP status codes to indicate the success or failure of API requests. Below are common errors and suggestions for handling them.

|Status Code|Message|Description|Suggested Handling|
|--|--|--|--|
| **400** | Bad Request | The request was malformed or missing required parameters (e.g., `domain` parameter not provided). | Verify that all required parameters are included and correctly formatted. |
| **401** | Unauthorized | Invalid or missing API key in the request headers. | Check that a valid API key is included in `x-rapidapi-key`. |
| **403** | Forbidden | Access to the requested resource is denied, possibly due to rate limits or restricted access. | Review rate limits and ensure API permissions. Retry after a delay if rate limit exceeded. |
| **404** | Not Found | The requested domain information could not be found (e.g., domain does not exist). | Check the spelling or availability of the domain. |
| **429** | Too Many Requests | The API rate limit has been exceeded. | Implement rate-limiting logic and retry after the specified rate limit reset time. |
| **500** | Internal Server Error | A server error occurred while processing the request. | Retry the request after a few seconds. If the error persists, contact API support. |
| **503** | Service Unavailable | The API service is temporarily unavailable (e.g., due to maintenance). | Retry the request later or check the API status page for maintenance alerts. |

## FAQs

### 1. What kind of data can I access through the F1 Motorsport Data API?

You can access live race data, driver and team information, race schedules, and historical race results.

### 2. How do I authenticate my API requests?

You must include your API key in the headers of your requests as outlined in the API documentation.

### 3. Are there usage limits for the API?

Yes, usage limits vary based on your chosen subscription plan. Check the RapidAPI dashboard for specifics.

### 4. Can I filter data by specific races or drivers?

Yes, the API allows filtering to retrieve data for specific races or individual drivers.

### 5. Is historical data available for past seasons?

Yes, the F1 Motorsport Data API includes historical data for previous seasons, allowing for detailed comparisons and analysis.

