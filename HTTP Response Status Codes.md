> Source: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

## \[`100` - `199`\] Informational Responses

### `100` Continue

This interim response indicates that the client should continue the request or ignore the response if the request is already finished.

## \[`200` - `299`\] Successful Responses

### `200` OK

The request succeeded. The result meaning of "success" depends on the HTTP method:

- `GET`: The resource has been fetched and transmitted in the message body.
- `HEAD`: The representation headers are included in the response without any message body.
- `PUT` or `POST`: The resource describing the result of the action is transmitted in the message body.
- `TRACE`: The message body contains the request message as received by the server.

## \[`300` - `399`\] Redirection Responses

### `301` Moved Permanently

The URL of the requested resource has been changed permanently. The new URL is given in the response.

### `302` Found

This response code means that the URI of requested resource has been changed *temporarily*. Further changes in the URI might be made in the future. Therefore, this same URI should be used by the client in future requests.

## \[`400` - `499`\] Client Error Responses

### `400` Bad Request

The server cannot or will not process the request due to something that is perceived to be a client error (e.g., malformed request syntax, invalid request message framing, or deceptive request routing).

### `401` Unauthorized

^962a49

Although the HTTP standard specifies "unauthorized", semantically this response means "unauthenticated". That is, the client must authenticate itself to get the requested response.

### `403` Forbidden

The client does not have access rights to the content; that is, it is unauthorized, so the server is refusing to give the requested resource. Unlike **401 Unauthorized**, the client's identity is known to the server.

### `404` Not Found

The server cannot find the requested resource. In the browser, this means the URL is not recognized. In an API, this can also mean that the endpoint is valid but the resource itself does not exist. Servers may also send this response instead of **403 Forbidden** to hide the existence of a resource from an unauthorized client. This response code is probably the most well known due to its frequent occurrence on the web.

## \[`500` - `599`\] Server Error Responses

### `500` Internal Server Error

The server has encountered a situation it does not know how to handle.

### `501` Not Implemented

The request method is not supported by the server and cannot be handled. The only methods that servers are required to support (and therefore that must not return this code) are `GET` and `HEAD`.

### `502` Bad Gateway

This error response means that the server, while working as a gateway to get a response needed to handle the request, got an invalid response.

### `503` Service Unavailable

The server is not ready to handle the request. Common causes are a server that is down for maintenance or that is overloaded. Note that together with this response, a user-friendly page explaining the problem should be sent. This response should be used for temporary conditions and the `Retry-After` HTTP header should, if possible, contain the estimated time before the recovery of the service. The webmaster must also take care about the caching-related headers that are sent along with this response, as these temporary condition responses should usually not be cached.

### `504` Gateway Timeout

This error response is given when the server is acting as a gateway and cannot get a response in time.
