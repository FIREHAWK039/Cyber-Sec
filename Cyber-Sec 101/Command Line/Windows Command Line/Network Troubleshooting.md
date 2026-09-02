
![](Attacments/Pasted%20image%2020260902134847.png)

#### Establishing an SSH Connection from the AttackBox

![](../../../Attacments/Pasted%20image%2020260902135014.png)

If this is the first time you initiate an SSH connection from the AttackBox to a target system, the steps are shown in the screenshot below, and they are the following:

1. Start the AttackBox’s terminal by clicking the terminal icon marked with 1.
2. To connect to the target VM, issue the command `ssh user@MACHINE_IP` as `user` is the username in this case.
3. Because this is your first time connecting to this target VM, you will be asked to trust this connection. Answer with **yes** as marked with 3.
4. Enter your password `Tryhackme123!`. Please note that the password will not appear as you type it. 
5.             


Use the `ver` command to determine the operating system (OS) version



![](Attacments/Pasted%20image%2020260902134558.png)

Run the `systeminfo` command to list various information about the system such as OS information, system details, processor and memory.


Another valuable tool for troubleshooting is tracert, which stands for trace route. The command tracert target_name traces the network route traversed to reach the target. Without getting into more details, it expects the routers on the path to notify us if they drop a packet because its time-to-live (TTL) has reached zero. The terminal output below shows that we passed through 15 routers before reaching our target.
      ![[Pasted image 20260901050653.png]]


One networking command worth knowing is nslookup. It looks up a host or domain and returns its IP address. The syntax nslookup example.com will look up example.com using the default name server; however, nslookup example.com 1.1.1.1 will use the name server one.one.one.one


The final networking command we will cover in this room is netstat. This command displays current network connections and listening ports. A basic netstat command with no arguments will show you established connections, as shown below. In this case, we only have one SSH connection; we figured out it is SSH because it is bound to port 22.
           
    ![[Pasted image 20260831045125.png]]
    
you can run netstat -h, where -h displays the help page. We opted for the following options:

**-a displays all established connections and listening ports**
**-b shows the program associated with each listening port and established connection**
**-o reveals the process ID (PID) associated with the connection**
**-n uses a numerical form for addresses and port numbers**

We combine these four options and execute the netstat -abon command. 
![](Pasted%20image%2020260831043358.png)
