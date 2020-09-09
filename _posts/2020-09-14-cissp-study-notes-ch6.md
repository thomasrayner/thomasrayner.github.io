---
layout: post
title: CISSP Study Notes Chapter 6 - Cryptography and Symmetric Key Algorithms
date: 2020-09-14 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 6 covers data security controls, understanding data states, and then it gets into cryptography. This chapter goes into assessing and mitigating vulnerabilities of systems related to cryptography, cryptographic lifecycle and methods, nonrepudiation, and data integrity.

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

## Chapter 6: Cryptography and Symmetric Key Algorithms

### My key takeaways and crucial points

#### Historical Milestones in Crypto

* *Caesar cipher* - Shift each letter of the alphabet 4 places to the right. A becomes D, B becomes E, etc..
  * Cracked via *frequency analysis* - Most common English letters are E, T, A, O, N, R, I, S, H. Attackers find the common substitutions and experiment until they can discern the message.

#### Crypto Basics

* Goals of Crypto
  * Confidentiality
    * Preservation of secrecy of stored information
    * *Symmetric* crypto systems use a secret key shared by all users
    * *Asymmetric* crypto systems use individual combos of public and private keys for each user
    * *Data in transit* aka *data on the wire* - exam terms, same thing
  * Integrity
    * *Message digests* - aka *digital signatures*, created when message is transmitted, used to ensure data wasn't altered
  * Authentication
    * Challenge-response authentication
    * Prove that one can encrypt/decrypt something to validate identity
  * Nonrepudiation
    * Only offered by asymmetric systems
    * Assurance that the message originated by the sender, not someone pretending to be the sender
* Cryptography Concepts
  * *Plaintext* - Before a message is coded
  * *Ciphertext* - After a message is encrypted
  * *Keys* - Used in encryption calculations.
  * *Key space* - The range of values that are valid for use as a key in a specific algorithm, aka *bit size*
  * **Kerckhoff's Principle** - A Cryptographic system should be secure even if everything about the system, except the key, is public knowledge
  * *Cryptovariable* - Sometimes used to refer to keys
  * *Cryptography* - Implementing secret codes and ciphers
  * *Cryptanalysis* - The study of methods to defeat codes and ciphers
  * *Cryptology* - Cryptography and cryptanalysis together

#### Cryptographic Mathematics

* Boolean Math - Logical Operations
  * *AND* - Represented by the `^` symbol, checks whether two input values are both true
  * *OR* - Represented by the `v` symbol, checks whether at least one input value is true
  * *NOT* - Represented by the `!` symbol, reverses the value of an input variable
  * *XOR* - Represented by the `⊕` symbol, returns true when only one of the input values is true
* *Modulo function* - showing a remainder value each time you performed a division operation, very important to crypto operations
* *Nonce* - A random number that acts as a placeholder variable in mathematical functions
* *Zero-Knowledge Proof* - Prove your knowledge of a fact to a third party without revealing the fact itself to the third party
* *Split knowledge* - Knowledge is divided among multiple users
  * *M of N control* - Requires a minimum (M) number of the total agents (N) work together to perform a high-security action
* *Work function* - Measures the strength of a crypto system
  * Time and effort required to complete a brute-force attack
  * Work function only needs to be slightly greater than the time value of the asset

#### Codes vs. Ciphers

* *Codes* - Crypto systems of symbols that represent words or phrases, sometimes secret, not always meant to provide confidentiality
  * Ex: "The eagle has landed"
* *Ciphers* - Always meant to hide the true meaning of a message
  * Ex: The transformation of plaintext to ciphertext

#### Transposition Ciphers

* *Transposition cipher* - Use an encryption algorithm to rearrange the letters of a plaintext message to form ciphertext
* Can used a keyword to perform a *columnar transposition*

#### Substitution Ciphers

* *Substitution cipher* - Use an encryption algorithm to replace each character or bit of the plaintext with a different character
* *Vigenère cipher* - Uses a chart of the alphabet shifted once per line, then a key is used to decrypt

#### One-Time Pads

* *One-time pads* - Use a different substitution alphabet for each letter of the plaintext message
* AKA *Vernam ciphers*
* One-time pad must be randomly generated
* Most be physically protected against disclosure
* OTP must be used only once
* Key must be at least as long as the plaintext
* When used properly, OTP is unbreakable - no repeating patterns

#### Running Key Ciphers

* *Running key cipher* - aka a *book cipher*
* Key is as long as the message itself, often chosen from a common book

#### Block Ciphers

* *Block ciphers* - Operate on chunks or blocks of a message

#### Stream Ciphers

* *Stream ciphers* - Operate on one character or bit of a message (or data stream) at a time

#### Confusion and Diffusion

* *Confusion* - Occurs when the relationship between plaintext and the key is too complicated for an attacker to altering the plaintext and analyzing the ciphertext to determine the key
* *Diffusion* - Occurs when a change in the plaintext results in multiple changes throughout the ciphertext
* Substitution introduces confusing
* Transposition introduces diffusion

#### Modern Crypto

* Crypto keys
  * *Kerckhoff's Principle* - Opening algorithms to public scrutiny actually improves their security
  * Modern cryptosystems rely on secrecy of one or more cryptographic keys
* Symmetric Key Algorithms
  * AKA *secret key* and *private key* crypto
  * Rely on a shared secret
  * Weaknesses
    * Need to distribute the key - See *Diffie-Hellman*
    * Does not implement nonrepudiation
    * Algo doesn't scale well - secure private comms between individuals can only be achieved if every possible combo of users has their own shared key
      * (n * (n - 1)) / 2 = number of keys needed
    * Keys need to be regenerated every time group membership changes
  * Very fast
* Asymmetric Key Algorithms
  * AKA *public key* algos
  * Each user has two keys
    * *Public key* - Shared with all users
    * *Private key* - Kept secret, known only to the user
  * Supports digital signing
  * Transience - new users requires only one new public-private key pair, users can be easily removed
  * Only need to regenerate keys when a user's private key is compromised
  * Can provide integrity, authentication, nonrepudiation
  * Simple key distribution
  * No pre-existing communication link needs to exist
  * Big disadvantage is slow speed of operation
  * Lots of applications use a asymmetric crypto to establish a connection, and exchange a symmetric secret, then the rest of the session is encrypted with symmetric crypto

#### Symmetric Cryptography

* Data Encryption Standard
  * No longer considered secure
  * Superseded by Advanced Encryption Standard (AES)
  * Uses a long series of XOR operations, repeated 16 times (aka 16 rounds of encryption)
  * 56 bit key size
  * Electronic Code Book Mode - ECB
    * Weakest mode
    * 64 bit blocks processed
    * The same block of input produces the same encrypted block
    * Only for exchanging small amounts of data
  * Cipher Block Chaining Mode - CBC
    * Each block of plaintext is XORed with the preceding block of ciphertext before it's encrypted with DES
    * CBC has an initialization vector and XORs it with the first block of the message - IV must be sent to recipient
    * Errors propagate
  * Cipher Feedback Mode - CFB
    * Streaming cipher version of CBC
    * Operates against data produced in real time
    * Uses a memory buffer instead of block size
    * Uses an IV and chaining
  * Output Feedback Mode - OFB
    * Almost the same as CFB, except instead of XORing an encrypted version of the previous ciphertext, it's XORed with a seed value
    * Still uses an IV to create the seed value
    * Future seeds are derived by running DES on previous seed
    * No chaining function, so transmission errors don't propagate
  * Counter Mode - CTR
    * Stream cipher similar to CFB and OFB
    * Uses a simple counter that increments for each operation
    * Errors do not propagate
    * Well suited for use in parallel computing
* Triple DES
  * Effective key = 64 bit
  * 64 bit block size
  * Four versions
    * Encrypt plaintext 3 times using 3 different keys
      * Effective key size of 112 bits
    * Uses three keys, but replaces the second encryption with a decryption operation
    * Only uses two keys
    * Uses two keys, and uses a decryption operation in the middle
* International Data Encryption Algorithm
  * Key is broken up in a series of operations into 52 16-bit subkeys
  * Same 5 modes as DES
  * Used in *PGP* - Pretty Good Privacy
* Blowfish
  * 64-bit blocks of text
  * Keys between 32 bits and 448 bits
  * Much faster than DES and IDEA
  * Released for public use with no license
* Skipjack
  * US Government
  * 64-bit blocks of text
  * 80-bit keys
  * Clipper and Capstone encryption chips - just know these are related to Skipjack
  * Supports escrow of encryption keys
  * Not widely embraced because of mistrust of escrow processes within US government
* RV5 - Rivest Cipher 5
  * Block sizes - 32, 64, 128 bits
  * Key sizes - between 0 and 2040 bits
* Advanced Encryption Standard - AES
  * 128-bit keys require 10 rounds of encryption
  * 192-bit keys require 12 rounds of encryption
  * 256-bit keys require 14 rounds of encryption
* Twofish
  * *Prewhitening* - XORing the plaintext with a separate subkey before the first round of encryption
  * *Postwhitening* - Uses a similar operation after the 16th round of encryption

> There is a table (6.2) that I won't reproduce here that you should familiarize yourself with before your exam

#### Symmetric Key Management

* Creation and distribution
  * Offline - physical distribution
  * Use public key encryption to setup an initial communications link, exchange a secret key over the secure public key link
  * Diffie-Hellman
* Storage and destruction of keys
  * Never store keys on the same system as encrypted data
  * Sensitive keys can be split up and then *split knowledge* can be used
* Key escrow and recovery
  * *Fair cryptosystems* - Secret keys used in communication are divided into two or more pieces, each of which is given to an independent third party
  * *Escrowed encryption standard* - Provides the government with a technological means to decrypt ciphertext - used in Skipjack

#### Cryptographic Lifecycle

* *Moore's Law* - except One-Time Pad, all crypto systems have a limited life span
  * A cited trend in the advancement of computing power that states the processing abilities of a microprocessor will double approximately every two years
  * Not a law, just a previous trend
  * Means what is hard to crack today might not be hard to crack tomorrow - especially with quantum computing
