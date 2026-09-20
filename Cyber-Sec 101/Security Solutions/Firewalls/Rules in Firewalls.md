A firewall gives you control over your network’s traffic. Although it filters the traffic based on its built-in rules, some customized rules can be defined for various networks. For example, there would be networks that want to deny all the SSH traffic coming into their network. However, your network would have a requirement to allow SSH traffic from a few specific IP addresses. The rules allow you to configure these customized settings for your network’s incoming and outgoing traffic.

The basic components of a firewall’s rule are described below:

Source address: The machine’s IP address that would originate the traffic.
Destination address: The machine’s IP address that would receive the data.
Port: The port number for the traffic.
Protocol: The protocol that would be used during the communication.
Action: This defines the action that would be taken upon identifying any traffic of this particular nature.
Direction: This field defines the rule’s applicability to incoming or outgoing traffic.
Types of Actions
The component “Action” from a rule indicates the steps to take after a data packet falls under the category of the defined rule. Three main actions that can be applied to a rule are explained below.

Allow
A rule’s “Allow” action indicates that the particular traffic defined inside the rule would be permitted.

For example, let’s create a rule with an action to allow all the outgoing traffic from our network for port 80 (used for HTTP traffic to the Internet).

Action	Source	Destination	Protocol	Port	Direction
Allow	192.168.1.0/24	Any	TCP	80	Outbound
Deny
A rule’s “Deny” action means that the traffic defined inside the rule would be blocked and not permitted. These rules are fundamental for the security team to deny specific traffic coming from malicious IP addresses and create more rules to reduce the threat surface of the network.

For example, let’s create a rule with an action to deny all the incoming traffic on port 22 (used for remotely connecting to a machine via SSH) of our critical server.

Action	Source	Destination	Protocol	Port	Direction
Deny	Any	192.168.1.0/24	TCP	22	Inbound
Forward
The action “Forward” redirects traffic to a different network segment using the forwarding rules created on the firewalls. This applies to the firewalls that provide routing functionality and act as gateways between different network segments.

For example, let’s create a rule with an action to forward all the incoming traffic on port 80 (used for HTTP traffic) to the web server 192.168.1.8.

Action	Source	Destination	Protocol	Port	Direction
Forward	Any	192.168.1.8	TCP	80	Inbound
Directionality of Rules
Firewalls have different categories of rules, each categorized based on the traffic directionality on which the rules are created. Let’s examine each of these directionalities.



Inbound Rules
Rules are categorized as inbound rules when they are meant to be applied to incoming traffic only. For example, you might allow incoming HTTP traffic (port 80) on your web server.

Outbound Rules
These rules are made for outgoing traffic only. For example, blocking all outgoing SMTP traffic (port 25) from all the devices except the mail server.

Forward Rules
Forwarding rules are created to forward specific traffic inside the network. For example, a forwarding rule can be created to forward the incoming HTTP (port 80) traffic to the web server located in your network.