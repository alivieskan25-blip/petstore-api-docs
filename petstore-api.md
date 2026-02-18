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
### Response fields description

| Field | Type | Описание |
|-------|------|----------|
| id | integer | The unique identifier of the pet |
| category | object | Pet's category information object |
| category.id | integer | Category ID |
| category.name | string | Category name (e.g, "cat", "dog") |
| name | string | Pet's name |
| photoUrls | array | List of photo URLs (may be empty) |
| tags | array | Tags list(each with id and name) |
| status | string | Pet status: available, pending or sold |

## Endpoint: Find pets by status

**URL:**(https://petstore.swagger.io/v2/pet/findByStatus)

**Method:** GET

**Description:** Returns the pets

### Query parameters

| Parameter | Type | Required |Description |
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

## Endpoint: Add a new pet to the store

**URL:** {{base_url}}/pet

**Method:** POST

**Description:** Adds a new pet to the store.The request body must contain the pet data in JSON format.

### Request Headers

| Header | Value | Description |
|--------|-------|-------------|
| `Content-Type` | `application/json` | Indicates that the request body is JSON. |

### Request Body Scheme

The request body must be a JSON object with the following structure:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | integer | Yes | Unique identifier for the pet. |
| `category` | object | Yes | An object containing the pet's category. |
| `category.id` | integer | Yes | Category ID. |
| `category.name` | string | Yes | Category name (e.g., `"cats"`, `"dogs"`). |
| `name` | string | Yes | Pet's name. |
| `photoUrls` | array | Yes | Array of photo URLs (can be empty). |
| `tags` | array | Yes | Array of tag objects. Each tag has `id` and `name`. |
| `tags[].id` | integer | Yes | Tag ID. |
| `tags[].name` | string | Yes | Tag name. |
| `status` | string | Yes | Pet status in the store: `available`, `pending`, or `sold`. |

### Request example

```json
{
  "id": 123456789,
  "category": {
    "id": 1,
    "name": "cats"
  },
  "name": "Barsik",
  "photoUrls": [
    "https://example.com/photo/barsik.jpg"
  ],
  "tags": [
    {
      "id": 1,
      "name": "fluffy"
    }
  ],
  "status": "available"
}
```

You can also use this cURL command to test the endpoint:

```bash
curl -X POST "{{base_url}}/pet" \
  -H "Content-Type: application/json" \
  -d '{
    "id": 123456789,
    "category": {
      "id": 1,
      "name": "cats"
    },
    "name": "Barsik",
    "photoUrls": [
      "https://example.com/photo/barsik.jpg"
    ],
    "tags": [
      {
        "id": 1,
        "name": "fluffy"
      }
    ],
    "status": "available"
  }'
  ```

  ### Response example (successful, code 200)

  If the pet is successfully created, the server returns the created pet object (usually the same as the request body, possibly with additional fields):

  ```
  {
  "id": 123456789,
  "category": {
    "id": 1,
    "name": "cats"
  },
  "name": "Barsik",
  "photoUrls": [
    "https://example.com/photo/barsik.jpg"
  ],
  "tags": [
    {
      "id": 1,
      "name": "fluffy"
    }
  ],
  "status": "available"
}
```
### Response fields

The response has the same structure as the request body (see the table above). Optionally, the server might include additional fields like *createdAt*, but in Petstore it's not present.

### Response codes

| Code | Description |
|------|-------------|
| 200 | Pet successfully created. |
| 405 | Invalid input (e.g., missing required field, wrong data type). |

