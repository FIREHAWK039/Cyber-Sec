
Gobuster is an open-source offensive tool written in Golang. It enumerates web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage by brute force, using specific wordlists and handling the incoming responses. Many security professionals use this tool for penetration testing, bug bounty hunting, and cyber security assessments. Looking at the phases of ethical hacking, we can place Gobuster between the reconnaissance and scanning phases.

- Open up a terminal on the the AttackBox and enter the command: `sudo nano /etc/resolv-dnsmasq`.
- Insert `nameserver MACHINE_IP` as the first line.
- Save the file by pressing CTRL+O, followed by pressing ENTER, and then exit the editor by pressing CTRL+X.
- Enter the command `/etc/init.d/dnsmasq restart` to restart the Dnsmasq service.

The file should look something like this:

```shell-session
root@tryhackme:~# cat /etc/resolv-dnsmasq 
nameserver MACHINE_IP
nameserver 169.254.169.253
```



Before exploring Gobuster, let’s briefly discuss the concepts of enumeration and Brute Force.

**Enumeration**

Enumeration is the act of listing all the available resources, whether they are accessible or not. For example, Gobuster enumerates web directories.

**Brute Force**

Brute force is the act of trying every possibility until a match is found. It is like having ten keys and trying them all on a lock until one fits. Gobuster uses wordlists for this purpose.

## Gobuster: Overview

Gobuster is included by default in distributions like Kali Linux. Let’s start by looking at Gobuster’s help page. This help page gives us a good overview of its functionalities and options.

Enter the following command: `gobuster --help`. You should get the help page for the Gobuster tool as shown below:

AttackBox Terminal

```shell-session
root@tryhackme:~# gobuster --help
Usage:
  gobuster [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
  gcs         Uses gcs bucket enumeration mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  tftp        Uses TFTP enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)

Flags:
      --debug                 Enable debug output
      --delay duration        Time each thread waits between requests (e.g. 1500ms)
  -h, --help                  help for gobuster
      --no-color              Disable color output
      --no-error              Don't display errors
  -z, --no-progress           Don't display progress
  -o, --output string         Output file to write results to (defaults to stdout)
  -p, --pattern string        File containing replacement patterns
  -q, --quiet                 Don't print the banner and other noise
  -t, --threads int           Number of concurrent threads (default 10)
  -v, --verbose               Verbose output (errors)
  -w, --wordlist string       Path to the wordlist. Set to - to use STDIN.
      --wordlist-offset int   Resume from a given position in the wordlist (defaults to 0)

Use "gobuster [command] --help" for more information about a command.
```

The help page contains multiple sections:

- **Usage:** Shows the syntax on how to use the command.
- **Available Commands:** Multiple commands are available to aid us in enumerating directories, files, DNS subdomains, Google Cloud Storage buckets, and Amazon AWS S3 buckets. Throughout this room, we will focus on the `dir`, `dns`, and `vhost` commands. We will cover each of them in the following tasks.
- **Flags:** These are specific options we can configure to customize our commands. Let’s look at the flags we will often use throughout this room:
    
    |Short Flag|Long Flag|Description|
    |---|---|---|
    |`-t`|`--threads`|This flag configures the number of threads to use for the scan. Each of these threads sends out requests with a slight delay. The default number of threads is 10. This number may be slow when using large wordlists. You can increase or decrease the number of threads depending on the available system resources.|
    |`-w`|`--wordlist`|The flag configures a wordlist to use for iterating. Each wordlist entry is attached to the URL you included in the command.|
    ||`--delay`|This flag defines the amount of time to wait between sending requests. Some web servers include mechanisms to detect enumeration by looking at how many requests are received in a certain period of time. We can increase the delay between subsequent requests to make it look like normal web traffic.|
    ||`--debug`|This flag helps us to troubleshoot when our command gives unexpected errors.|
    |`-o`|`--output`|This flag writes the enumeration results to a file we choose.|
    

## Example

Let us look at an example of how we would use these commands and flags together to enumerate a web directory:

```
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```

- `gobuster dir` indicates that we will use the directory and file enumeration mode.
- `-u "http://www.example.thm/"` tells Gobuster that the target URL is [http://example.thm/(opens in new tab)](http://example.thm/).
- `-w /usr/share/wordlists/dirb/small.txt` directs Gobuster to use the _small.txt_ wordlist to brute force the web directories. Gobuster will use each entry in the wordlist to form a new URL and send a GET request to that URL. If the first entry of the wordlist were images, Gobuster would send a GET request to [http://example.thm/images/.(opens in new tab)](http://example.thm/images/)
- `-t 64` sets the number of threads Gobuster will use to 64. This improves the performance drastically.