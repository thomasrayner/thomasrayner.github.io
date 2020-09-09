---
layout: post
title: CISSP Study Notes Chapter 7 - PKI and Cryptographic Applications
date: 2020-09-16 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 7 is all about applying cryptography. It covers the cryptographic lifecycle, methods, Public Key Infrastructure, and key management practices. It also covers Digital signatures, nonrepudiation, integrity, cryptanalytic attacks, and Digital Rights Management.

Last summer I spent about a month studying for and getting my Certified Information Systems Security Professional (CISSP) certification from ISC2. I went about studying for the test a few ways:

* I used the PocketPrep app
* I attended a study bootcamp
* I did a bunch of practice tests

And finally...

* I got the ISC2 CISSP official study guide - I read it cover to cover, and highlighted and annotated the entire thing.

[Twitter (@MrThomasRayner)](https://twitter.com/mrthomasrayner) told me there is interest in seeing my study notes. So, here we go! Welcome to my 21 part series on the takeaways and crucial points from each chapter in the ISC2 CISSP official study guide. To be clear, this isn't a replacement for all those other study methods I mentioned above. This is just a supplement. This also isn't *everything* you need to know for the test. This is just what I feel are the most important points.

> It's important to remember that while many of these terms and phrases have different meanings in different contexts, the definitions I'm providing below are the ones that are relevant in the CISSP exam. Your own training or experience may tell you that a definition is incorrect or invalid, but if you want to get the exam questions right, you'll have to know them as they're defined in the books and study material.

The CISSP exam is often said to be "a mile wide but only an inch deep" which means you need to know a little bit about **a lot of stuff**. Accordingly, these posts contain **a lot of points** and while you might not be questioned on all of them, you could be questioned on any of them. It's important to have a good grip on *every chapter* in its entirety.

## Previous Chapters

* [Chapter 1: Security Governance Through Principles and Policies](/cissp-study-notes-ch1)
* [Chapter 2: Personnel Security and Risk Management Concepts](/cissp-study-notes-ch2)
* [Chapter 3: Business Continuity Planning](/cissp-study-notes-ch3)
* [Chapter 4: Laws, Regulations, and Compliance](/cissp-study-notes-ch4)
* [Chapter 5: Protecting Security of Assets](/cissp-study-notes-ch5)
* [Chapter 6: Cryptography and Symmetric Key Algorithms](/cissp-study-notes-ch6)

## Chapter 7: PKI and Cryptographic Applications

### My key takeaways and crucial points

#### Public and Private Keys

* Every user maintains a public key and a private key in asymmetric crypto
* Private key is preserved for the sole use of the individual who owns the key
* Public key is available to anyone they want to communicate with
* RSA
  * Choose two large prime numbers approximately 200 digits each labeled `p` and `q`
  * Multiply them together `n = p * q`
  * Select a number `e` that is:
    * Less than `n`
    * `e` and `(p - 1)(q - 1)` are relatively prime (no common factors)
  * Find `d` that is `(ed - 1) mod (p - 1)(q - 1) = 1`
  * Distribute `e` and `n` as the public key and keep `d` as the secret private key
* Key length is the most important parameter
  * RSA key length: 1024 bits
  * DSA key length: 1024 bits
  * Elliptical curve key length: 160 bits
* El Gamal
  * Major disadvantage - this algo doubles the length of any message it encrypts
* Elliptical Curve
  * Better for low power devices like phones
  * 1024 bit RSA key is cryptographically equivalent to 160 bit elliptical curve

#### Hash Functions

* *Hash functions* - Take a potentially long message and generate a unique output value derived from the content of the message
  * *Message digest* - The output of a hash function
* Basic hash function requirements
  * Input can be any length
  * Output has a fixed length
  * Should be relatively easy to compute for any input
  * Hash function is `one-way` which means it is extremely hard to determine the input when provided the output
  * Collision free - hard to find two inputs that produce the same message digest
* SHA - Secure Hash Algorithm
  * SHA-1 produces 160 bit digest
  * Processes 512 bit blocks
  * Pads messages to fit
  * SHA-256 produces 256 bit messages using 512 bit block size
  * SHA-224 uses truncated version of SHA-256 hash to make a 224 bit message with 512 bit block size
  * SHA-512 produces 512 bit message digests using a 1024 bit block size
  * SHA-384 uses truncated SHA-512 to produce 384 bit digest with 1024 bit block size
* MD5
  * 512 bit blocks
  * 4 distinct rounds of computation
  * Message length must be 64 bits less than a multiple of 512 bits
    * Uses padding to make up the difference
* Hash of Variable Length (HAVAL) - MD5 variant
  * Hash value length: 128, 160, 192, 224, 256 bits

#### Digital Signatures

* Enforces nonrepudiation
* Assures the recipient that the message was not altered while in transit
* If Alice wants to sign a message she's sending to Bob...
  * Alice generates a message digest of the original plaintext using a hashing algo
  * Alice encrypts the message digest using her private key - this is the digital signature
  * Alice appends the signed message digest to the plaintext
  * Alice transmits the appended message to Bob
  * Bob decrypts the digital signature using Alice's public key
  * Bob uses the same hashing function to create a message digest of the full plaintext received from Alice
  * Bob compares the decrypted message digest he got from Alice with the message digest he computed himself
    * If the hashes match, the signature is verified and the message was sent from Alice
    * If the hashes do not match, the signature is invalid and either the message didn't come from Alice, or it was modified in transit
* Does not provide privacy/confidentiality
* Does provide integrity, authentication, nonrepudiation
* HMAC - Hashed Message Authentication Code
  * Provides integrity, does not provide nonrepudiation
  * Depends on a shared secret key

#### Which Key To Use When

| If you want to | Use this key |
|----|----|
| Encrypt a message | Recipient's public key |
| Decrypt a message sent to you | Your private key|
| Digitally sign a message you are sending to someone else | Your private key |
| Verify the signature on a message sent by someone else | Sender's public key |

#### Digital Signature Standard

* Federal Information processing Standard (FIPS) 186-4

#### Public Key Infrastructure

* Certificates
  * Endorsed copies of a public key
  * International standard: X.509
  * Contains
    * Version of X.509 it conforms to
    * Serial number
    * Signature algo identifier
    * Issuer name
    * Validity period
    * Subject's name
    * Subject's public key
  * Certificate extensions are custom variables inserted into a certificate
* Certificate Authorities
  * Neutral organizations that offer notarization services for digital certificates
  * Registration authorities assist by verifying user's identities prior to issuing certificates but do not issue certs themselves
  * *Certificate Path Validation* - CPV. Each certificate in the certificate path from the original start or root of trust down to the server or client in question is valid and legitimate.
* Certificate Generation and Destruction
  * Enrollment
    * Prove your identity to the CA
    * Provide them your public key
    * CA signs your certificate with their private key
  * Verification
    * Verify the cert by checking the CA's digital signature using the CA's public key
    * Make sure it was not revoked (Certificate Revocation List - CRL)
      * Or Online Certificate Status Protocol (OCSP)
