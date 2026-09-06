A **packet** is a piece of data from Layer 3 (Network Layer) of the OSI model, containing information such as an IP header and payload. A **frame**, however, is used at Layer 2 (Data Link) of the OSI model, which, encapsulates the packet and adds additional information such as MAC addresses.

You can think of this process as similar to mailing a letter through the post. The envelope is a frame, which, is used to move the contents (in this analogy, the packet) of the envelope to another place. Once the recepient opens the envelop (frame), they will know how to forward the letter (packet) itself.
This process is called encapsulation which we discussed in  the OSI model

|                     |                                                                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Header**          | **Description**                                                                                                                                                         |
| Time to Live        | This field sets an expiry timer for the packet to not clog up your network if it never manages to reach a host or escape!                                               |
| Checksum            | This field provides integrity checking for protocols such as TCP/IP. If any data is changed, this value will be different from what was expected and therefore corrupt. |
| Source Address      | The IP address of the device that the packet is being sent **from** so that data knows where to **return to**.                                                          |
| Destination Address | The device's IP address the packet is being sent to so that data knows where to travel next.                                                                            |
What is the name for a piece of data when it **does have** IP addressing information?
Packet

What is the name for a piece of data when it **does not have** IP addressing information?
Frame