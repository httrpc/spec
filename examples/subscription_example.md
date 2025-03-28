# Subscription Example

This example demonstrates how to create a subscription to receive real-time updates for a user.

## Request

### URL
```
GET /httrpc/users/userUpdates?args=eyJ0eXBlIjoibmFtZWQiLCJhcmdzIjp7ImlkIjoiMTIzIn19
```

### Headers
```
X-HTTRPC-Version: 1
Accept: text/event-stream
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Decoded Query Args
The base64-decoded `args` parameter contains:
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
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive
```

### Event Stream
```
event: data
data: {"data":{"id":"123","name":"John Doe","email":"john@example.com","age":30}}

event: data
data: {"data":{"id":"123","name":"John Doe","email":"john.doe@example.com","age":30}}

event: error
data: {"error":{"code":"INTERNAL_ERROR","message":"Connection lost to database"}}
``` 
