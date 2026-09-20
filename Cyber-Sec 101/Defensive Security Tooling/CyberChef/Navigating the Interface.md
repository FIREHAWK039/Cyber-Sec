CyberChef consists of four areas. Each consists of different components or features.

These are the following areas:

1. Operations
2. Recipe
3. Input
4. Output

![CyberChef's main page with all the features.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1728731934241.png)  

Let's discuss each of these areas below.

## The Operations Area

This is a practical and comprehensive repository of all the diverse operations that CyberChef is equipped to perform. These operations are meticulously categorized, offering users convenient access to various capabilities. Users can utilize the search feature to locate specific operations quickly, enhancing their efficiency and productivity.

Below are some operations you might use throughout your cyber security journey.

|Operations|Description|Examples|
|---|---|---|
|From Morse Code|Translates Morse Code into (upper case) alphanumeric characters.|`- .... .-. . .- - ...` becomes `THREATS` when used with default parameters|
|URL Encode|Encodes problematic characters into percent-encoding, a format supported by URIs/URLs.|`https://tryhackme.com/r/room/cyberchefbasics` becomes `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` when used with the parameter “Encode all special chars”|
|To Base64|This operation encodes raw data into an ASCII Base64 string.|`This is fun!` becomes `VGhpcyBpcyBmdW4h`|
|To Hex|Converts the input string to hexadecimal bytes separated by the specified delimiter.|`This Hex conversion is awesome!` becomes `54 68 69 73 20 48 65 78 20 63 6f 6e 76 65 72 73 69 6f 6e 20 69 73 20 61 77 65 73 6f 6d 65 21`|
|To Decimal|Converts the input data to an ordinal integer array.|`This Decimal conversion is awesome!` becomes `84 104 105 115 32 68 101 99 105 109 97 108 32 99 111 110 118 101 114 115 105 111 110 32 105 115 32 97 119 101 115 111 109 101 33`|
|ROT13|A simple Caesar substitution cipher which rotates alphabet characters by the specified amount (default 13).|`Digital Forensics and Incident Response` becomes `Qvtvgny Sberafvpf naq Vapvqrag Erfcbafr`|

Alternatively, you can directly check how the operations work by hovering on the specific operation. This should give you a sample or a description and a link to Wikipedia.

![Hovering to an operation in CyberChef tool.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1729081368672.png)  

## The Recipe Area

This is considered as the heart of the tool. In this area, you can seamlessly select, arrange, and fine-tune operations to suit your needs. This is where you take control, defining each operation's arguments and options precisely and purposefully. The recipe area is a designated space to select and arrange specific operations and then define their respective arguments and options to customize their behaviour further. In the recipe area, you can drag the operations you want to use and specify arguments and options.

Features include the following:

- `Save recipe`: This feature allows the user to save selected operations.
- `Load recipe`: Allows the user to load previously saved recipes.
- `Clear Recipe`: This feature will enable users to clear the chosen recipe during usage.

These can be found in the highlighted icons below:

![The Recipe area of CyberChef tool with multiple options.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1728731934220.png)

The bottom part of the image above is the `BAKE!` button. This processes the data with the given recipe.

Additionally, you can tick the `Auto Bake` checkbox. This feature allows users to automatically cook using the selected recipe without manually clicking `BAKE!` every time.

## Input Area

The input area provides a user-friendly space where you can easily input text or files by pasting, typing, or dragging them to perform operations.

![The Input area of CyberChef tool with multiple options.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1729081714973.png)  

Additionally, it has the following features:

- `Add a new input tab`: This is where an additional tab is created for the user to use different values from the previous tab.

![Open a new input tab option under the Input Area.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1728731934218.png)

- `Open folder as input`: This feature allows users to upload a whole folder as input value.

![Open folder as input option under the Input Area.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1728731934186.png)  

- `Open file as input`: This feature allows the user to upload a file as its input value.

![Open file as input option under the Input Area.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1728731934210.png)  

- `Clear input and output`: This feature allows the user to clear any input values inserted and the corresponding output value.
- `Reset pane layout`: This feature brings the tool's interface to its default window sizes.

## Output Area

The output area is a visual space that showcases the data processing results. It neatly presents the outcomes of any manipulations or transformations you have applied to the input data, allowing for a clear and intuitive display of the processed information.

![The Output area of CyberChef tool with multiple options.](https://cdn-images.tryhackme.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1729081715061.png)  

Features include:

- `Save output to file`: This feature allows the users to save the result into a .dat file.
- `Copy raw output to the clipboard`: This feature allows users to copy raw output directly to their clipboard, allowing them to quickly copy the results for use in other applications or documents.
- `Replace input with output`: This feature allows users to quickly overwrite the input data based on the operations' results.
- `Maximise output pane`: This feature brings the tool's interface to its default window sizes.