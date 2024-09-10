## What are the components of the HTTP protocol?

The HTTP (Hypertext Transfer Protocol) protocol is a foundation of web communication, and its components can be categorized into several key areas:

### 1. **HTTP Methods**
   - **GET**: Requests data from a specified resource. It is used to retrieve information.
   - **POST**: Submits data to be processed to a specified resource, often resulting in a change in state or side effects.
   - **PUT**: Updates a specified resource with new data.
   - **DELETE**: Deletes a specified resource.
   - **HEAD**: Similar to GET but only requests the headers of a resource, not the actual content.
   - **OPTIONS**: Describes the communication options for the target resource.
   - **PATCH**: Applies partial modifications to a resource.

### 2. **HTTP Headers**
   - **Request Headers**: Include metadata about the request, such as `Accept` (what media types are acceptable), `User-Agent` (information about the client), and `Authorization` (credentials for authentication).
   - **Response Headers**: Provide information about the server's response, such as `Content-Type` (type of the returned data), `Content-Length` (length of the returned data), and `Set-Cookie` (cookie information).
   - **General Headers**: Applied to both requests and responses, like `Cache-Control` (caching policies) and `Connection` (control options for the current connection).

### 3. **HTTP Status Codes**
   - **1xx (Informational)**: Indicate that the request has been received and is being processed (e.g., `100 Continue`).
   - **2xx (Success)**: Indicate that the request was successfully received, understood, and accepted (e.g., `200 OK`, `201 Created`).
   - **3xx (Redirection)**: Indicate that further action is needed to fulfill the request (e.g., `301 Moved Permanently`, `302 Found`).
   - **4xx (Client Error)**: Indicate that the client made an error (e.g., `400 Bad Request`, `404 Not Found`).
   - **5xx (Server Error)**: Indicate that the server failed to fulfill a valid request (e.g., `500 Internal Server Error`, `502 Bad Gateway`).

### 4. **HTTP Versions**
   - **HTTP/1.0**: The original version, which introduced basic features for request and response.
   - **HTTP/1.1**: Improved version with persistent connections, chunked transfer encoding, and additional methods.
   - **HTTP/2**: Introduced multiplexing, header compression, and binary framing to improve performance.
   - **HTTP/3**: Built on QUIC, which provides improvements in latency and security.

### 5. **Request and Response Format**
   - **Request Line**: Contains the HTTP method, the resource URI, and the HTTP version (e.g., `GET /index.html HTTP/1.1`).
   - **Response Line**: Includes the HTTP version, status code, and a textual description (e.g., `HTTP/1.1 200 OK`).
   - **Body**: Contains the actual data being sent in the request or response, such as HTML content, JSON, or files.

These components work together to enable the transfer of information between clients (like web browsers) and servers over the web.


## What happens when you type google.com into your browser’s address bar and press enter?

When you type `google.com` into your browser’s address bar and press Enter, several steps take place to retrieve and display the Google homepage. Here's a simplified overview of the process:

### 1. **URL Parsing**
   - **Browser Processes URL**: The browser parses `google.com` to determine that it should make a request to the Google web server. Since no protocol (like `http://` or `https://`) is specified, the browser defaults to `https://`.

### 2. **DNS Resolution**
   - **Query DNS Server**: The browser needs to convert the domain name `google.com` into an IP address. It sends a query to a DNS (Domain Name System) server to find out the IP address associated with `google.com`.
   - **DNS Lookup**: The DNS server responds with the IP address of Google's servers. This address allows the browser to locate and communicate with Google’s web server.

### 3. **Establishing a Connection**
   - **TCP Connection**: The browser establishes a TCP (Transmission Control Protocol) connection with the Google server using the IP address obtained. This involves a three-way handshake to ensure a reliable connection.
   - **TLS Handshake (if using HTTPS)**: If the URL is `https://`, the browser and server perform a TLS (Transport Layer Security) handshake to establish a secure connection. This involves negotiating encryption methods and exchanging encryption keys.

### 4. **Sending the HTTP Request**
   - **Request Formation**: The browser sends an HTTP request to the Google server. This request includes a line with the HTTP method (GET), the requested resource (in this case, the root `/`), and the HTTP version (e.g., `HTTP/1.1`).
   - **Request Headers**: The request also includes headers such as `Host` (specifying `google.com`), `User-Agent` (information about the browser), and others.

### 5. **Server Processing**
   - **Request Handling**: The Google server receives the request, processes it, and generates a response. This involves retrieving the appropriate content and preparing it for delivery.
   - **Response Generation**: The server creates an HTTP response that includes a status code (e.g., `200 OK`), response headers, and the body of the response (the HTML content of Google's homepage).

### 6. **Receiving the Response**
   - **Response Transmission**: The server sends the HTTP response back to the browser over the established TCP connection. If the response is large or includes multiple resources (like images, CSS, and JavaScript), these may be sent in multiple chunks or subsequent requests.

### 7. **Rendering the Page**
   - **Parsing HTML**: The browser receives the HTML content and begins parsing it. It constructs the DOM (Document Object Model) tree based on the HTML.
   - **Loading Resources**: The browser identifies additional resources referenced in the HTML (like CSS stylesheets, JavaScript files, images) and makes additional HTTP requests to fetch these resources.
   - **Rendering**: The browser applies CSS styles, executes JavaScript, and assembles the page content into a visual representation. This is then displayed on your screen.

### 8. **Interactive Elements**
   - **JavaScript Execution**: JavaScript code on the page may further modify the content, handle user interactions, and make additional network requests (AJAX calls) to fetch more data or interact with the server.

Throughout this process, various optimizations and caching mechanisms might come into play to speed up the loading of the page and reduce network traffic.


## REST API – knowledge about the concept, pros, and cons.
What does REST mean? How do REST APIs work?

### What Does REST Mean?

REST stands for **Representational State Transfer**. It is an architectural style for designing networked applications and is often used in the context of web services. RESTful APIs (or REST APIs) are designed based on REST principles.

### Core Principles of REST

1. **Stateless**: Each request from a client to a server must contain all the information needed to understand and process the request. The server should not store any client context between requests.

2. **Client-Server Architecture**: The client and server operate independently, and the client only interacts with the server through requests and responses. This separation of concerns allows for greater scalability and flexibility.

3. **Uniform Interface**: REST APIs use a standardized set of operations (typically HTTP methods) and resources (identified by URIs). This uniformity simplifies the interaction between clients and servers.

4. **Resource-Based**: Resources (such as users, articles, or products) are identified by URIs. Each resource can be represented in multiple formats (e.g., JSON, XML).

5. **Stateless Communication**: Each request from a client to the server must contain all the information needed to understand and process the request. The server does not store any state information about the client between requests.

6. **Cacheable**: Responses from the server can be explicitly marked as cacheable or non-cacheable, which can improve performance and reduce the need for repetitive processing.

7. **Layered System**: A REST API can be composed of multiple layers (e.g., security layers, load balancers) that work together to handle requests and responses. Each layer should only interact with the adjacent layers.

### How Do REST APIs Work?

1. **Resource Identification**:
   - Resources are identified using URIs (Uniform Resource Identifiers). For example, a REST API might use a URI like `/users/123` to represent a specific user.

2. **HTTP Methods**:
   - **GET**: Retrieve information about a resource.
   - **POST**: Create a new resource.
   - **PUT**: Update an existing resource.
   - **DELETE**: Remove a resource.
   - **PATCH**: Apply partial updates to a resource.

3. **Request and Response**:
   - **Request**: A client sends an HTTP request to a server. This request includes a method, a URI, headers, and potentially a body.
   - **Response**: The server processes the request and returns an HTTP response, which includes a status code, headers, and a body containing the resource representation.

4. **Data Formats**:
   - Data is typically exchanged in formats such as JSON (JavaScript Object Notation) or XML (eXtensible Markup Language). JSON is more common due to its simplicity and compatibility with JavaScript.

5. **Stateless Communication**:
   - Each request is independent and contains all necessary information. The server does not rely on or maintain any session state between requests.

### Pros of REST APIs

1. **Scalability**: REST's stateless nature and client-server separation allow for easier scaling and load balancing.

2. **Flexibility**: REST APIs support multiple data formats (e.g., JSON, XML) and are not tied to a specific protocol, though HTTP is commonly used.

3. **Simplicity**: REST is based on standard HTTP methods, making it easier to understand and implement. The uniform interface simplifies interactions between clients and servers.

4. **Performance**: Stateless communication can lead to improved performance and responsiveness. Caching mechanisms can also enhance performance by reducing the need to repeatedly process the same requests.

5. **Ease of Integration**: REST APIs are widely supported and can be integrated with a variety of platforms and languages.

### Cons of REST APIs

1. **Statelessness Limitations**: While statelessness simplifies the server design, it can lead to inefficiencies if the client needs to repeatedly send redundant information.

2. **Overhead**: HTTP headers and payloads can introduce overhead, especially if the data format is verbose or if many resources are requested at once.

3. **Limited to HTTP**: REST APIs typically use HTTP, which means they are subject to the limitations and constraints of the HTTP protocol.

4. **Complex Data Relationships**: REST can become cumbersome when dealing with complex relationships between resources. Operations that involve multiple steps or transactions can be challenging to manage.

5. **Versioning Challenges**: Evolving a REST API over time while maintaining backward compatibility can be complex. Different strategies (e.g., URL versioning, header versioning) need to be considered.

Overall, REST APIs are a popular choice for web services due to their simplicity, scalability, and flexibility. However, they may not be suitable for all scenarios, and understanding their strengths and limitations can help in designing effective systems.

## What is an API contract?

An API contract is a formal agreement that specifies how different systems or components interact through an Application Programming Interface (API). It defines the rules, expectations, and constraints for how API requests and responses should be structured and processed. Here are the key components of an API contract:

1. **Endpoints**: Defines the URIs or paths where the API can be accessed, along with the methods (e.g., GET, POST, PUT, DELETE) that are supported at each endpoint.

2. **Request and Response Formats**: Specifies the format and structure of requests and responses. This includes data types, required fields, optional fields, and the overall schema for request bodies and response payloads.

3. **HTTP Methods**: Details which HTTP methods are allowed for each endpoint (e.g., GET for fetching data, POST for creating new records).

4. **Authentication and Authorization**: Outlines the methods and requirements for authentication (e.g., API keys, OAuth tokens) and authorization to ensure that only permitted users can access certain functionalities.

5. **Status Codes**: Describes the HTTP status codes that the API will return to indicate the result of a request (e.g., 200 for success, 404 for not found, 500 for server error).

6. **Error Handling**: Defines how errors should be communicated back to the client, including the format and content of error messages.

7. **Rate Limiting and Throttling**: Specifies any limits on how frequently the API can be accessed and the actions that will be taken if these limits are exceeded.

8. **Versioning**: Outlines how different versions of the API are handled, allowing clients to specify which version they are using and ensuring compatibility across versions.

9. **Examples**: Provides sample requests and responses to illustrate how the API should be used and what clients can expect.

10. **Contract Testing**: Sometimes, the API contract is used as a basis for testing to ensure that the API implementation adheres to the agreed-upon specifications and behaves correctly in different scenarios.

In essence, the API contract acts as a blueprint for both API developers and consumers, ensuring that there is a clear, mutual understanding of how interactions should occur, which helps prevent misunderstandings and integration issues.