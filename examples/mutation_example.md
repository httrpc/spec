# Mutation Example

This example demonstrates how to make a mutation request to create a new user.

## Request

### URL
```
POST /httrpc/users/createUser
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
    "name": "Jane Smith",
    "email": "jane@example.com",
    "age": 28
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
    "id": "456",
    "name": "Jane Smith",
    "email": "jane@example.com",
    "age": 28
  }
}
```
