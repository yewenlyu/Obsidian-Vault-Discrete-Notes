---
aliases:
  - CORS
---
## Same-Origin Policy

This is a *security measure* that restricts how resources on a web page can interact with resources from another origin. 

**By default, web pages can only make requests to the same domain that served the web page.**

## **Preflight Requests**

Before making certain types of requests, browsers send an HTTP `OPTIONS` request to the server to check if the actual request is safe. 
This preflight request asks the server if it allows the actual request method and headers.

## Cross-Origin Resource Sharing (CORS)

**CORS** is a security feature implemented in web browsers to control how resources on a web page can be requested from *another domain* outside *the domain from which the resource originated*.
It is a *mechanism* that allows servers to specify who can access their assets and how the assets can be accessed.

### CORS Headers

#### `Access-Control-Allow-Origin`

Specifies which origins are allowed to access the resource. For example, `Access-Control-Allow-Origin: *` allows access from any origin, while `Access-Control-Allow-Origin: https://example.com` restricts access to only that domain.

#### `Access-Control-Allow-Methods`

Lists the HTTP methods (e.g., `GET`, `POST`, `PUT`) that are allowed when accessing the resource.

#### `Access-Control-Allow-Headers`

Lists the headers that can be used when making the actual request.

#### `Access-Control-Allow-Credentials`

Indicates whether the response can be exposed when the credentials flag is true.

#### `Access-Control-Max-Age`

Specifies how long the results of a preflight request can be cached.

### Preflight `OPTION` Service Response

```http
OPTIONS /resource
Host: api.example.com
Origin: https://mywebsite.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-Custom-Header

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://mywebsite.com
Access-Control-Allow-Methods: POST
Access-Control-Allow-Headers: X-Custom-Header
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 86400
```