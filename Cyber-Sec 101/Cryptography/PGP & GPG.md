**PGP** stands for Pretty Good Privacy. It’s software that implements encryption for encrypting files, performing digital signing, and more. [GnuPG or GPG(opens in new tab)](https://gnupg.org/) is an open-source implementation of the OpenPGP standard.

GPG is commonly used in email to protect the confidentiality of the email messages. Furthermore, it can be used to sign an email message and confirm its integrity.

Below is an example of generating GPG. You are asked about the purpose of using `gpg`, whether signing only or signing and encrypting. Besides selecting the cryptographic algorithm, we needed to choose an expiry date for the generated key. Finally, we provided some information about us: our name, email address, and a comment usually about the purpose of this key.

Terminal

```shell-session
gpg --full-gen-key
gpg (GnuPG) 2.4.4; Copyright (C) 2024 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card
Your selection? 9
Please select which elliptic curve you want:
   (1) Curve 25519 *default*
   (4) NIST P-384
   (6) Brainpool P-256
Your selection? 1
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: strategos
Email address: strategos@tryhackme.thm
[...]
pub   ed25519 2024-08-29 [SC]
      AB7E6AA87B6A8E0D159CA7FFE5E63DBD5F83D5ED
uid                      Strategos <strategos@tryhackme.thm>
sub   cv25519 2024-08-29 [E]
```

You may need to use GPG to decrypt files in CTFs. With PGP/GPG, private keys can be protected with passphrases in a similar way that we protect SSH private keys. If the key is passphrase protected, you can attempt to crack it using John the Ripper and `gpg2john`. The key provided in this task is not protected with a passphrase. The man page for GPG can be found online [here(opens in new tab)](https://www.gnupg.org/gph/de/manual/r1023.html).

Practi﻿cal Example

Now that you have your GPG key pair, you can share the public key with your contacts. Whenever your contacts want to communicate securely, they encrypt their messages to you using your public key. To decrypt the message, you will have to use your private key. Due to the importance of the GPG keys, it is vital that you keep a backup copy in a secure location.

Let’s say you got a new computer. All you need to do is import your key, and you can start decrypting your received messages again:

- You would use `gpg --import backup.key` to import your key from backup.key
- To decrypt your messages, you need to issue `gpg --decrypt confidential_message.gpg`


We have defined **cryptography** as the science of securing communication in the presence of adversaries. Another important science that studies how to break or bypass cryptographic systems is **cryptanalysis**. As for trying every possible password combination, we call that a **brute-force attack**. However, when we know that the password is most likely a dictionary word, it will make more sense to try words from a dictionary instead of every possible password combination; this is called a **dictionary attack**.

- **Cryptography** is the science of securing communication and data using codes and ciphers.
- **Cryptanalysis** is the study of methods to break or bypass cryptographic security systems without knowing the key.
- **Brute-Force Attack** is an attack method that involves trying every possible key or password to decrypt a message.
- **Dictionary Attack** is an attack method where the attacker tries dictionary words or combinations of them.