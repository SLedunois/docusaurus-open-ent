---
title: rest
id: rest
---
ODE Framework offers, on top of Vertx3, an "annotation API" to implement a REST API.
It makes it possible to map a controller method with a path (a route) by annotation.
There are two ideas behind that approach :

-   provide a descriptive style at code time (that reminds JAX-RS for Java developers)

-   keep asynchronous vertx3 execution at runtime

> **Note**
>
> With ODE annotations you don’t need to manage a vertx3 RouteMatcher.
> The URL path format follows the verxt3 one (for parameter extraction, pattern matching …​)
> . See [Vert3 manual](http://vertx.io./)

# HTTP method

> **Note**
>
> Annotations are shipped in the `import fr.wseduc.rs` package.

## GET

    @Get("/group/:groupId")
    public void delete(final HttpServerRequest request) {
        String groupId = request.params().get("groupId");
    }

## DELETE

    @Delete("/group/:groupId")
    public void delete(final HttpServerRequest request) {
        String groupId = request.params().get("groupId");
    }

## PUT

    @Put("/group/:groupId")
    public void update(final HttpServerRequest request) {
        bodyToJson(request, new Handler<JsonObject>() {
            @Override
            public void handle(JsonObject body) {
                // modification's stuff with the body object
            }
        });
    }

> **Note**
>
> `bodyToJson` is a static method provided by `fr.wseduc.webutils.request.RequestUtils`.
> It wraps vertx3 `request.bodyHandler` in order to strip common XSS pattern from the request body.

## POST

    @Post("/group/:groupId")
    public void create(final HttpServerRequest request) {
        bodyToJson(request, new Handler<JsonObject>() {
            @Override
            public void handle(JsonObject body) {
                // creation's stuff with the body object
            }
        });
    }

# HTTP Response

According to REST best practice and [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt), ODE framework offers multiple HTTP responses. All responses are provided by `fr.wseduc.webutils.http.Renders` and available in `ControllerHelper` class.

## 2xx Success response

### 200 OK

The request has succeeded. It ends the request with a default `200` status code. However, a `renderJson` alternative method allows rendering `JSON` with a `200` status code.

    void ok(HttpServerRequest request)

    void renderJson(HttpServerRequest request, JsonObject jo)
    void renderJson(HttpServerRequest request, JsonArray jo)

### 201 Created

The request has been fulfilled and resulted in a new resource being created. It ends the request and returns a `201` status code with `Created` message.

    void created(HttpServerRequest request)

### 204 No Content

The server has fulfilled the request but does not need to return an entity-body. It ends the request and returns a `204` status code and `No Content` message.

    void noContent(HttpServerRequest request)

## 3xx Redirection

### 301 Moved Permanently

The requested resource has been assigned a new permanent URI and any future references toe the resource should use the returned URI. It redirect the request to the new URI, returns a `301` status code and set `Location` to the new URI.

    void redirectPermanent(HttpServerRequest request, String location)
    void redirectPermanent(HttpServerRequest request, String host, String location)

### 302 Found

The requested resource resides temporarily under a different URI. This method can be used to redirect the request to an internal or external resource. It ends the request with a `302` status code and `Location` header matching the new URI.

    void redirect(HttpServerRequest request, String location)
    void redirect(HttpServerRequest request, String host, String location)

### 304 Not Modified

If the client has performed a conditional `GET` request and access is allowed, but the document has not been modified, the server should respond with this status code. It ends the request with `304` status code and `Not Modified` message. However, you can add an optional resource identifier.

    void notModified(HttpServerRequest request)
    void notModified(HttpServerRequest request, String fileId)

## 4xx Client Error

### 400 Bad Request

The request could not be understood by the server due to malformed syntax. It ends the request with a `400` status code and `Bad Request` message. However, you can set an optional message error.

    void badRequest(HttpServerRequest request)
    void badRequest(HttpServerRequest request, String message)

### 401 Unauthorized

The request requires user authentication. It ends the request with a `401` status code and `Unauthorized` message. However, you can set an optional message error.

    void unauthorized(HttpServerRequest request)
    void unauthorized(HttpServerRequest request, String message)

### 403 Forbidden

The server understood the request, but is refusing to fulfill it due to permission lack. It end the request with a `403` status code and `Forbidden` message. However, you can set an optional message error.

    void forbidden(HttpServerRequest request)
    void forbidden(HttpServerRequest request, String message)

### 404 Not Found

The server has not found anything match the Request-URI. It ends the request with a `404` status code and `Not Found` message. However, you can add an optional error message.

    void notFound(HttpServerRequest request)
    void notFound(HttpServerRequest request, String message)

### 409 Conflict

The request could not be completed due to a conflict with the current state of the resource. It ends the request with a `409` status code and `Conflict` message. However, you can add an optional error message.

    void conflict(HttpServerRequest request)
    void conflict(HttpServerRequest request, String message)

## 5xx Server Error

### 500 Internal Server Error

The server encountered an unexpected condition which prevented it form fulfilling the request. It ends the request with a `500` status code and `Internal Server Error` message. However, you can add an optional `JSON object`.

    void renderError(HttpServerRequest request)
    void renderError(HttpServerRequest request, JsonObject error)
