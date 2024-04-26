# HTTP

If you want to know more widely about HTTP in video format, and the context of the WWW, check out [this excellent video](https://www.youtube.com/watch?v=wW2A5SZ3GkI).

To understand the HTTP verbs and methods, let's go back to the start of the HTTP protocol. 

<!-- TOC -->

- [HTTP](#http)
    - [HTTP History and Purpose](#http-history-and-purpose)
        - [Evolution of HTTP](#evolution-of-http)
        - [Purpose of HTTP](#purpose-of-http)
    - [Request/Response Model](#requestresponse-model)
        - [Request Components](#request-components)
        - [Response Components](#response-components)
        - [Example](#example)
            - [Request](#request)
            - [Response](#response)
    - [Methods](#methods)
        - [Idempotence](#idempotence)
    - [Cheat Sheet](#cheat-sheet)
    - [HTTP Status Codes](#http-status-codes)
        - [Status Code Classes](#status-code-classes)
        - [Common Status Codes](#common-status-codes)

<!-- /TOC -->

## HTTP History and Purpose

HTTP, or *Hypertext Transfer Protocol*, is the foundation of data communication on the World Wide Web. It's an application-layer protocol that facilitates the transfer of hypermedia documents, such as HTML pages, images, and other resources, between *clients and servers*.

### Evolution of HTTP

- **HTTP/0.9**: The initial version of HTTP, introduced in 1991 by Tim Berners-Lee. It supported only the GET method and had a simple request/response model.
- **HTTP/1.0**: Developed in 1996, this version introduced additional methods like POST, HEAD, and PUT, along with status codes and headers for more complex interactions.
- **HTTP/1.1**: Released in 1997, it brought improvements in performance, caching, persistent connections, and support for various media types. It's still widely used today.
- **HTTP/2**: Introduced in 2015, it focused on performance enhancements such as multiplexing, header compression, and server push.
- **HTTP/3**: Currently under development, HTTP/3 aims to improve performance further by using the QUIC transport protocol over UDP.

### Purpose of HTTP

HTTP serves as the foundation for communication between clients (such as web browsers or mobile apps) and servers. Its primary purpose is to facilitate the transfer of resources, enabling users to access web pages, download files, submit forms, and interact with web applications.

## Request/Response Model

HTTP follows a request/response model, where clients send requests to servers, and servers respond with corresponding responses.

![alt text](images/request-response.png)

### Request Components

- **Method**: Specifies the action to be performed (e.g., GET, POST, PUT, DELETE).
- **URL**: Identifies the resource being requested.
- **Headers**: Provide additional information about the request, such as the user agent, content type, and cookies.
- **Body**: Contains optional data sent with the request, typically used in POST or PUT requests.

### Response Components

- **Status Code**: Indicates the outcome of the request (e.g., 200 for success, 404 for not found, 500 for server error).
- **Headers**: Similar to request headers, but contain metadata about the response.
- **Body**: Contains the requested resource or additional information, such as error messages.

### Example

#### Request

The client sends a `GET` request for the `index.html` page to `www.example.com`:

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
```

#### Response

The server responds with a 200 OK status code along with the HTML content of the page:

```
HTTP/1.1 200 OK
Date: Mon, 26 Apr 2024 12:00:00 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 1234

<!DOCTYPE html>
<html>
<head>
  <title>Example Page</title>
</head>
<body>
  <h1>Welcome to Example Page</h1>
  <!-- Content goes here -->
</body>
</html>
```

## Methods

When HTTP began, it defined only three methods, which are still relevant today in HTTP 1.0:

- **GET**: Fetches resources from a server. For example, requesting web pages or downloading files.
- **POST**: Sends data to the server, typically for processing or updating resources.
- **HEAD**: Retrieves only the headers from a resource on the server, useful for checking metadata like creation date or size.

With the introduction of HTTP 1.1, several new methods emerged, including two significant methods:
- **PUT**: Completely replaces or creates a resource on the server by sending all the data describing it.
- **DELETE**: Deletes the resource specified by the URL.

These methods are distinct from CRUD operations:
- **GET** retrieves resources.
- **PUT** and **DELETE** replace and delete resources, respectively.
- **POST** can create, update, or sometimes delete resources.
- **PATCH** is similar to **PUT** but updates specific fields without sending the entire resource representation.

### Idempotence

Each HTTP method has a property called "idempotence".

"Idempotent" refers to the property of a method where multiple identical requests have the same effect as a single request. In other words, if you perform an idempotent operation multiple times, *the result remains the same as if you had performed it only once*.

**GET**, **TRACE**, **OPTIONS**, and **HEAD** are inherently idempotent. However, **PUT** and **DELETE** must be idempotent. **POST** and **PATCH** don't require idempotence.

As an example of an idempotent operation, we can think of deleting a subscription, where invoking it multiple times doesn't change the server's state. In contrast, a non-idempotent operation like increasing a salary will have different outcomes with each invocation.

## Cheat Sheet

Got all that? Well, good news, the most common operations are analogous to CRUD (Create, Read, Update, Delete), so here's a handy table:

| HTTP Method | CRUD | Explanation                                   |
|-------------|------|-----------------------------------------------|
| POST        | Create | Submits data to be processed by a server. Typically used to create new resources or perform actions that change server state. |
| GET         | Read | Retrieves data from a server without altering it. It is used to retrieve resources identified by a URL. |
| PUT         | Update/Replace | Updates or replaces a resource on the server with the provided data. If the resource doesn't exist, it may create a new one. |
| DELETE      | Delete | Removes a resource identified by the specified URL from the server. It deletes the resource permanently. |

---

## HTTP Status Codes

HTTP status codes are three-digit numbers returned by a server in response to a client's request made to the server. They provide information about the outcome of the request and any actions that need to be taken.

### Status Code Classes

Status codes are grouped into the following classes:

- **1xx Informational**: Request received, continuing process.
- **2xx Success**: The action was successfully received, understood, and accepted.
- **3xx Redirection**: Further action must be taken to complete the request.
- **4xx Client Error**: The request contains bad syntax or cannot be fulfilled.
- **5xx Server Error**: The server failed to fulfill a seemingly valid request.

### Common Status Codes

| Code | Name | Description |
|------|------|-------------|
| 200  | OK | The request has succeeded. |
| 201  | Created | The request has been fulfilled, and a new resource has been created. |
| 204  | No Content | The server successfully processed the request but does not need to return any content. |
| 301  | Moved Permanently | The requested resource has been permanently moved to a new location. |
| 400  | Bad Request | The server cannot process the request due to client error (e.g., malformed syntax). |
| 401  | Unauthorized | The request requires user authentication. |
| 404  | Not Found | The requested resource could not be found on the server. |
| 500  | Internal Server Error | A generic server error message when no specific error message is suitable. |

### How are they used by the client?

By receiving and interpreting status codes, the client can handle failures gracefully. 

1. **Error Handling** When the server encounters an error (e.g., 404 Not Found, 500 Internal Server Error), it communicates this to the client through the appropriate status code. The client can then display a user-friendly error message or take alternative actions to mitigate the issue.
2. **Retries** In some cases, the client may attempt to retry the request if it receives a temporary error (e.g., 503 Service Unavailable). By understanding the status code, the client can determine whether it's appropriate to retry the request and how many times to retry.
3. **Redirects** If the server needs the client to navigate to a different URL (e.g., due to a resource being moved), it can issue a redirect status code (e.g., 301 Moved Permanently, 302 Found). The client can then automatically follow the redirect to the new URL.
4. **Authentication Challenges** If the server requires authentication for a particular resource, it can return a 401 Unauthorized status code. The client can then prompt the user to provide credentials or handle the authentication challenge in an appropriate manner.