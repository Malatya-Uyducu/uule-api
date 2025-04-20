# Local & International Google SERP Checker API

![UULE Search API](https://img.shields.io/badge/API-UULE%20Search-4361ee)
![Location-based](https://img.shields.io/badge/Search-Location%20Based-4895ef)
![Google SERP](https://img.shields.io/badge/SERP-Google-4cc9f0)

A powerful API for conducting location-based Google searches using the UULE parameter. This tool enables you to view Google search results as if you were searching from specific geographic locations worldwide.

## 🌍 Overview

The Local & International Google SERP Checker API allows you to:

- Perform Google searches targeted to specific geographic locations
- Test SEO performance across different regions and countries
- Compare search results between multiple locations
- Generate valid UULE parameters for location-based searches
- Redirect to Google search results or receive JSON data for analysis

Perfect for SEO professionals, marketers, researchers, and developers who need to check how search results vary by location.

## ⚙️ How It Works

The API generates a valid UULE (Universal Unique Location Entity) parameter based on the provided location and country code. This parameter is used to tell Google which location to use for search results.

## 📖 API Documentation

### Basic Usage

Send a GET request to the API endpoint:

```
GET https://www.malatyauyducum.com/search/search_api.php?location=POSTAL_CODE&query=SEARCH_QUERY&country=COUNTRY_CODE
```

### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `location` | Yes | - | Postal code or place name. Specifies the location for the search. |
| `query` | Yes | - | The search query to look up on Google. |
| `country` | No | TR | Two-letter ISO country code (e.g., TR, US, DE, GB). |
| `format` | No | json | Response format. Can be `json` or `redirect`. |

### Example Requests

**Simple Query (JSON response)**:
```
GET https://www.malatyauyducum.com/search/search_api.php?location=34000&query=pizza&country=TR
```

**Query with Place Name**:
```
GET https://www.malatyauyducum.com/search/search_api.php?location=istanbul&query=weather+forecast&country=TR
```

**Direct Redirect to Google**:
```
GET https://www.malatyauyducum.com/search/search_api.php?location=90210&query=best+restaurants&country=US&format=redirect
```

### Response Format

By default, the API returns data in JSON format:

```json
{
  "success": true,
  "search_url": "https://google.com.tr/search?q=pizza&gl=TR&hl=tr&uule=a+CMKC...",
  "location": {
    "input": "34000",
    "resolved": "Istanbul",
    "country": "TR",
    "latitude": 41.0138,
    "longitude": 28.9496
  },
  "query": "pizza",
  "uule": "a+CMKC..."
}
```

## 🧰 Code Examples

### JavaScript (Fetch API)

```javascript
// Sending a request to the API
async function searchWithLocation(location, query, country = 'TR') {
  try {
    const url = `https://www.malatyauyducum.com/search/search_api.php?location=${encodeURIComponent(location)}&query=${encodeURIComponent(query)}&country=${country}`;
    const response = await fetch(url);
    
    if (!response.ok) {
      throw new Error(`API request failed: ${response.status}`);
    }
    
    const data = await response.json();
    
    if (data.success) {
      // Use the search URL
      window.open(data.search_url, '_blank');
    } else {
      // Show error message
      console.error(data.error);
    }
  } catch (error) {
    console.error('Request error:', error);
  }
}
```

### PHP (cURL)

```php
// Sending a request to the API
function searchWithLocation($location, $query, $country = 'TR') {
  $url = "https://www.malatyauyducum.com/search/search_api.php?location=" . urlencode($location) . 
         "&query=" . urlencode($query) . 
         "&country=" . $country;
         
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
  $response = curl_exec($ch);
  
  if (curl_errno($ch)) {
    echo 'Request error: ' . curl_error($ch);
    return false;
  }
  
  curl_close($ch);
  $data = json_decode($response, true);
  
  if ($data['success']) {
    // Use the search URL
    header("Location: " . $data['search_url']);
    exit;
  } else {
    // Show error message
    echo 'API error: ' . $data['error'];
  }
}
```

## 📋 Supported Countries

The API currently supports the following countries:

- TR (Turkey)
- US (United States)
- SE (Sweden)
- SG (Singapore)
- SK (Slovakia)
- SI (Slovenia)
- UA (Ukraine)
- TH (Thailand)
- UY (Uruguay)
- ZA (South Africa)
- And several others

## ⚠️ Limitations

- The API uses UULE parameter generation which is not an official feature of Google Search API and may change over time
- Search results are subject to Google's search algorithms and may vary
- No rate limiting is implemented on the API, but reasonable usage is expected

## 🔍 About UULE Parameter

The UULE parameter is a base64-encoded location string that Google uses to determine the location context for search results. This API provides an easy way to generate valid UULE parameters without having to manually encode the location data.

---

Keywords: uule, uule create, uule api, Local & International Google SERP Checker, location-based search, Google search by location, SERP checker 
