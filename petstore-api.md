# API Petstore

## Endpoint: receive a pet with ID

**URL:** (https://petstore.swagger.io/v2/pet/{petId})

**Method:** `GET`

**Description:** Returns information about a pet by its unique identifier.

### Request parameters

| Parameter | Type    | Required | Description                    |
|-----------|---------|----------|--------------------------------|
| petId     | integer | Yes      | ID of the pet (e.g., 1)        |

### Request example

[GET] (https://petstore.swagger.io/v2/pet/1)

### Response example (successful, code 200)

```json
{
  "id": 1,
  "category": {
    "id": 1,
    "name": "cat"
  },
  "name": "dog",
  "photoUrls": [],
  "tags": [],
  "status": "sold"
}
```
## Endpoint: Find pets by status

**URL:**(https://petstore.swagger.io/v2/pet/findByStatus)

**Method:** GET

**Description:** Returns the pets

### Query parameters

| Parameter | Type | Status |Description |
|-----------|------|--------|------------------------|
| status | string | Yes | Status of pets to return. Available values: `available`, `pending`, `sold`.|

### Request example

[GET] (https://petstore.swagger.io/v2/pet/findByStatus?status=available)

### Response example (successful, code 200)

The response is an array of pet objects. Below is an example containing two elements:

```json
[
  {
    "id": 9223372036854776000,
    "category": {
      "id": 0,
      "name": "Michale"
    },
    "name": "doggie",
    "photoUrls": ["string"],
    "tags": [
      {
        "id": 59623654,
        "name": "string"
      }
    ],
    "status": "available"
  },
  {
    "id": 40303748,
    "category": {
      "id": 38394334,
      "name": "fish"
    },
    "name": "Nemo",
    "photoUrls": [
      "non nulla culpa",
      "https://pbs.twimg.com/profile_images/786145766192648192/asPAQcOZ_400x400.jpg"
    ],
    "tags": [
      {
        "id": -41408652,
        "name": "ad ea ut"
      },
      {
        "id": -82715229,
        "name": "sint nostrud lab"
      }
    ],
    "status": "available"
  }
]
```
### Response fields description

Each object in the array has the following structure:

| Field | Type | Description |
|-------|--------|------------------------|
| id  | integer | Unique pet identifier |
| category | object | Object containing category details (see below) |
| name | string | Pet's name |
| photoUrls | array | List of photo URLs (may be empty) |
| tags | array | List of tag objects (each with id and name) |
| status | string | Pet status: available, pending, or sold |

The category object has the following fields:

| Field |	Type | Description |
|-------|-------|-------------|
| id | integer |	Category ID |
| name | string | Category name |

The tags array contains objects with:

| Field |	Type | Description |
|-------|-------|-------------|
| id | integer | Tag ID |
| name | string |	Tag name |

### Response codes

| Code | Description |
|-------|-------------|
| 200 | Successful request |
| 400	| Invalid status value |

