# API Petstore

## Endpoint: receive a pet with ID

**URL:** `https://petstore.swagger.io/v2/pet/{petId}`

**Method:** `GET`

**Description:** Returns information about a pet by its unique identifier.

### Request parameters

### Request parameters

| Parameter | Type    | Required | Description                    |
|-----------|---------|----------|--------------------------------|
| petId     | integer | Yes      | ID of the pet (e.g., 1)        |

### Request example

`GET https://petstore.swagger.io/v2/pet/1`

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