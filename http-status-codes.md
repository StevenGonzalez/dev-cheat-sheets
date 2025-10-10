# HTTP Status Codes Cheat Sheet

## Table of Contents

- [Overview](#overview)
- [1xx Informational](#1xx-informational)
- [2xx Success](#2xx-success)
- [3xx Redirection](#3xx-redirection)
- [4xx Client Errors](#4xx-client-errors)
- [5xx Server Errors](#5xx-server-errors)
- [Common Status Code Groups](#common-status-code-groups)
- [RESTful API Usage](#restful-api-usage)
- [Browser Behavior](#browser-behavior)
- [Caching Implications](#caching-implications)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Overview

HTTP status codes are three-digit numbers returned by web servers to indicate the result of a client's request. They are grouped into five classes based on the first digit.

### Status Code Format

```
HTTP/1.1 200 OK
HTTP/1.1 404 Not Found
HTTP/1.1 500 Internal Server Error
```

### Quick Reference

| Range | Category      | Purpose                                                 |
| ----- | ------------- | ------------------------------------------------------- |
| 1xx   | Informational | Request received, continuing process                    |
| 2xx   | Success       | Request successfully received, understood, and accepted |
| 3xx   | Redirection   | Further action needs to be taken to complete request    |
| 4xx   | Client Error  | Request contains bad syntax or cannot be fulfilled      |
| 5xx   | Server Error  | Server failed to fulfill valid request                  |

## 1xx Informational

### 100 Continue

```http
HTTP/1.1 100 Continue
```

- **Purpose**: Server has received request headers and client should proceed with request body
- **Use Case**: Large file uploads, form submissions
- **Client Action**: Send request body
- **Example**: Upload progress indication

### 101 Switching Protocols

```http
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
```

- **Purpose**: Server is switching protocols as requested by client
- **Use Case**: WebSocket upgrades, HTTP/2 upgrades
- **Client Action**: Switch to new protocol
- **Example**: WebSocket handshake completion

### 102 Processing (WebDAV)

```http
HTTP/1.1 103 Early Hints
Link: </style.css>; rel=preload; as=style
```

- **Purpose**: Server has received and is processing request
- **Use Case**: Long-running operations
- **Client Action**: Wait for final response
- **Example**: Complex database queries

### 103 Early Hints

```http
HTTP/1.1 103 Early Hints
Link: </style.css>; rel=preload; as=style
Link: </script.js>; rel=preload; as=script
```

- **Purpose**: Send preliminary response headers before final response
- **Use Case**: Performance optimization, resource preloading
- **Client Action**: Start preloading resources
- **Example**: CSS/JS preloading hints

## 2xx Success

### 200 OK

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "message": "Request successful",
  "data": { ... }
}
```

- **Purpose**: Request succeeded
- **Use Case**: Successful GET, POST, PUT operations
- **Response**: Contains requested resource or confirmation
- **Example**: API data retrieval, form submission success

### 201 Created

```http
HTTP/1.1 201 Created
Location: /api/users/123
Content-Type: application/json

{
  "id": 123,
  "message": "User created successfully"
}
```

- **Purpose**: Request succeeded and new resource was created
- **Use Case**: POST requests creating new resources
- **Headers**: Often includes `Location` header with new resource URL
- **Example**: User registration, article creation

### 202 Accepted

```http
HTTP/1.1 202 Accepted
Location: /api/jobs/456

{
  "jobId": 456,
  "status": "processing",
  "estimatedTime": "5 minutes"
}
```

- **Purpose**: Request accepted for processing but not completed
- **Use Case**: Asynchronous operations, batch processing
- **Response**: Often includes job ID or status endpoint
- **Example**: File processing, email sending, report generation

### 204 No Content

```http
HTTP/1.1 204 No Content
```

- **Purpose**: Request succeeded but no content to return
- **Use Case**: DELETE operations, PUT updates
- **Response**: Empty response body
- **Example**: Resource deletion, profile updates

### 206 Partial Content

```http
HTTP/1.1 206 Partial Content
Content-Range: bytes 200-1023/2048
Content-Length: 824

[partial file content]
```

- **Purpose**: Server is delivering part of resource due to range request
- **Use Case**: Video streaming, file downloads with resume capability
- **Headers**: `Content-Range`, `Content-Length`
- **Example**: Video player seeking, download managers

## 3xx Redirection

### 301 Moved Permanently

```http
HTTP/1.1 301 Moved Permanently
Location: https://www.example.com/new-url
```

- **Purpose**: Resource has permanently moved to new URL
- **Use Case**: URL restructuring, domain changes
- **SEO Impact**: Transfers search engine ranking to new URL
- **Browser**: Updates bookmarks, caches redirect
- **Example**: Site migration, URL cleanup

### 302 Found (Temporary Redirect)

```http
HTTP/1.1 302 Found
Location: /temporary-maintenance-page
```

- **Purpose**: Resource temporarily moved to different URL
- **Use Case**: Temporary maintenance, A/B testing
- **SEO Impact**: Preserves original URL ranking
- **Browser**: Doesn't cache redirect permanently
- **Example**: Maintenance pages, temporary promotions

### 304 Not Modified

```http
HTTP/1.1 304 Not Modified
ETag: "abc123"
Cache-Control: max-age=3600
```

- **Purpose**: Resource hasn't changed since last request
- **Use Case**: Conditional requests with `If-Modified-Since` or `If-None-Match`
- **Performance**: Saves bandwidth by not resending content
- **Headers**: `ETag`, `Cache-Control`, `Last-Modified`
- **Example**: Browser caching, API caching

### 307 Temporary Redirect

```http
HTTP/1.1 307 Temporary Redirect
Location: /api/v2/users
```

- **Purpose**: Temporary redirect that preserves request method
- **Use Case**: API versioning, temporary endpoints
- **Difference from 302**: Guarantees method preservation (POST stays POST)
- **Example**: API maintenance, load balancing

### 308 Permanent Redirect

```http
HTTP/1.1 308 Permanent Redirect
Location: https://api.example.com/v2/endpoint
```

- **Purpose**: Permanent redirect that preserves request method
- **Use Case**: API versioning, HTTPS enforcement
- **Difference from 301**: Guarantees method preservation
- **Example**: API migrations, secure redirects

## 4xx Client Errors

### 400 Bad Request

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Invalid JSON syntax",
  "details": "Unexpected token at line 3"
}
```

- **Purpose**: Server cannot process request due to client error
- **Use Case**: Malformed JSON, invalid parameters, syntax errors
- **Response**: Should include error details
- **Example**: Invalid form data, malformed API requests

### 401 Unauthorized

```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer realm="api"

{
  "error": "Authentication required",
  "message": "Please provide valid credentials"
}
```

- **Purpose**: Authentication is required and has failed or not provided
- **Use Case**: Missing or invalid credentials
- **Headers**: `WWW-Authenticate` header indicates auth method
- **Example**: Missing API key, expired token, wrong password

### 403 Forbidden

```http
HTTP/1.1 403 Forbidden

{
  "error": "Access denied",
  "message": "Insufficient permissions to access this resource"
}
```

- **Purpose**: Server understood request but refuses to authorize it
- **Use Case**: Insufficient permissions, resource restrictions
- **Difference from 401**: User is authenticated but not authorized
- **Example**: Admin-only endpoints, private resources

### 404 Not Found

```http
HTTP/1.1 404 Not Found

{
  "error": "Resource not found",
  "message": "User with ID 123 does not exist"
}
```

- **Purpose**: Server cannot find requested resource
- **Use Case**: Broken links, deleted resources, wrong URLs
- **Response**: Often includes suggestions or search functionality
- **Example**: Deleted blog post, wrong API endpoint, typos in URL

### 405 Method Not Allowed

```http
HTTP/1.1 405 Method Not Allowed
Allow: GET, POST, PUT

{
  "error": "Method not allowed",
  "allowed": ["GET", "POST", "PUT"]
}
```

- **Purpose**: Request method not supported for requested resource
- **Use Case**: DELETE on read-only resource, POST to static endpoint
- **Headers**: `Allow` header lists supported methods
- **Example**: POST to GET-only endpoint

### 409 Conflict

```http
HTTP/1.1 409 Conflict

{
  "error": "Conflict",
  "message": "Email address already exists",
  "conflictingField": "email"
}
```

- **Purpose**: Request conflicts with current state of server
- **Use Case**: Duplicate entries, concurrent modifications, version conflicts
- **Response**: Should explain the conflict
- **Example**: Duplicate email registration, optimistic locking conflicts

### 410 Gone

```http
HTTP/1.1 410 Gone

{
  "error": "Resource permanently removed",
  "message": "This API version has been discontinued"
}
```

- **Purpose**: Resource was available previously but is permanently gone
- **Use Case**: Deprecated API versions, deleted content with no redirect
- **Difference from 404**: Indicates resource existed before
- **Example**: Deprecated API endpoints, expired promotional content

### 422 Unprocessable Entity

```http
HTTP/1.1 422 Unprocessable Entity

{
  "error": "Validation failed",
  "violations": [
    {
      "field": "email",
      "message": "Invalid email format"
    },
    {
      "field": "age",
      "message": "Must be at least 18"
    }
  ]
}
```

- **Purpose**: Request syntactically correct but semantically invalid
- **Use Case**: Validation failures, business rule violations
- **Response**: Detailed validation errors
- **Example**: Form validation errors, data constraint violations

### 429 Too Many Requests

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 60
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1640995200

{
  "error": "Rate limit exceeded",
  "retryAfter": 60
}
```

- **Purpose**: Client has sent too many requests in given time frame
- **Use Case**: API rate limiting, abuse prevention
- **Headers**: `Retry-After`, `X-RateLimit-*` headers
- **Example**: API throttling, spam prevention

## 5xx Server Errors

### 500 Internal Server Error

```http
HTTP/1.1 500 Internal Server Error

{
  "error": "Internal server error",
  "message": "An unexpected error occurred",
  "requestId": "req_123456789"
}
```

- **Purpose**: Generic server error when no specific error is appropriate
- **Use Case**: Unhandled exceptions, server crashes, database errors
- **Response**: Should not expose internal details in production
- **Example**: Database connection failures, unhandled exceptions

### 501 Not Implemented

```http
HTTP/1.1 501 Not Implemented

{
  "error": "Not implemented",
  "message": "PATCH method not supported"
}
```

- **Purpose**: Server doesn't support functionality required to fulfill request
- **Use Case**: Unimplemented HTTP methods, missing features
- **Example**: PATCH method not implemented, unsupported API features

### 502 Bad Gateway

```http
HTTP/1.1 502 Bad Gateway

{
  "error": "Bad Gateway",
  "message": "Upstream server returned invalid response"
}
```

- **Purpose**: Server acting as gateway received invalid response from upstream
- **Use Case**: Proxy/gateway errors, microservice communication failures
- **Example**: Load balancer can't reach backend, API gateway errors

### 503 Service Unavailable

```http
HTTP/1.1 503 Service Unavailable
Retry-After: 300

{
  "error": "Service temporarily unavailable",
  "message": "Server is under maintenance",
  "retryAfter": 300
}
```

- **Purpose**: Server temporarily unable to handle request
- **Use Case**: Maintenance mode, server overload, temporary outages
- **Headers**: `Retry-After` suggests when to retry
- **Example**: Scheduled maintenance, traffic spikes, deployment

### 504 Gateway Timeout

```http
HTTP/1.1 504 Gateway Timeout

{
  "error": "Gateway timeout",
  "message": "Upstream server did not respond in time"
}
```

- **Purpose**: Server acting as gateway didn't receive timely response from upstream
- **Use Case**: Slow backend services, network timeouts
- **Example**: Database query timeout, slow API responses

## Common Status Code Groups

### Authentication & Authorization

```http
401 Unauthorized    # Missing or invalid credentials
403 Forbidden      # Authenticated but not authorized
407 Proxy Authentication Required
```

### Content Negotiation

```http
300 Multiple Choices
406 Not Acceptable     # Cannot produce content matching Accept headers
415 Unsupported Media Type  # Content-Type not supported
```

### Caching Related

```http
304 Not Modified      # Resource unchanged
412 Precondition Failed  # If-Match, If-Unmodified-Since failed
```

### Rate Limiting & Abuse

```http
429 Too Many Requests
420 Enhance Your Calm (Twitter)
```

## RESTful API Usage

### Resource Creation

```http
POST /api/users
201 Created           # User successfully created
400 Bad Request       # Invalid user data
409 Conflict         # Email already exists
422 Unprocessable Entity  # Validation errors
```

### Resource Retrieval

```http
GET /api/users/123
200 OK               # User found and returned
404 Not Found        # User doesn't exist
304 Not Modified     # Cached version is current
```

### Resource Updates

```http
PUT /api/users/123
200 OK               # Update successful, return updated resource
204 No Content       # Update successful, no content returned
404 Not Found        # User doesn't exist
409 Conflict         # Concurrent modification
422 Unprocessable Entity  # Validation errors
```

### Resource Deletion

```http
DELETE /api/users/123
204 No Content       # Deletion successful
404 Not Found        # User doesn't exist
409 Conflict         # User has dependencies
```

### Collection Operations

```http
GET /api/users
200 OK               # List of users
200 OK + empty array # No users found (not 404)

GET /api/users?page=999
200 OK + empty array # Page beyond results (not 404)
400 Bad Request      # Invalid query parameters
```

## Browser Behavior

### Automatic Redirects

```http
301, 302, 307, 308   # Browsers automatically follow
3xx with Location header
```

### Caching Behavior

```http
200, 301, 410        # Cacheable by default
304                  # Validates cache freshness
Cache-Control: no-cache  # Always revalidate
Cache-Control: no-store  # Never cache
```

### Error Page Display

```http
4xx, 5xx            # Browsers may show error pages
404                 # Custom 404 pages common
500                 # Generic error pages
```

### Method Handling

```http
GET, HEAD           # Safe methods, cacheable
POST, PUT, DELETE   # May trigger confirmation dialogs
PATCH               # Not supported by all browsers
```

## Caching Implications

### Cacheable Status Codes

```http
200 OK              # Cache with proper headers
301 Moved Permanently  # Cache redirect permanently
304 Not Modified    # Refresh cache validation
410 Gone           # Cache the fact it's gone
```

### Cache Headers

```http
Cache-Control: max-age=3600        # Cache for 1 hour
Cache-Control: no-cache           # Always validate
ETag: "abc123"                    # Entity tag for validation
Last-Modified: Wed, 21 Oct 2015   # Modification date
Expires: Thu, 01 Dec 1994         # Absolute expiry
```

### CDN Considerations

```http
200, 301, 404      # Often cached by CDNs
Cache-Control: public    # Explicitly cacheable
Cache-Control: private   # Not cacheable by shared caches
Vary: Accept-Encoding    # Cache varies by header
```

## Best Practices

### Choosing Appropriate Status Codes

```http
# Resource Creation
POST /users
201 Created + Location header    # New resource created
200 OK                          # Existing resource updated
409 Conflict                    # Duplicate detected

# Resource Updates
PUT /users/123
200 OK + response body          # Updated resource returned
204 No Content                  # Update confirmed, no body
404 Not Found                   # Resource doesn't exist

# Error Responses
400 Bad Request                 # Client error, fixable
422 Unprocessable Entity       # Validation errors
500 Internal Server Error      # Server error, not client's fault
```

### Error Response Bodies

```javascript
// Good: Detailed error information
{
  "error": "ValidationError",
  "message": "Request validation failed",
  "details": [
    {
      "field": "email",
      "code": "INVALID_FORMAT",
      "message": "Email must be a valid email address"
    }
  ],
  "timestamp": "2023-10-09T10:30:00Z",
  "requestId": "req_abc123"
}

// Bad: Generic or no error information
{
  "error": "Error occurred"
}
```

### Status Code Consistency

```javascript
// Consistent pattern across your API
app.post('/users', (req, res) => {
  try {
    const user = await createUser(req.body);
    res.status(201).json(user);
  } catch (ValidationError) {
    res.status(422).json({ error: 'Validation failed' });
  } catch (ConflictError) {
    res.status(409).json({ error: 'Email already exists' });
  }
});
```

### Documentation Standards

```yaml
# OpenAPI specification example
paths:
  /users:
    post:
      responses:
        201:
          description: User created successfully
        400:
          description: Invalid request data
        409:
          description: Email already exists
        422:
          description: Validation errors
```

## Troubleshooting

### Common Issues

#### Wrong Status Code Usage

```http
# Wrong: 200 for not found
GET /api/users/999
200 OK
{ "user": null }

# Correct: 404 for not found
GET /api/users/999
404 Not Found
{ "error": "User not found" }
```

#### Missing Location Headers

```http
# Wrong: 201 without Location
POST /api/users
201 Created
{ "id": 123, "name": "John" }

# Correct: 201 with Location
POST /api/users
201 Created
Location: /api/users/123
{ "id": 123, "name": "John" }
```

#### Inconsistent Error Format

```http
# Inconsistent error responses
400 Bad Request: { "message": "Invalid input" }
404 Not Found: { "error": "Not found" }
422 Validation: { "errors": [...] }

# Consistent error format
400 Bad Request: { "error": "BadRequest", "message": "Invalid input" }
404 Not Found: { "error": "NotFound", "message": "Resource not found" }
422 Validation: { "error": "ValidationError", "message": "Validation failed", "details": [...] }
```

### Debugging Status Codes

#### Browser Developer Tools

```javascript
// Check response status in browser console
fetch("/api/users").then((response) => {
  console.log("Status:", response.status);
  console.log("Status Text:", response.statusText);
  console.log("OK:", response.ok); // true for 2xx
});
```

#### Curl Commands

```bash
# Check status code with curl
curl -I http://example.com/api/users
curl -w "%{http_code}\n" -s -o /dev/null http://example.com

# Follow redirects
curl -L http://example.com

# Include response headers
curl -i http://example.com/api/users
```

#### Server-side Logging

```javascript
// Express.js middleware to log status codes
app.use((req, res, next) => {
  const originalSend = res.send;
  res.send = function (data) {
    console.log(`${req.method} ${req.path} - ${res.statusCode}`);
    originalSend.call(this, data);
  };
  next();
});
```

### Status Code Testing

```javascript
// Jest test examples
describe("API Status Codes", () => {
  test("returns 200 for existing user", async () => {
    const response = await request(app).get("/api/users/1");
    expect(response.status).toBe(200);
  });

  test("returns 404 for non-existing user", async () => {
    const response = await request(app).get("/api/users/999");
    expect(response.status).toBe(404);
  });

  test("returns 201 when creating user", async () => {
    const response = await request(app)
      .post("/api/users")
      .send({ name: "John", email: "john@example.com" });
    expect(response.status).toBe(201);
    expect(response.headers.location).toMatch(/\/api\/users\/\d+/);
  });
});
```

### Performance Monitoring

```javascript
// Monitor status code distribution
const statusCodes = {
  "2xx": 0,
  "3xx": 0,
  "4xx": 0,
  "5xx": 0,
};

app.use((req, res, next) => {
  res.on("finish", () => {
    const statusClass = `${Math.floor(res.statusCode / 100)}xx`;
    statusCodes[statusClass]++;
  });
  next();
});

// Alert on high error rates
setInterval(() => {
  const errorRate =
    (statusCodes["4xx"] + statusCodes["5xx"]) /
    Object.values(statusCodes).reduce((a, b) => a + b, 0);
  if (errorRate > 0.1) {
    console.warn("High error rate detected:", errorRate);
  }
}, 60000); // Check every minute
```

## Tools & References

### Essential Resources

- **MDN HTTP Status Codes**: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status - Complete reference
- **IANA Status Code Registry**: https://www.iana.org/assignments/http-status-codes/ - Official registry
- **RFC 9110**: https://www.rfc-editor.org/rfc/rfc9110.html - HTTP Semantics specification
