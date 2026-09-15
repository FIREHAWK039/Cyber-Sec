Throughout the tasks of this room, we will be using the following :

- The “Jumbo John” version of John the Ripper
- The RockYou password list

If you use the attached lab machine or the AttackBox, you don’t need to install John the Ripper on your system. Consequently, feel free to skip through the installation section. If you prefer to use your system to follow along, please read along to learn how to proceed with the installation. We should note that if you use a version of John the Ripper other than Jumbo John, you might not have some of the required tools, such as `zip2john` and `rar2john`.

## Installation

John the Ripper is supported on many Operating Systems, not just Linux Distributions. Before we go through this, there are multiple versions of John, the standard “core” distribution, and multiple community editions, which extend the feature set of the original John distribution. The most popular of these distributions is the “**Jumbo John**,” which we will use specific features of later.

**AttackBox and Kali**

Jumbo John is already installed on the attached lab machine and on the AttackBox, so if you plan to use either one, you need not take any further action. Furthermore, offensive Linux distributions like Kali are shipped with Jumbo John installed.

You can double-check this by typing `john` into the terminal. You should be met with a usage guide for John, with the first line reading “John the Ripper 1.9.0-jumbo-1” or something similar with a different version number.

**Other Linux Distributions**

Many Linux distributions have John the Ripper available for installation from their official repositories. For instance, on Fedora Linux, you can install John the Ripper with `sudo dnf install john`, while on Ubuntu, you can install it with `sudo apt install john`. Unfortunately, at the time of writing, these versions provided core functionality and missed some of the tools available through Jumbo John.

Consequently, you need to consider building from the source to access all the tools available via Jumbo John. The [official installation guide(opens in new tab)](https://github.com/openwall/john/blob/bleeding-jumbo/doc/INSTALL) provides detailed installation and build configuration instructions.

**Installing on Windows**

To install Jumbo John the Ripper on Windows, you need to download and install the zipped binary for either 64-bit systems [here(opens in new tab)](https://www.openwall.com/john/k/john-1.9.0-jumbo-1-win64.zip) or for 32-bit systems [here(opens in new tab)](https://www.openwall.com/john/k/john-1.9.0-jumbo-1-win32.zip).

## Wordlists

Now that we have `john` ready, we must consider another indispensable component: wordlists.

As we mentioned earlier, to use a dictionary attack against hashes, you need a list of words to hash and compare; unsurprisingly, this is called a wordlist. There are many different wordlists out there, and a good collection can be found in the [SecLists(opens in new tab)](https://github.com/danielmiessler/SecLists) repository. There are a few places you can look for wordlists for attacking the system of choice; we will quickly run through where you can find them.

On the AttackBox and Kali Linux distributions, the `/usr/share/wordlists` directory contains a series of great wordlists.

**RockYou**

For all of the tasks in this room, we will use the infamous `rockyou.txt` wordlist, a very large common password wordlist obtained from a data breach on a website called rockyou.com in 2009. If you are not using any of the above distributions, you can get the `rockyou.txt` wordlist from the [SecLists(opens in new tab)](https://github.com/danielmiessler/SecLists) repository under the `/Passwords/Leaked-Databases` subsection. You may need to extract it from the `.tar.gz` format using `tar xvzf rockyou.txt.tar.gz`.

Now that we have our hash cracker and wordlists all set up, let’s move on to some hash cracking!

To follow along, first, let’s start the **Lab Machine** by pressing the Start **Machine button** below.

The machine will start in **Split-Screen** view. In case the VM is not visible, use the blue **Show Split View** button at the top of the page.

	You can also access the lab machine using SSH at the IP address `MACHINE_IP` using the following credentials: