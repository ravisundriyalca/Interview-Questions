# Interview-Questions
 
 ## List Of Interview Questions
- [explain how a web request to amazon.com works and is served?](#workflow)
- [Explain REST request lifecycle](#restflow)
- [Explain Cookies in HTTP request ](#cookies)

## Workflow

When you type **`https://www.amazon.com`** into your browser and hit Enter, a complex series of steps takes place behind the scenes to serve you the Amazon website. Here's a detailed explanation of how a web request to Amazon.com works and is served:



![image](https://github.com/user-attachments/assets/6d675282-10a3-4595-953d-4495f1b6beaa)

---

## **1. DNS Resolution**
1. **Browser Cache**: The browser first checks its cache to see if it already knows the IP address for `www.amazon.com`.
2. **OS Cache**: If not found, the browser asks the operating system for the IP address.
3. **Router Cache**: If the OS doesn't know, the request is sent to your router.
4. **ISP DNS Server**: If the router doesn't have the information, the request is forwarded to your Internet Service Provider's (ISP) DNS server.
5. **Recursive DNS Lookup**: If the ISP's DNS server doesn't have the IP address, it performs a recursive lookup:
   - It queries the **root DNS servers** to find the authoritative DNS server for `.com`.
   - It then queries the `.com` authoritative server to find the DNS server for `amazon.com`.
   - Finally, it queries Amazon's DNS server to get the IP address for `www.amazon.com`.
6. The IP address is returned to your browser.

---

## **2. Establishing a Connection (TCP Handshake)**
1. **TCP Handshake**: Your browser initiates a **TCP (Transmission Control Protocol)** connection with Amazon's server using the IP address obtained.
   - **SYN**: Your browser sends a SYN (synchronize) packet to the server.
   - **SYN-ACK**: The server responds with a SYN-ACK (synchronize-acknowledge) packet.
   - **ACK**: Your browser sends an ACK (acknowledge) packet to confirm the connection.
2. **TLS/SSL Handshake**: Since the request is over HTTPS, a **TLS (Transport Layer Security)** handshake occurs to establish a secure connection:
   - Your browser and Amazon's server agree on encryption protocols.
   - The server sends its SSL certificate, which your browser verifies.
   - A symmetric encryption key is exchanged for secure communication.

---

## **3. Sending the HTTP Request**
1. **HTTP Request**: Your browser sends an **HTTP GET request** to Amazon's server, asking for the content of `https://www.amazon.com`.
   - The request includes headers like `User-Agent`, `Accept-Language`, and `Cookies`.
2. **Load Balancer**: The request first reaches Amazon's **load balancer**, which distributes the request to one of many backend servers based on factors like server load and geographic location.

---

## **4. Processing the Request on Amazon's Server**
1. **Web Server**: The request is handled by a **web server** (e.g., Apache, Nginx, or Amazon's custom server).
2. **Application Server**: The web server forwards the request to an **application server**, which runs the business logic of Amazon's website.
3. **Database Queries**: The application server may query **databases** (e.g., product information, user data) to fetch relevant data.
4. **Caching**: Amazon uses **caching systems** (e.g., Redis, Memcached) to serve frequently accessed data quickly.
5. **Content Generation**: The application server generates the HTML, CSS, and JavaScript for the webpage.

---

## **5. Serving the Response**
1. **HTTP Response**: The server sends an **HTTP response** back to your browser, including:
   - **Status code** (e.g., 200 OK).
   - **Headers** (e.g., `Content-Type`, `Cache-Control`).
   - **Body** (the HTML, CSS, and JavaScript content).
2. **CDN (Content Delivery Network)**: Static assets like images, CSS, and JavaScript files are often served from a **CDN** (e.g., Amazon CloudFront) to reduce latency and improve load times.

---

## **6. Rendering the Webpage**
1. **HTML Parsing**: Your browser parses the HTML to construct the **DOM (Document Object Model)**.
2. **CSS Parsing**: The browser parses the CSS to construct the **CSSOM (CSS Object Model)**.
3. **JavaScript Execution**: The browser executes any JavaScript code, which may modify the DOM or fetch additional data (e.g., product recommendations).
4. **Rendering**: The browser combines the DOM and CSSOM to create the **render tree** and displays the webpage on your screen.

---

## **7. Additional Requests**
1. **AJAX Requests**: After the initial page load, your browser may send additional **AJAX requests** to fetch dynamic content (e.g., product reviews, recommendations).
2. **WebSocket Connections**: For real-time updates (e.g., chat, notifications), your browser may establish a **WebSocket connection** with Amazon's server.

---

## **8. Monitoring and Analytics**
1. **Logging**: Amazon logs the request for monitoring, debugging, and analytics.
2. **Analytics**: Data about your visit (e.g., pages viewed, time spent) is collected for improving the user experience and personalizing content.

---

## **Key Technologies Involved**
- **DNS**: Domain Name System for resolving domain names to IP addresses.
- **TCP/IP**: Transmission Control Protocol/Internet Protocol for reliable communication.
- **TLS/SSL**: Transport Layer Security/Secure Sockets Layer for encryption.
- **HTTP/HTTPS**: Hypertext Transfer Protocol (Secure) for web communication.
- **Load Balancers**: Distribute traffic across multiple servers.
- **CDN**: Content Delivery Network for serving static assets.
- **Databases**: Store and retrieve data (e.g., product information, user data).
- **Caching**: Improve performance by serving frequently accessed data quickly.
- **JavaScript**: Adds interactivity and dynamic content to the webpage.

---

By following these steps, your browser successfully retrieves and displays the Amazon.com webpage. This process happens in milliseconds.



## Restflow

# A Capable RESTFul Backend
![image](https://github.com/user-attachments/assets/d417a9ae-21c9-40c2-9872-591d4014b995)

The **REST (Representational State Transfer) request lifecycle** describes the sequence of steps that occur when a client (e.g., a browser or mobile app) sends a request to a RESTful API and receives a response. REST is an architectural style for designing networked applications, and it relies on **HTTP** as the communication protocol. Below is a detailed explanation of the REST request lifecycle:

---

## **1. Client Sends an HTTP Request**
- The client initiates the process by sending an **HTTP request** to the server.
- The request includes:
  - **HTTP Method**: Specifies the action to be performed (e.g., `GET`, `POST`, `PUT`, `DELETE`).
  - **Endpoint (URL)**: The address of the resource (e.g., `https://api.example.com/users`).
  - **Headers**: Metadata about the request (e.g., `Content-Type`, `Authorization`).
  - **Body (Optional)**: Data sent to the server (e.g., JSON or form data for `POST` or `PUT` requests).

**Example Request**:
```http
GET /users/123 HTTP/1.1
Host: api.example.com
Authorization: Bearer <token>
Accept: application/json
```

---

## **2. Server Receives the Request**
- The server receives the HTTP request and processes it.
- The server identifies:
  - The **resource** being requested (e.g., `/users/123`).
  - The **HTTP method** (e.g., `GET`).
  - The **headers** and **body** (if present).

---

## **3. Routing and Controller Handling**
- The server uses a **router** to map the request to the appropriate **controller** or handler.
- The controller is responsible for processing the request and generating a response.

**Example**:
- A `GET /users/123` request might be routed to a `UserController` with a `getUser` method.

---

## **4. Business Logic Execution**
- The controller executes the **business logic** required to fulfill the request.
- This may involve:
  - Querying a database.
  - Calling other services or APIs.
  - Performing calculations or validations.

**Example**:
- The `getUser` method queries the database for the user with ID `123`.

---

## **5. Data Access Layer (Optional)**
- If the request involves data retrieval or manipulation, the server interacts with the **data access layer** (e.g., a database).
- The data access layer performs operations like:
  - Fetching data (`SELECT` queries for `GET` requests).
  - Inserting or updating data (`INSERT` or `UPDATE` queries for `POST` or `PUT` requests).
  - Deleting data (`DELETE` queries for `DELETE` requests).

---

## **6. Response Generation**
- Once the business logic is executed, the server generates an **HTTP response**.
- The response includes:
  - **Status Code**: Indicates the result of the request (e.g., `200 OK`, `404 Not Found`).
  - **Headers**: Metadata about the response (e.g., `Content-Type`).
  - **Body (Optional)**: Data returned to the client (e.g., JSON, XML, or HTML).

**Example Response**:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

---

## **7. Client Receives the Response**
- The client receives the HTTP response and processes it.
- The client may:
  - Display the data (e.g., render a webpage or update a mobile app UI).
  - Handle errors (e.g., show an error message for a `404 Not Found` response).

---

## **8. Client-Side Rendering or Processing**
- If the response contains data (e.g., JSON), the client may:
  - Parse the data and update the user interface.
  - Store the data locally (e.g., in a browser cache or local storage).
  - Trigger additional requests (e.g., fetch related resources).

---

## **Key Components of the REST Request Lifecycle**
1. **Client**: Initiates the request and processes the response.
2. **Server**: Handles the request, executes business logic, and generates the response.
3. **HTTP**: The protocol used for communication between the client and server.
4. **Resource**: The entity being accessed or manipulated (e.g., a user, product, or order).
5. **Endpoint**: The URL that identifies the resource.
6. **HTTP Methods**: Define the action to be performed (e.g., `GET`, `POST`, `PUT`, `DELETE`).
7. **Headers**: Provide metadata about the request or response.
8. **Body**: Contains data sent to or returned from the server.
9. **Status Codes**: Indicate the result of the request (e.g., `200 OK`, `404 Not Found`, `500 Internal Server Error`).

---

## **Example Lifecycle for a `GET` Request**
1. **Client**: Sends a `GET` request to `https://api.example.com/users/123`.
2. **Server**: Receives the request and routes it to the `UserController`.
3. **Controller**: Executes the `getUser` method, which queries the database for the user with ID `123`.
4. **Database**: Returns the user data to the controller.
5. **Controller**: Generates a response with the user data and a `200 OK` status code.
6. **Client**: Receives the response and displays the user data.

---

## **Example Lifecycle for a `POST` Request**
1. **Client**: Sends a `POST` request to `https://api.example.com/users` with a JSON body containing new user data.
2. **Server**: Receives the request and routes it to the `UserController`.
3. **Controller**: Executes the `createUser` method, which validates the data and inserts it into the database.
4. **Database**: Stores the new user data and returns the generated user ID.
5. **Controller**: Generates a response with the new user ID and a `201 Created` status code.
6. **Client**: Receives the response and updates the UI to reflect the new user.

---

## **Advantages of REST**
- **Stateless**: Each request is independent and contains all the information needed to process it.
- **Scalable**: RESTful APIs can handle a large number of clients and requests.
- **Cacheable**: Responses can be cached to improve performance.
- **Uniform Interface**: Uses standard HTTP methods and status codes, making it easy to understand and use.

---




## Cookies

# How cookies are used for session management

**Cookies** are a fundamental mechanism for **session management** in web applications. They allow servers to maintain stateful interactions with clients over the stateless HTTP protocol. Here's a detailed explanation of how cookies are used for session management:

---

## **1. What Are Cookies?**
- **Cookies** are small pieces of data (key-value pairs) that a server sends to a client (e.g., a browser).
- The client stores the cookie and sends it back to the server with every subsequent request to the same domain.
- Cookies are primarily used for:
  - Session management (e.g., keeping users logged in).
  - Personalization (e.g., remembering user preferences).
  - Tracking (e.g., analytics or advertising).

---

## **2. How Cookies Work for Session Management**

### **Step 1: User Logs In**
1. The user submits a login form (e.g., username and password).
2. The server validates the credentials.
3. If valid, the server creates a **session** for the user and stores the session data (e.g., user ID, permissions) in a **session store** (e.g., in-memory store, database, or Redis).
4. The server generates a **session ID** (a unique identifier for the session) and sends it to the client as a **cookie**.

**Example HTTP Response**:
```http
HTTP/1.1 200 OK
Set-Cookie: sessionId=abc123; Path=/; HttpOnly; Secure; SameSite=Strict
Content-Type: application/json

{
  "message": "Login successful"
}
```

- **`sessionId=abc123`**: The session ID stored in the cookie.
- **`Path=/`**: The cookie is sent for all requests to the domain.
- **`HttpOnly`**: The cookie cannot be accessed by JavaScript (for security).
- **`Secure`**: The cookie is only sent over HTTPS (for security).
- **`SameSite=Strict`**: The cookie is only sent for same-site requests (prevents CSRF attacks).

---

### **Step 2: Browser Stores the Cookie**
- The browser stores the cookie in its **cookie jar**.
- The cookie is associated with the domain of the server (e.g., `example.com`).

---

### **Step 3: Subsequent Requests Include the Cookie**
- For every subsequent request to the server, the browser automatically includes the cookie in the `Cookie` header.

**Example HTTP Request**:
```http
GET /profile HTTP/1.1
Host: example.com
Cookie: sessionId=abc123
Accept: application/json
```

---

### **Step 4: Server Validates the Session**
1. The server extracts the `sessionId` from the `Cookie` header.
2. The server looks up the session data in the **session store** using the `sessionId`.
3. If the session is valid, the server processes the request and returns the appropriate response.
4. If the session is invalid (e.g., expired or not found), the server returns an error (e.g., `401 Unauthorized`).

---

### **Step 5: User Logs Out**
1. The user logs out by sending a request to the server (e.g., `POST /logout`).
2. The server deletes the session from the **session store**.
3. The server instructs the browser to delete the cookie by sending an expired `Set-Cookie` header.

**Example HTTP Response**:
```http
HTTP/1.1 200 OK
Set-Cookie: sessionId=; Path=/; Expires=Thu, 01 Jan 1970 00:00:00 GMT; HttpOnly; Secure
Content-Type: application/json

{
  "message": "Logout successful"
}
```

- **`Expires=Thu, 01 Jan 1970 00:00:00 GMT`**: Sets the cookie's expiration date to the past, causing the browser to delete it.

---

## **3. Types of Cookies Used in Session Management**
1. **Session Cookies**:
   - Temporary cookies that are deleted when the browser is closed.
   - Used for managing user sessions.
   - Example: `sessionId=abc123`.

2. **Persistent Cookies**:
   - Cookies with an expiration date.
   - Used for long-term storage (e.g., "Remember Me" functionality).
   - Example: `rememberMe=true; Expires=Fri, 31 Dec 2023 23:59:59 GMT`.

---

## **4. Security Considerations**
1. **Secure Cookies**:
   - Use the `Secure` flag to ensure cookies are only sent over HTTPS.
   - Prevents cookies from being intercepted over unencrypted connections.

2. **HttpOnly Cookies**:
   - Use the `HttpOnly` flag to prevent JavaScript from accessing the cookie.
   - Protects against XSS (Cross-Site Scripting) attacks.

3. **SameSite Cookies**:
   - Use the `SameSite` attribute to prevent cookies from being sent in cross-site requests.
   - Protects against CSRF (Cross-Site Request Forgery) attacks.

4. **Session Expiry**:
   - Set a reasonable expiration time for sessions to reduce the risk of session hijacking.
   - Implement mechanisms to invalidate sessions (e.g., logout, session timeout).

---

## **5. Alternatives to Cookies for Session Management**
1. **JSON Web Tokens (JWT)**:
   - Stateless tokens that encode session data.
   - Sent in the `Authorization` header instead of cookies.
   - Commonly used in Single Page Applications (SPAs) and mobile apps.

2. **Local Storage**:
   - Stores session data in the browser's local storage.
   - Requires manual handling of tokens in requests (e.g., in the `Authorization` header).

---

## **6. Example Workflow**
1. **Login**:
   - User submits login form.
   - Server creates a session and sends a cookie with the session ID.
   - Browser stores the cookie.

2. **Access Protected Resource**:
   - Browser sends the cookie with the session ID in the request.
   - Server validates the session and returns the resource.

3. **Logout**:
   - User logs out.
   - Server deletes the session and instructs the browser to delete the cookie.

---

By using cookies for session management, web applications can maintain stateful interactions with clients while leveraging the stateless nature of HTTP. Proper implementation and security measures are essential to protect user sessions and data.
