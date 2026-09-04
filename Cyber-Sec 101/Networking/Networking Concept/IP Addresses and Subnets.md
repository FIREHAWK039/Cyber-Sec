What makes an IP address? An IP address comprises four octets, i.e., 32 bits. Being 8 bits, an octet allows us to represent a decimal number between 0 and 255
                ![359](../../../Attacments/Pasted%20image%2020260904125231.png)
                
At the risk of oversimplifying things, the 0 and 255 are reserved for the network and broadcast addresses,  In other words, `192.168.1.0` is the network address, while `192.168.1.255` is the broadcast address.
If you are curious about the math, it is approximately 232 because we have 32 bits.

`ipconfig`
`ip address show` == `ip a s`



![](../../../Attacments/Pasted%20image%2020260904125824.png)

The terminal output above indicates the following:

- The host (laptop) IP address is `192.168.66.89`
- The subnet mask is `255.255.255.0`
- The broadcast address is `192.168.66.255`

### Private Addresses

As we are explaining IP addresses, it is useful to mention that for most practical purposes, there are two types of IP addresses:

- Public IP addresses
- Private IP addresses

RFC 1918 defines the following three ranges of private IP addresses:

- `10.0.0.0` - `10.255.255.255` (`10/8`)
- `172.16.0.0` - `172.31.255.255` (`172.16/12`)
- `192.168.0.0` - `192.168.255.255` (`192.168/16`)

### Routing

A router is like your local post office; you hand them the mail parcel, and they would know how to deliver it. If we dig deeper, you might mail something to an address in another city or country. The post office will check the address and decide where to send it next. For example, if it is to leave the country, we expect one central office to handle all shipments abroad.

In technical terms, a router forwards data packets to the proper network. Usually, a data packet passes through multiple routers before it reaches its final destination. The router functions at layer 3, inspecting the IP address and forwarding the packet to the best network (router) so the packet gets closer to its destination.