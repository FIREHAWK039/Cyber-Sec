
 `pwd`:  Where Am I
 `ls`:  What's Around Me
 `ls -l`: This lists the content of the current directory. If we need more details
 `ls -al`:  Hidden Files
 `cat`: Read the file
  
	 
 Hidden files aren't really `secret`; they start with a dot `.`, and Linux hides such files by default.

## Learn the Power of "Find"
 This built-in utility is used to locate files within the file system. Here's a simple version of the command: `find <starting_point> -name <filename>`. Since your supervisor mentioned that the file mission_brief.txt resides somewhere in your home directory, begin the home directory symbol: `~`. So we will run the command: `find ~ -name mission_brief.txt`, as shown below:

![](../../Attacments/Pasted%20image%2020260904193717.png)


`df -h`: check storage info

The `-h` means "human readable"; it shows sizes like 2G or 500M instead of long bytes-only numbers.

![](../../Attacments/Pasted%20image%2020260904194238.png)

**Breakdown of the Information**

- `/dev/root` is the main disk of the system with **--G total**, **12G used**, **<REDACTED>G free**, and is **17% full**.
- `tmpfs` entries are temporary filesystems stored in **RAM**, not on the physical disk.
- `/dev/shm` is a shared memory area with **1.9G** available and **0 used**.
- `/run/user/114` is similar temporary storage for another system user, also **387M total** and mostly empty.