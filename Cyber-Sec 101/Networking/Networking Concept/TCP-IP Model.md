TCP/IP stands for Transmission Control Protocol/Internet Protocol and was developed in the 1970s by the Department of Defense (DoD)

In our presentation of the ISO OSI model, we went from bottom to top, from layer 1 to layer 7. let’s look at things from a different perspective, from top to bottom. From top to bottom, we have:

- **Application Layer**: The OSI model application, presentation and session layers, i.e., layers 5, 6, and 7, are grouped into the application layer in the TCP/IP model.
- **Transport Layer**: This is layer 4.
- **Internet Layer**: This is layer 3. The OSI model’s network layer is called the Internet layer in the TCP/IP model.
- **Link Layer**: This is layer 2.
 
The table below shows how the TCP/IP model layers map to the ISO/OSI model layers.

| Layer Number | ISO OSI Model      | TCP/IP Model (RFC 1122) | Protocols                                        |
| ------------ | ------------------ | ----------------------- | ------------------------------------------------ |
| 7            | Application Layer  | Application Layer       | HTTP, HTTPS, FTP, POP3, SMTP, IMAP, Telnet, SSH, |
| 6            | Presentation Layer |                         |                                                  |
| 5            | Session Layer      |                         |                                                  |
| 4            | Transport Layer    | Transport Layer         | TCP, UDP                                         |
| 3            | Network Layer      | Internet Layer          | IP, ICMP, IPSec                                  |
| 2            | Data Link Layer    | Link Layer              | Ethernet 802.3, WiFi 802.11                      |
| 1            | Physical Layer     |                         |                                                  |
