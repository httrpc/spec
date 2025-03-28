# HTTP RPC Protocol (HTTRPC)

A language-agnostic RPC protocol over HTTP with type-safe schema support.

## Overview

HTTRPC is a simple, efficient protocol for implementing Remote Procedure Calls over HTTP. It provides:

- **Type safety** with JSON schema validation
- **Simple integration** with any language that supports HTTP
- **Multiple interaction patterns** including queries, mutations, and subscriptions
- **Flexible authentication** supporting various auth schemes

## Documentation

- [Full Specification](./SPEC.md) - Complete protocol details
- [Examples](./examples/) - Sample implementations in various languages
- [Schemas](./schemas/) - JSON schema definitions

## Quick Start

HTTRPC endpoints follow a consistent pattern:

```
/httrpc/<namespace>/<action>
```

### Basic Query

```http
GET /httrpc/users/getUser?args=eyJ0eXBlIjoicG9zaXRpb25hbCIsImFyZ3MiOlsxMjNdfQ==
X-HTTRPC-Version: 1
```

Where the args parameter is the base64 encoding of:
```json
{"type":"positional","args":[123]}
```

### Basic Mutation

```http
POST /httrpc/users/createUser
X-HTTRPC-Version: 1
Content-Type: application/json

{
  "type": "named",
  "args": {
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

## License

MIT
