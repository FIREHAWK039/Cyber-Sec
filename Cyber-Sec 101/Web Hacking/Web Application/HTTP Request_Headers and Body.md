## Request Headers

Request Headers allow extra information to be conveyed to the web server about the request. Some common headers are as follows:  

**Common Request Headers**

|   |   |   |
|---|---|---|
|**Request Header**|**Example**|**Description**|
|Host|`Host: tryhackme.com`|Specifies the name of the web server the request is for.|
|User-Agent|`User-Agent: Mozilla/5.0`|Shares information about the web browser the request is coming from.|
|Referer|`Referer: https://www.google.com/`|Indicates the URL from which the request came from.|
|Cookie|`Cookie: user_type=student; room=introtowebapplication; room_status=in_progress`|Information the web server previously asked the web browser to store is held in cookies.|
|Content-Type|`Content-Type: application/json`|Describes what type or format of data is in the request.|

  

## Request Body

In HTTP requests such as POST and PUT, where data is sent to the web server as opposed to requested from the web server, the data is located inside the HTTP Request Body. The formatting of the data can take many forms, but some common ones are `URL Encoded`, `Form Data`, `JSON`, or `XML`.

- **URL Encoded (application/x-www-form-urlencoded)**  
    A format where data is structured in pairs of key and value where (`key=value`). Multiple pairs are separated by an (`&`) symbol, such as `key1=value1&key2=value2`. Special characters are percent-encoded.  
      
    **_Example_**  
    
    ```http
    POST /profile HTTP/1.1
    Host: tryhackme.com
    User-Agent: Mozilla/5.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 33
    
    name=Aleksandra&age=27&country=US
    ```
    
- **Form Data (multipart/form-data)**  
    Allows multiple data blocks to be sent where each block is separated by a boundary string. The boundary string is the defined header of the request itself. This type of formatting can be used to send binary data, such as when uploading files or images to a web server.  
      
    **_Example_**  
    
    ```http
    POST /upload HTTP/1.1
    Host: tryhackme.com
    User-Agent: Mozilla/5.0
    Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
    
    ----WebKitFormBoundary7MA4YWxkTrZu0gW
    Content-Disposition: form-data; name="username"
    
    aleksandra
    ----WebKitFormBoundary7MA4YWxkTrZu0gW
    Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
    Content-Type: image/jpeg
    
    [Binary Data Here representing the image]
    ----WebKitFormBoundary7MA4YWxkTrZu0gW--
    ```
    
- **JSON (application/json)**  
    In this format, the data can be sent using the JSON (JavaScript Object Notation) structure. Data is formatted in pairs of name : value. Multiple pairs are separated by commas, all contained within curly braces { }.  
      
    **_Example_**  
    
    ```http
    POST /api/user HTTP/1.1
    Host: tryhackme.com
    User-Agent: Mozilla/5.0
    Content-Type: application/json
    Content-Length: 62
    
    {
        "name": "Aleksandra",
        "age": 27,
        "country": "US"
    }
    ```
    
- **XML (application/xml)**  
    In XML formatting, data is structured inside labels called tags, which have an opening and closing. These labels can be nested within each other. You can see in the example below the opening and closing of the tags to send details about a user called Aleksandra.  
      
    **_Example_**  
    
    ```http
    POST /api/user HTTP/1.1
    Host: tryhackme.com
    User-Agent: Mozilla/5.0
    Content-Type: application/xml
    Content-Length: 124
    
    <user>
        <name>Aleksandra</name>
        <age>27</age>
        <country>US</country>
    </user>
    ```
    

Answer the questions below

Which HTTP request header specifies the domain name of the web server to which the request is being sent?

Correct Answer

What is the default content type for form submissions in an HTTP request where the data is encoded as key=value pairs in a query string format?

Correct Answer

Which part of an HTTP request contains additional information like host, user agent, and content type, guiding how the web server should process the request?

Correct Answer