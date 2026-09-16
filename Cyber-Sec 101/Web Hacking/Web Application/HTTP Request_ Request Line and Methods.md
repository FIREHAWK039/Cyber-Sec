An **HTTP request** is what a user sends to a web server to interact with a web application and make something happen. Since these requests are often the first point of contact between the user and the web server, knowing how they work is super important—especially if you’re into cyber security.

![Illustration showing a GET request and all of the different headers that are used.](https://cdn-images.tryhackme.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1730445201524.png)

Imagine an HTTP request showing the key parts like the method (e.g., GET or POST), path (e.g., /login), and version (e.g., HTTP/1.1). These elements make up the basics of how a client (user) communicates with a server.

### Request Line

The **request line** (or start line) is the first part of an HTTP request and tells the server what kind of request it’s dealing with. It has three main parts: the **HTTP method**, the **URL path**, and the **HTTP version**.

**Example:** `METHOD /path HTTP/version`

### HTTP Methods

The **HTTP method** tells the server what action the user wants to perform on the resource identified by the URL path. Here are some of the most common methods and their possible security issue:

**GET  
**Used to **fetch** data from the server without making any changes. Reminder! Make sure you’re only exposing data the user is allowed to see. Avoid putting sensitive info like tokens or passwords in GET requests since they can show up as plaintext.

**POST  
****Sends** data to the server, usually to create or update something. Reminder! Always validate and clean the input to avoid attacks like SQL injection or XSS.

**PUT  
**Replaces or **updates** something on the server. Reminder! Make sure the user is authorised to make changes before accepting the request.

**DELETE  
****Removes** something from the server. Reminder! Just like with PUT, make sure only authorised users can delete resources.

Besides these common methods, there are a few others used in specific cases:

**PATCH  
**Updates part of a resource. It’s useful for making small changes without replacing the whole thing, but always validate the data to avoid inconsistencies.

**HEAD  
**Works like GET but only retrieves headers, not the full content. It’s handy for checking metadata without downloading the full response.

**OPTIONS  
**Tells you what methods are available for a specific resource, helping clients understand what they can do with the server.

**TRACE  
**Similar to OPTIONS, it shows which methods are allowed, often for debugging. Many servers disable it for security reasons.

**CONNECT  
**Used to create a secure connection, like for HTTPS. It’s not as common but is critical for encrypted communication.

Each of these methods has its own set of security rules. For example, PATCH requests should be validated to avoid inconsistencies, and OPTIONS and TRACE should be turned off if not needed to avoid possible security risks.

### URL Path

The **URL path** tells the server where to find the resource the user is asking for. For instance, in the URL `https://tryhackme.com/api/users/123`, the path `/api/users/123` identifies a specific user.

Attackers often try to manipulate the URL path to exploit vulnerabilities, so it’s crucial to:

- Validate the URL path to prevent unauthorised access
- Sanitise the path to avoid injection attacks
- Protect sensitive data by conducting privacy and risk assessments

Following these practices helps protect your web application from common attacks.

### HTTP Version

The **HTTP version** shows the protocol version used to communicate between the client and server. Here’s a quick rundown of the most common ones:

**HTTP/0.9** (1991)The first version, only supported GET requests.

**HTTP/1.0** (1996)Added headers and better support for different types of content, improving caching.

**HTTP/1.1** (1997)Brought persistent connections, chunked transfer encoding, and better caching. It’s still widely used today.

**HTTP/2** (2015)Introduced features like multiplexing, header compression, and prioritisation for faster performance.

**HTTP/3** (2022)Built on HTTP/2, but uses a new protocol (QUIC) for quicker and more secure connections.

Although HTTP/2 and HTTP/3 offer better speed and security, many systems still use **HTTP/1.1** because it’s well-supported and works with most existing setups. However, upgrading to HTTP/2 or HTTP/3 can provide significant performance and security improvements as more systems adopt them.

Answer the questions below

Which HTTP protocol version became widely adopted and remains the most commonly used version for web communication, known for introducing features like persistent connections and chunked transfer encoding?


Which HTTP request method describes the communication options for the target resource, allowing clients to determine which HTTP methods are supported by the web server?


In an HTTP request, which component specifies the specific resource or endpoint on the web server that the client is requesting, typically appearing after the domain name in the URL?

