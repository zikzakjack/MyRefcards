# OpenAPI (API Design and Documentation)

## References

1. [The OpenAPI Initiative](https://www.openapis.org/)
2. [The OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification)
3. [https://swagger.io/](https://swagger.io/)
4. [OpenAPI 3.0 Tutorial](https://support.smartbear.com/swaggerhub/docs/tutorials/openapi-3-tutorial.html)
5. [yaml](https://yaml.org/)
6. [yaml Crash Course](https://learnxinyminutes.com/docs/yaml/)
7. [Online YAML Validator](http://www.yamllint.com/)

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

# OpenAPI Overview

From the [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification):

> The OpenAPI Specification (OAS) defines a standard, programming language-agnostic interface description for HTTP APIs, which allows both humans and computers to discover and understand the capabilities of a service without requiring access to source code, additional documentation, or inspection of network traffic. When properly defined via OpenAPI, a consumer can understand and interact with the remote service with a minimal amount of implementation logic. Similar to what interface descriptions have done for lower-level programming, the OpenAPI Specification removes guesswork in calling a service.

> An OpenAPI definition can then be used by documentation generation tools to display the API, code generation tools to generate servers and clients in various programming languages, testing tools, and many other use cases.

# OpenAPI Schema

# OpenAPI Components

# OpenAPI Parameters

# OpenAPI Requests

# OpenAPI Security Definitions

# OpenAPI CodeGen

# OpenAPI Tools

# OpenAPI Spring Integration
