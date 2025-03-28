# HTTP RPC Protocol Specification v1

## Overview
Language-agnostic RPC protocol over HTTP with type-safe schema support.

## Endpoints
All endpoints are prefixed with `/httrpc`

### Queries
- Method: POST
- Path: `/httrpc/<namespace>/<action>`
- Headers:
  - `Content-Type: application/json`
  - `X-HTTRPC-Version: 1`
  - Authentication headers (if required)

### Mutations
- Method: POST
- Path: `/httrpc/<namespace>/<action>`
- Headers:
  - `Content-Type: application/json`
  - `X-HTTRPC-Version: 1`
  - Authentication headers (if required)

### Subscriptions
- Protocol: Server-Sent Events (SSE)
- Method: GET
- Path: `/httrpc/<namespace>/<action>`
- Headers:
  - `Accept: text/event-stream`
  - `X-HTTRPC-Version: 1`
  - Authentication headers (if required)
- Query: `?args=<base64-encoded-args>`

## Request Format

### Query Request
```json
{
  "type": "positional|named",
  "args": [value1, value2] | {"name1": value1, "name2": value2}
}
```

### Mutation Request
```json
{
  "type": "positional|named",
  "args": [value1, value2] | {"name1": value1, "name2": value2}
}
```

### Subscription Events

Server -> Client event format:
```text
event: data
data: {"data": <payload>}

event: error
data: {"error": {"code": "ERROR_CODE", "message": "Error description"}}
```

SSE automatically handles:
- Reconnection with Last-Event-ID
- Keep-alive
- Connection management

Error message:
```json
{
  "type": "error",
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description"
  }
}
```

## Response Format

### Success Response
```json
{
  "data": <result>
}
```

### Error Response
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description",
    "data": {} // Optional additional info
  }
}
```

## Authentication
Authentication can be defined at namespace or action level.

### Supported Schemes

#### Bearer Token
```json
{
  "type": "bearer",
  "in": "header"
}
```
Adds `Authorization: Bearer <token>` header

#### API Key
```json
{
  "type": "apiKey",
  "in": "header",
  "name": "X-API-Key"
}
```
Adds custom header with API key

#### Basic Auth
```json
{
  "type": "basic"
}
```
Adds standard HTTP Basic Authentication header

## Schema Structure
Schema is defined in JSON format and follows JSON Schema standards.

### Root Fields
- version: Schema version
- auth: Authentication scheme definitions
- types: Type definitions
- rpc: RPC endpoint definitions

### Type System
Basic types:
- string
- number
- boolean
- null

Complex types:
- object
- array

Type Reference:
Use `$ref` to reference other types, following JSON Schema reference format: `{"$ref": "#/types/TypeName"}`

### Type Definition
```json
{
  "type": "object|array|string|number|boolean",
  "properties": {}, // for objects (JSON Schema compatible)
  "required": [], // array of required property names
  "items": {}, // for arrays
  "format": "", // string format (e.g., email, date-time)
  "minimum": 0, // for numbers
  "maximum": 100, // for numbers
  "minLength": 1, // for strings
  "maxLength": 255 // for strings
}
```

## Error Codes
Standard error codes:
- INVALID_INPUT
- UNAUTHORIZED
- NOT_FOUND
- INTERNAL_ERROR
- VALIDATION_ERROR
