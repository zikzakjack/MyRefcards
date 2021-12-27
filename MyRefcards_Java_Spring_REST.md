# MyRefcards_Java_Spring_REST

## References

3. [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
3. [HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
3. [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
3. [HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
3. [Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
3. [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
1. [List of HTTP header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
2. [List of HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

# HTTP

## HTTP Request Methods

HTTP Method | Operation | Comment
----------- | ------------- | --------------------------------------------------------------------
GET | Read Operation only | Uses only for the read operation.GET should be idempotent
POST |Create new resource | Should only be used to create a new resource
PUT | Update / Replace Resource | Update an existing resource.Think of PUT method as putting a resource
DELETE | Delete Resource | To remove a given resource.DELETE operation is idempotent
PATCH | Partial Update / Modify | Partial update to a resource should happen through PATCH
HEAD | |  
OPTIONS | |  
TRACE | |  
 
- status codes
- idempotent
- method cheatsheet

## HTTP Status Codes

- 100 series are informational in nature
- 200 series indicate successful request
- 300 series are redirections
- 400 series are client errors
- 500 series are server side errors

## Common HTTP Status Codes
- 200 OK
- 201 CREATED
- 204 ACCEPTED
- 301 MOVED PERMANENTLY
- 400 BAD REQUEST
- 401 NOT AUTHORIZED
- 404 NOT FOUND
- 500 INTERNAL SERVER ERROR
- 503 SERVICE UNAVAILABLE
