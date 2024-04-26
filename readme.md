# HTTP

To understand the HTTP verbs and methods, let's go back to the start of the HTTP protocol. 

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

