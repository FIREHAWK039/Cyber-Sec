Gobuster has a `dir` mode, allowing users to enumerate website directories and their files. This mode is useful when you are performing a penetration test and would like to see what the directory structure of a website is and what files it contains. Often, directory structures of websites and web apps follow a particular convention, making them susceptible to Brute Force using wordlists. For example, the  directory structure on the web server hosting WordPress looks something  like this:

AttackBox Terminal

```shell-session
root@tryhackme:~# tree -L 3 -d
.
└── html
    └── wordpress
        ├── wp-admin
        ├── wp-content
        └── wp-includes
```

Gobuster is powerful because it allows you to scan the website and return the status codes. These status codes immediately tell you if you, as an outside user, can request that directory or not.

## Help

If you want a complete overview of what the Gobuster `dir` command can offer, you can look at the help page. Seeing the extensive help page for the dir command can somewhat be intimidating. So, we will focus on the most essential flags in this room. Type the following command to display the help: `gobuster dir --help`.

Many flags are used to fine-tune the `gobuster dir` command. It is out of scope to go over each one of them, but in the table below, we have listed the flags that cover most of the scenarios:

  

|Flag|Long Flag|Description|
|---|---|---|
|`-c`|`--cookies`|This flag configures a cookie to pass along each request, such as a session ID.|
|`-x`|`--extensions`|This flag specifies which file extensions you want to scan for. E.g., .php, .js|
|`-H`|`--headers`|This flag configures an entire header to pass along with each request.|
|`-k`|`--no-tls-validation`|This flag  skips the process that checks the certificate when https is used. It often happens for CTF events or test rooms like the ones on THM a self-signed certificate is used. This causes an error during the TLS check.|
|`-n`|`--no-status`|You can set this flag when you don’t want to see status codes of each response received. This helps keep the output on the screen clear.|
|`-P`|`password`|You can set this flag together with the --username flag to execute authenticated requests. This is handy when you have obtained credentials from a user.|
|`-s`|`--status-codes`|With this flag, you can configure which status codes of the received responses you want to display, such as 200, or a range like 300-400.|
|`-b`|`--status-codes-blacklist`|This flag allows you to configure which status codes of the received responses you don’t want to display. Configuring this flag overrides the -s flag.|
|`-U`|`--username`|You can set this flag together with the `--password` flag to execute authenticated requests. This is handy when you have obtained credentials from a user.|
|`-r`|`--followredirect`|This flags configures Gobuster to follow the redirect that it received as a response to the sent request. A HTTP redirect status code (e.g., 301 or 302) is used to redirect the client to a different URL.|

## How To Use dir Mode

To run Gobuster in `dir` mode, use the following command format:

```
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist
```

  
Notice that the command also includes the flags `-u` and `-w`, in addition to the `dir` keyword. These two flags are required for the Gobuster directory enumeration to work. Let us look at a practical example of how to enumerate directories and files with Gobuster `dir` mode:

```
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```

  
This command scans all the directories located at _www.example.thm_ using the wordlist _directory-list-2.3-medium.txt_. Let’s look a bit closer at each part of the command:

- `gobuster dir`: Configures Gobuster to use the directory and file enumeration mode.
- `-u http://www.example.thm`:

- The URL will be the base path where Gobuster starts looking. So, the URL  above is using the root web directory. For example, in a typical Apache installation on Linux, this is `/var/www/html`. So if you have a “resources” directory and you want to enumerate that directory, you’d set the URL as `http://www.example.thm/resources`. You can also think of this like `http://www.example.thm/path/to/folder`.
- The URL must contain the protocol used, in this case, HTTP. This is important and required. If you pass the wrong protocol, the scan will fail.
- In the host part of the URL, you can either fill in the IP or the HOSTNAME. However, it is important to mention that when using the IP, you may target a different website than intended. A web server can host multiple websites using one IP (this technique is also called virtual hosting). Use the HOSTNAME if you want to be sure.
- Gobuster does not enumerate recursively. So, if the results show a directory path you are interested in, you will have to enumerate that specific directory.

- `-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` configures Gobuster to use the _directory-list-2.3-medium.txt_ wordlist to enumerate. Each entry of the wordlist is appended to the configured URL.
- `-r` configures Gobuster to follow the redirect responses received from the sent requests. If a status code 301 was received, Gobuster will navigate to the redirect URL that is included in the response.  
    

Let’s look at a second example where we use the `-x` flag to specify what type of files we want to enumerate:

```
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```

  
This command will look for directories located at [http://example.thm(opens in new tab)](http://example.thm/) using the wordlist _directory-list-2.3-medium.txt_. In addition to directory listing, this command also lists all the files that have a .php or .js extension.