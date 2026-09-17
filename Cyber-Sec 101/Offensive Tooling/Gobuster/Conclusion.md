We have covered three different modes of the Gobuster tool:

- `dns` mode: enumerates dns subdomains.
- `dir` mode: enumerates directories.
- `vhost` mode: enumerates virtual hosts.

For each mode, we covered the required flags to configure and additional optional flags that fine-tune the desired results.

We have highlighted the difference between virtual hosts and subdomains and the way Gobuster scans for these:

- `dns` mode uses the DNS services to scan for subdomains using the configured domain and wordlist.
- `vhost` mode sends web requests using the configured URL and wordlist.