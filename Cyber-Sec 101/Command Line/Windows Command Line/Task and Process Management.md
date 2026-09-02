We can list the running processes using tasklist

Some filtering is helpful because the output is expected to be very long. You can check all available filters by displaying the help page using tasklist /?. Let’s say that we want to search for tasks related to sshd.exe, we can do that with the command tasklist /FI "imagename eq sshd.exe". Note that /FI is used to set the filter image name equals sshd.exe.

![](../../../Attacments/Pasted%20image%2020260902214234.png)

With the process ID (PID) known, we can terminate any task using *taskkill /PID target_pid.* For example, if we want to kill the process with PID 4567, we would issue the command *taskkill /PID 4567.*


***chkdsk:*** checks the file system and disk volumes for errors and bad sectors.
***driverquery:*** displays a list of installed device drivers.
***sfc /scannow:*** scans system files for corruption and repairs them if possible

we used the command more in two ways:

Display text files: ***more file.txt***
Pipe long output to view it page by page: ***some_command | more***