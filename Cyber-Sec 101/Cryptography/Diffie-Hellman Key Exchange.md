One of the challenges of using symmetric encryption is sharing the secret key. Let’s say you want to send a password-protected document to your business partner to discuss confidential business strategies. How would you share the password with them? It would be best if you had a secure channel to send the password, knowing that adversaries cannot read or alter it.

### Diffie-Hellman Key Exchange

**Key exchange** aims to establish a shared secret between two parties. It is a method that allows two parties to establish a shared secret over an insecure communication channel without requiring a pre-existing shared secret and without an observer being able to get this key. Consequently, this shared key can be used for symmetric encryption in subsequent communications.

Consider the following scenario. Alice and Bob want to talk securely. They want to establish a shared key for symmetric cryptography but don’t want to use asymmetric cryptography for the key exchange. This is where the Diffie-Hellman Key Exchange comes in.

Alice and Bob generate secrets independently; let’s call these secrets A and B. They also have some public common material; let’s call this C.

We need to make some assumptions. Firstly, whenever we combine secrets, they’re practically impossible to separate. Secondly, the order in which they’re combined doesn’t matter. Alice and Bob will combine their secrets with the common material to form AC and BC. They will then send these to each other and combine the received part with their secret to create two identical keys, both ABC. Now, they can use this key to communicate.

If you found the previous paragraphs too abstract, let’s investigate the exact process.

1. Alice and Bob agree on the **public variables**: a large prime number _p_ and a generator _g_, where 0 < _g_ < _p_. These values will be disclosed publicly over the communication channel. Although insecurely small, we will choose _p_ = 29 and _g_ = 3 to simplify our calculations.
2. Each party chooses a private integer. As a numerical example, Alice chooses _a_ = 13, and Bob chooses _b_ = 15. Each of these values represents a **private key** and must not be disclosed.
3. It is time for each party to calculate their **public key** using their private key from step 2 and the agreed-upon public variables from step 1. Alice calculates _A_ = _g__a_ mod _p_ = 313 mod 29 = 19 and Bob calculates _B_ = _g__b_ mod _p_ = 315 mod 29 = 26. These are the public keys.
4. Alice and Bob send the keys to each other. Bob receives _A_ = _g__a_ mod _p_ = 19, i.e., Alice’s public key. And Alice receives _B_ = _g__b_ mod _p_ = 26, i.e., Bob’s public key. This step is called the **key exchange**.
5. Alice and Bob can finally calculate the **shared secret** using the received public key and their own private key. Alice calculates _B__a_ mod _p_ = 2613 mod 29 = 10 and Bob calculates _A__b_ mod _p_ = 1915 mod 29 = 10. Both calculations yield the same result, _g__a__b_ mod _p_ = 10, the shared secret key.

![Diffie-Hellman Key Exchange](https://cdn-images.tryhackme.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1728439878360.svg)  

The chosen numbers are too small to provide any security, and in real-life applications, we would consider much bigger numbers.

Diffie-Hellman Key Exchange is often used alongside RSA public key cryptography. Diffie-Hellman is used for key agreement, while RSA is used for digital signatures, key transport, and authentication, among many others. For instance, RSA helps prove the identity of the person you’re talking to via digital signing, as you can confirm based on their public key. This would prevent someone from attacking the connection with a man-in-the-middle attack against Alice by pretending to be Bob. In brief, Diffie-Hellman and RSA are incorporated into many security protocols and standards to provide a comprehensive security solution.