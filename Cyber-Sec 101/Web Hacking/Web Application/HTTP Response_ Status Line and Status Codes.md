![Illustration depicting HTTP Response or Status Codes, showing different codes like 200 (OK), 404 (Not Found), and 500 (Internal Server Error). Each code is represented visually with labels, indicating the server's response to client requests and the status of the interaction.](https://cdn-images.tryhackme.com/user-uploads/66c513e4445cb5649e636a36/room-content/66c513e4445cb5649e636a36-1725910481619.png)

When you interact with a web application, the server sends back an **HTTP response** to let you know whether your request was successful or something went wrong. These responses include a **status code** and a short explanation (called the **Reason Phrase**) that gives insight into how the server handled your request.

### Status Line

The first line in every HTTP response is called the **Status Line**. It gives you three key pieces of info:

1. **HTTP Version**: This tells you which version of HTTP is being used.
2. **Status Code**: A three-digit number showing the outcome of your request.
3. **Reason Phrase**: A short message explaining the status code in human-readable terms.

Since we already covered HTTP Versions in Task 5, let’s focus on the **Status Codes** and **Reason Phrases** here.

### Status Codes and Reason Phrases

The **Status Code** is the number that tells you if the request succeeded or failed, while the **Reason Phrase** explains what happened. These codes fall into five main categories:

**Informational Responses (100-199)**  
These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.

**Successful Responses (200-299)**  
These codes mean everything worked as expected. The server processed the request and sent back the requested data.

**Redirection Messages (300-399)**  
These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.

**Client Error Responses (400-499)**  
These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.

**Server Error Responses (500-599)**  
These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.

### Common Status Codes

Here are some of the most frequently seen status codes:

**100 (Continue)**  
The server got the first part of the request and is ready for the rest.

**200 (OK)**  
The request was successful, and the server is sending back the requested resource.

**301 (Moved Permanently)**  
The resource you’re requesting has been permanently moved to a new URL. Use the new URL from now on.

**404 (Not Found)**  
The server couldn’t find the resource at the given URL. Double-check that you’ve got the right address.

**500 (Internal Server Error)**  
Something went wrong on the server’s end, and it couldn’t process your request.

Answer the questions below

What part of an HTTP response provides the HTTP version, status code, and a brief explanation of the response's outcome?



Which category of HTTP response codes indicates that the web server encountered an internal issue or is unable to fulfil the client's request?



Which HTTP status code indicates that the requested resource could not be found on the web server?

