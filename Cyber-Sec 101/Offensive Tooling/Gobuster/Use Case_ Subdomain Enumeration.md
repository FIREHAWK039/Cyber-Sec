## Help

If you want a complete overview of what the Gobuster dns command can offer, you can have a look at the help page. Seeing the extensive help page for the `dns` command can be intimidating. So, we will focus on the most important flags in this room. Type the following command to display the help: `gobuster dns --help`  

The `dns` mode offers fewer flags than the `dir` mode. But these are more than enough to cover most DNS subdomain enumeration scenarios. Let us have a look at some of the commonly used flags:

|Flag|Long Flag|Description|
|---|---|---|
|`-c`|`--show-cname`|Show CNAME Records (cannot be used with the `-i` flag).|
|`-i`|`--show-ips`|Including this flag shows IP addresses that the domain and subdomains resolve to.|
|`-r`|`--resolver`|This flag configures a custom DNS server to use for resolving.|
|`-d`|`--domain`|This flag configures the domain you want to enumerate.|

### How to Use dns Mode

To run Gobuster in dns mode, use the following command syntax:  
`gobuster dns -d example.thm -w /path/to/wordlist`  

Notice that the command also includes the flags `-d` and `-w`, in addition to the `dns` keyword. These two flags are required for the Gobuster subdomain enumeration to work. Let us look at an example of how to enumerate  subdomains with Gobuster dns mode:

`gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`

- `gobuster dns` enumerates subdomains on the configured domain.  
    
- `-d example.thm` sets the target to the _example.thm_ domain.  
    
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` sets the wordlist to s_ubdomains-top1million-5000.txt_. Gobuster uses each entry of this list to construct a new DNS query. If the first entry of this list is 'all', the query would be _all.example.thm._

Go ahead and enter the command for yourself. You should get the following output:

AttackBox Terminal

```shell-session
root@tryhackme:~# gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Domain:     example.thm
[+] Threads:    10
[+] Timeout:    1s
[+] Wordlist:   /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
===============================================================
Starting gobuster in DNS enumeration mode
===============================================================
Found: www.example.thm
                                                                                                                                                            
Found: shop.example.thm
                                                                                                                                                            
Found: academy.example.thm
                                                                                                                                                            
Found: primary.example.thm
                                                                                                                                                            
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
=============================================================== 
```


# Use Case: Vhost Enumeration

The last and final mode we’ll focus on is the `vhost` mode. This mode allows Gobuster to brute force virtual hosts. Virtual hosts are different websites on the same machine. Sometimes, they look like subdomains, but don’t be deceived! Virtual hosts are IP-based and are running on the same server. Subdomains are set up in DNS. The  difference between `vhost` and `dns` mode is in the way Gobuster scans:

- `vhost` mode will navigate to the URL created by combining the configured HOSTNAME (-u flag) with an entry of a wordlist.
- `dns` mode will do a DNS lookup to the FQDN created by combining the configured domain name (-d flag) with an entry of a wordlist.

## Help

If you want a complete overview of what the Gobuster `vhost` command can offer, you can have a look at the help page. Seeing the extensive help page for the vhost command can be intimidating. So, we will focus on the most important flags in this room. Type the  following command to display the help: `gobuster vhost --help`  

The `vhost` mode offers flags similar to those of the dir mode. Let us have a look at some of the commonly used flags:

|**Short Flag**|**Long Flag**|**Description**|
|---|---|---|
|`-u`|`--url`|Specifies the base URL (target domain) for brute-forcing virtual hostnames.|
||`--append-domain`|Appends the base domain to each word in the wordlist (e.g., word.example.com).|
|`-m`|`--method`|Specifies the HTTP method to use for the requests (e.g., GET, POST).|
||`--domain`|Appends a domain to each wordlist entry to form a valid hostname (useful if not provided explicitly).|
||`--exclude-length`|Excludes results based on the length of the response body (useful to filter out unwanted responses).|
|`-r`|`--follow-redirect`|Follows HTTP redirects (useful for cases where subdomains may redirect).|

## How To Use vhost Mode

To run Gobuster in `vhost` mode, type the following command:

```
gobuster vhost -u "http://example.thm" -w /path/to/wordlist
```

  
Notice that the command also includes the flags `-u` and `-w`, in addition to the `vhost` keyword. These two flags are required for the Gobuster vhost enumeration to work. Let us look at a practical example of how to enumerate virtual hosts with Gobuster `vhost` mode:

AttackBox Terminal

```shell-session
root@tryhackme:~# gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) &amp; Christian Mehlmauer (@firefart)
===============================================================
[+] Url:              http://10.10.94.214
[+] Method:           GET
[+] Threads:          10
[+] Wordlist:         /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
[+] User Agent:       gobuster/3.6
[+] Timeout:          10s
[+] Append Domain:    true
[+] Exclude Length:   250,254,263,274,283,293,294,299,253,261,269,277,285,290,300,257,258,270,278,282,291,252,260,264,268,271,279,280,289,251,256,262,265,272,297,287,292,295,255,266,276,284,286,296,267,273,275,281,288,259,298
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: blog.example.thm Status: 200 [Size: 1493]
Found: shop.example.thm Status: 200 [Size: 2983]
Found: www.example.thm Status: 200 [Size: 84352]
Found: chelyabinsk-rnoc-rr02.backbone.example.thm Status: 404 [Size: 304]
Found: academy.example.thm Status: 200 [Size: 434]
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
===============================================================
```

  
You will notice that this command is much more complex than the base command syntax. It contains many more configured flags. This will often be the case in realistic tests, depending on how the infrastructure of the domain to test has been set up. In our case, we don't have a fully set up DNS infrastructure. This requires us to give in extra flags like `--domain` and `--append-domain`. We need to look at the web requests Gobuster sends to understand better how these flags work. Below, you can see a basic GET request to _www.example.thm_:

```javascript
GET / HTTP/1.1
Host: www.example.thm
User-Agent: gobuster/3.6
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

Gobuster will send multiple requests, each time changing the `Host:` part of the request. The value of `Host:` in this example is _www.example.thm_. We can break this down into three parts:

- `www`: This is the subdomain. This is the part that Gobuster will fill in with each entry of the configured wordlist.
- `.example`: This is the second-level domain. You can configure this with the `--domain` flag (this needs to be configured together with the top-level domain).
- `.thm`: This is the top-level domain. You can configure this with the `--domain` flag (this needs to be configured together with the second-level domain).

Now that we know how Gobuster sends its request, let's break down the command and examine each flag more closely:  

- `gobuster vhost` instructs Gobuster to enumerate virtual hosts.
- `-u "http://MACHINE_IP"` sets the URL to browse to MACHINE_IP.
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` configures Gobuster to use the _subdomains-top1million-5000.txt_ wordlist. Gobuster appends each entry in the wordlist to the configured domain. If no domain is explicitly configured with the `--domain` flag, Gobuster will extract it from the URL. E.g., _test.example.thm_, _help.example.thm_, etc. If any subdomains are found, Gobuster will report them to you in the terminal.  
    
- `--domain example.thm` sets the top- and second-level domains in the `Hostname:` part of the request to _example.thm._  
    
- `--append-domain` appends the configured domain to each entry in the wordlist. If this flag is not configured, the set hostname would be _www_, _blog_, etc. This will cause the command to work incorrectly and display false positives.
- `--exclude-length` filters the responses we get from the sent web requests. With this flag, we can filter out the false positives. If you run the command without this flag, you will notice you will get a lot of false positives like "Found: Orion.example.thm Status: 404 [Size: 279]" or  "Found: pm.example.thm Status: 404 [Size: 276]". These false positives typically have a similar response size, so we can use this to filter out most false positives. We expect to get a 200 OK response back to have a true positive. There are, however, exceptions, but it is not in the scope of this room to go deeper into these.