The TELNET (Teletype Network) protocol is a network protocol for remote terminal connection. In simpler words, telnet, a TELNET client, allows you to connect to and communicate with a remote system and issue text commands. Although initially it was used for remote administration, we can use telnet to connect to any server listening on a TCP port number.

On the target lab machine, different services are running. We will experiment with three of them:

Echo server: This server echoes everything you send it. By default, it listens on port 7.
Daytime server: This server listens on port 13 by default and replies with the current day and time.
Web (HTTP) server: This server listens on TCP port 80 by default and serves web pages.
Before continuing, we should mention that the echo and daytime servers are considered security risks and should not be run; however, we started them explicitly to demonstrate communication with the server using telnet. In the terminal below, we connect to the target VM at the echo server’s TCP port number 7. To close the connection, press the CTRL + ] keys simultaneously.


![](../../../Attacments/Pasted%20image%2020260910053110.png)


In the terminal below, we use telnet to connect to the daytime server listening at port 13. We noticed that the connection closes once the current date and time are returned.


![](../../../Attacments/Pasted%20image%2020260910053324.png)


Finally, let’s request a web page using telnet. After connecting to port 80, you need to issue the command GET / HTTP/1.1 and identify the host where anything goes, such as Host: telnet.thm. Next, you need to press Enter twice so your last input line is a blank line. The output below shows the exchange. (The page has been redacted.)

Note: You may have to press Enter after sending the information in case you don’t get a response.


![](../../../Attacments/Pasted%20image%2020260910053339.png)
