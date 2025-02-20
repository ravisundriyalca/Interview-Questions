# Interview-Questions
 
 ## List Of Interview Questions
- [explain how a web request to amazon.com works and is served?](#workflow)
- [Explain REST request lifecycle](#restflow)

# Workflow

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

By following these steps, your browser successfully retrieves and displays the Amazon.com webpage. This process happens in milliseconds, thanks to the highly optimized infrastructure and technologies used by Amazon.



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


