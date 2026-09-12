Unlike HTTP, which is designed to retrieve web pages, File Transfer Protocol (FTP) is designed to transfer files. As a result, FTP is very efficient for file transfer, and when all conditions are equal, it can achieve higher speeds than HTTP.

Example commands defined by the FTP protocol are:

USER is used to input the username
PASS is used to enter the password
RETR (retrieve) is used to download a file from the FTP server to the client.
STOR (store) is used to upload a file from the client to the FTP server.
FTP server listens on TCP port 21 by default; data transfer is conducted via another connection from the client to the server.

In the terminal below we executed the command ftp 10.49.180.230 to connect to the remote FTP server using the local ftp client. Then we went through the following steps:

We used the username anonymous to log in
We didn’t need to provide any password
Issuing ls returned a list of files available for download
type ascii switched to ASCII mode as this is a text file
get coffee.txt allowed us to retrieve the file we want
The command exchange via the FTP client is shown in the terminal below.

![](../../../Attacments/Pasted%20image%2020260912200203.png)

![](../../../Attacments/Pasted%20image%2020260912200214.png)