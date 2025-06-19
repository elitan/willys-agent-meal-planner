# Willys.se API Documentation

_Reverse engineered API documentation for Willys.se Swedish grocery store_

## Base Endpoint

```
https://www.willys.se/search
```

## API Overview

The Willys.se search API is a REST API that returns product information in JSON format. It supports full-text search with pagination, filtering, and sorting capabilities.

## Required Headers

```bash
Accept: */*
Accept-Language: en-GB,en;q=0.9
Content-Type: application/json
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36
```

## Query Parameters

| Parameter | Type    | Required | Description                              | Example                                       |
| --------- | ------- | -------- | ---------------------------------------- | --------------------------------------------- |
| `q`       | string  | Yes      | Search query term                        | `ost`, `kaffe`, `bröd`                        |
| `page`    | integer | No       | Page number (0-based)                    | `0`, `1`, `2`                                 |
| `size`    | integer | No       | Number of results per page (default: 30) | `10`, `30`, `50`                              |
| `sort`    | string  | No       | Sort order                               | `price:asc`, `price:desc`, `name_text_sv:asc` |

## Available Sort Options

- `relevance` - Relevance (default)
- `ranking_int:asc` - Most popular
- `name_text_sv:asc` - A – Ö
- `name_text_sv:desc` - Ö – A
- `price:asc` - Price (Cheapest - Most expensive)
- `price:desc` - Price (Most expensive - Cheapest)
- `compareprice:asc` - Compare price (Cheapest - Most expensive)
- `compareprice:desc` - Compare price (Most expensive - Cheapest)

## Example Requests

### Basic Search

```bash
curl 'https://www.willys.se/search?q=ost&page=0&size=30' \
  -H 'accept: */*' \
  -H 'accept-language: en-GB,en;q=0.9' \
  -H 'content-type: application/json' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'
```

### Search with Sorting

```bash
curl 'https://www.willys.se/search?q=kaffe&size=5&sort=price:asc' \
  -H 'accept: */*' \
  -H 'accept-language: en-GB,en;q=0.9' \
  -H 'content-type: application/json' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'
```

## Response Structure

The API returns a JSON object with the following main sections:

### Top Level

```json
{
  "results": [...],           // Array of product objects
  "pagination": {...},        // Pagination information
  "sorts": [...],            // Available sort options
  "facets": [...],           // Filter/facet options
  "freeTextSearch": "ost",   // The search term used
  "breadcrumbs": [],         // Category breadcrumbs
  // ... other metadata
}
```

### Product Object Structure

Each product in the `results` array contains:

```json
{
  "code": "101230572_KG",           // Product code/ID
  "name": "Gouda 28%",              // Product name
  "price": "84,90 kr",              // Formatted price string
  "priceValue": 84.9,               // Numeric price value
  "comparePrice": "84,90 kr",       // Price per unit for comparison
  "comparePriceUnit": "kg",         // Unit for comparison (kg, st, etc.)
  "priceUnit": "kr/kg",             // Price unit description
  "manufacturer": "Eldorado",        // Brand/manufacturer
  "displayVolume": "ca: 1.2kg",     // Package size
  "productLine2": "ELDORADO, ca: 1.2kg", // Product line info
  "outOfStock": false,              // Stock status
  "online": true,                   // Available online
  "image": {                        // Product image
    "url": "https://assets.axfood.se/image/upload/f_auto,t_200/...",
    "imageType": "PRIMARY",
    "format": "product"
  },
  "thumbnail": {...},               // Thumbnail image
  "potentialPromotions": [...],     // Current promotions/discounts
  "labels": [...],                  // Product labels (ecological, etc.)
  // ... many other fields
}
```

### Pagination Object

```json
{
  "pageSize": 30,
  "currentPage": 0,
  "numberOfPages": 19,
  "totalNumberOfResults": 554
}
```

### Facets (Filters)

The API provides filtering options via facets:

- **productLabelTypes**: Ekologisk, Fairtrade, Glutenfri, Laktosfri, etc.
- **category**: Ost, Kaffe, Bröd, Chark, etc.
- **commercialName2**: Brand names (Arla, Garant, Eldorado, etc.)

## Individual Product API

### Endpoint

```
https://www.willys.se/axfood/rest/p/{product_code}
```

### Usage

To get detailed information about a specific product, use the product `code` from the search results in this endpoint.

### Example Request

```bash
curl 'https://www.willys.se/axfood/rest/p/101332175_ST' \
  -H 'accept: */*' \
  -H 'accept-language: en-GB,en;q=0.9' \
  -H 'content-type: application/json' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36'
```

### Product Code Format

Product codes follow these patterns:

- `101332175_ST` - Individual items (ST = Stycke/Piece)
- `101230572_KG` - Weight-based items (KG = Kilogram)

### Detailed Product Response

This endpoint provides much more detailed information than the search API:

```json
{
  "code": "101332175_ST",
  "name": "Gräddis Skivad Ost 30%",
  "description": "Arla® Familjefavoriter - detailed product description...",
  "ingredients": "Pastöriserad MJÖLK, salt, syrningskultur, ystenzym.",
  "nutritionsFactList": [
    {
      "value": "1530",
      "typeCode": "energi",
      "unitCode": "kilojoule"
    },
    {
      "value": "370",
      "typeCode": "energi",
      "unitCode": "kilokalori"
    }
    // ... more nutritional data
  ],
  "breadcrumbs": [...],           // Category navigation
  "minStorageTemperature": "2°C",
  "maxStorageTemperature": "8°C",
  "tradeItemCountryOfOrigin": "Danmark",
  "nutritionalClaim": "Naturligt rik på kalcium",
  "consumerStorageInstructions": "",
  "image": {
    "format": "zoom",
    "url": "https://assets.axfood.se/image/upload/f_auto,t_500/..."
  }
  // ... many more detailed fields
}
```

### Additional Data Available

- **Nutritional Information**: Complete nutrition facts per 100g
- **Ingredients**: Full ingredient list
- **Storage Instructions**: Temperature and storage requirements
- **Origin Information**: Country of origin
- **Breadcrumbs**: Category hierarchy
- **High-res Images**: Larger product images
- **Health Claims**: Nutritional and health claims
- **EAN Code**: European Article Number barcode

## How to Find Product IDs

To get individual product information:

1. **Search for products** using the search API: `https://www.willys.se/search?q=your_search_term`
2. **Extract the product code** from the `code` field in search results
3. **Use the product code** in the individual product API: `https://www.willys.se/axfood/rest/p/{code}`

### Example Workflow

```bash
# 1. Search for cheese products
curl 'https://www.willys.se/search?q=ost&size=5' | jq '.results[0].code'
# Returns: "101230572_KG"

# 2. Get detailed product information
curl 'https://www.willys.se/axfood/rest/p/101230572_KG' | jq '.name, .ingredients'
# Returns detailed product data
```

## Key Findings

1. **Swedish Grocery Store**: Willys.se is a Swedish grocery store chain (part of Axfood)
2. **Comprehensive Product Data**: Rich product information including prices, images, nutritional info, promotions
3. **Advanced Search**: Supports faceted search, sorting, and pagination
4. **Real-time Data**: Includes stock status and current promotions
5. **Swedish Language**: Product names and categories are in Swedish
6. **Image Assets**: High-quality product images hosted on `assets.axfood.se`

## Rate Limiting & Usage Notes

- No obvious rate limiting detected in testing
- API appears to be public (no authentication required)
- **Swedish characters (ä, ö, å) must be URL encoded in search queries**
- Some search terms may return HTTP 400 errors if improperly formatted

### **Swedish Character URL Encoding**

When searching for Swedish terms, special characters must be URL encoded:

| Character | URL Encoded | Example Term | Encoded Query      |
| --------- | ----------- | ------------ | ------------------ |
| **å**     | `%C3%A5`    | blåbär       | `bl%C3%A5b%C3%A4r` |
| **ä**     | `%C3%A4`    | kött         | `k%C3%B6tt`        |
| **ö**     | `%C3%B6`    | mjölk        | `mj%C3%B6lk`       |

### **Working Examples with Swedish Characters**

```bash
# ❌ This will fail with HTTP 400
curl 'https://www.willys.se/search?q=blåbär&size=2'

# ✅ This works correctly
curl 'https://www.willys.se/search?q=bl%C3%A5b%C3%A4r&size=2'

# ✅ Other working examples
curl 'https://www.willys.se/search?q=mj%C3%B6lk&size=2'  # mjölk (milk)
curl 'https://www.willys.se/search?q=k%C3%B6tt&size=2'   # kött (meat)
curl 'https://www.willys.se/search?q=br%C3%B6d&size=2'   # bröd (bread)
```

## Sample Data Points

From testing `q=ost` (cheese):

- 554 total results across 19 pages
- Price range from ~54 kr to 159 kr
- Various cheese types: Gouda, Hushållsost, Gräddost, etc.
- Multiple brands: Arla, Eldorado, Skånemejerier, etc.
- Rich filtering options by brand, category, and labels
