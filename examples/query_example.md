# Query Example

This example demonstrates how to make a query request to get a user by ID.

## Request

### URL
```
POST /httrpc/users/getUser
```

### Headers
```
X-HTTRPC-Version: 1
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Body
```json
{
  "type": "named",
  "args": {
    "id": "123"
  }
}
```

## Response

### Status Code
```
200 OK
```

### Headers
```
Content-Type: application/json
```

### Body
```json
{
  "data": {
    "id": "123",
    "name": "John Doe",
    "email": "john@example.com",
    "age": 30
  }
}
