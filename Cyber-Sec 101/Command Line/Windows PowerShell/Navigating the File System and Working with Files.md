 dir command in Command Prompt (or ls in Unix-like systems), ***Get-ChildItem*** lists the files and directories in a location specified with the -Path parameter. It can be used to explore directories and view their contents. If no Path is specified, the cmdlet will display the content of the current working directory.
 
![](../../../Attacments/Pasted%20image%2020260903211813.png)


To create an item in PowerShell, we can use ***New-Item.*** We will need to specify the path of the item and its type (whether it is a file or a directory).

![](../../../Attacments/Pasted%20image%2020260903211934.png)


![](../../../Attacments/Pasted%20image%2020260903212008.png)

![](../../../Attacments/Pasted%20image%2020260903212100.png)


Finally, to read and display the contents of a file, we can use the Get-Content cmdlet, which works similarly to the type command in Command Prompt (or cat in Unix-like systems).
		
PS C:\Users\captain\Documents\captain-cabin> Get-Content -Path ".\captain-hat.txt"