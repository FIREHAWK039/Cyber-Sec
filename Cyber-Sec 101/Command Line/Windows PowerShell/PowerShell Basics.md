PowerShell commands are known as ***cmdlets*** (pronounced command-lets). They are much more powerful than the traditional Windows commands and allow for more advanced data manipulation.

Cmdlets follow a consistent Verb-Noun naming convention. This structure makes it easy to understand what each cmdlet does. The Verb describes the action, and the Noun specifies the object on which action is performed. For example:

***Get-Content:*** Retrieves (gets) the content of a file and displays it in the console.
***Set-Location:*** Changes (sets) the current working directory.

To list all available cmdlets, functions, aliases, and scripts that can be executed in the current PowerShell session, we can use ***Get-Command.*** It’s an essential tool for discovering what commands one can use.

![](../../../Attacments/Pasted%20image%2020260903203719.png)

***Get-Alias*** lists all aliases available. For example, dir is an alias for Get-ChildItem, and cd is an alias for Set-Location

![](../../../Attacments/Pasted%20image%2020260903204458.png)