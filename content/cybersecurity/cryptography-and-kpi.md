# Cryptography and the PKI

## An Overview of Cryptography

* Plain text - The actual text
* Ciphertext - The encoded version of your text
* Cipher - The method/technique to obfuscate/encode the text.
* Cryptology -  The overarching science, and cryptography is its key component for creating secure systems
* Steganography - Hide messages in plane sight using cryptograhic techiques in anohter file
  * Images, text, audio, video, etc...
  * Can be also used for watermarking
  * [OpenStego](https://www.openstego.com/)

## Goals of Cryptography
There are 4 fundamental goals of cryptography

### Confidentiality
* Most cited goal of cryptography
* Ensure data is private when
  * At-Rest
    * Susceptible to theft of physical drives
    * Options:
      * **Encrypting Data on Disk**
        * *Full-disk encryption (FDE)* - All data is automatically encrypted
          * Protects against physical theft
          * Does not work once the system us booted, so at run time it doesn't do much.
        * *Partition encryption* - Same as FDE but targets a partition
          * Good for dual boot systems with senstive data.
        * *File-Level encryption* - On file level, bit less secure (as secure and non secure files can coexist)
        * *Volume encryption* - A "volume" like a set of files/folders
          * Middle ground between Partition and File encryption.
      * **Encrypting Database Data**
        * Database-level encryption - protect from access by unauthorized individuals
          * *Transparent Data Encryption (TDE)*  - Encrypt eentire database
          * *Column-Level Encryption (CLE)* - Encrypt specific columns within tables
        * Record-level encryption - Encrypts specific record
          * Where a table is shared between different users with other level of permission.
  * In-Transit (aka "data on the wire")
    * Susceptible to eavesdropping
    * TLS is most mainstream
  * In-use
    * Susceptible to aunauthorized processes
* 2 Types
  * Symmetric cryptosystems - One shared key for all users of the system
  * Assemtric cryptosystems - public/private keys for each user of the system
* Obfuscation - Related but not the same
  * Used to make it intentionally difficult for humans to understand how code works. Typical for IP.

### Integrity

* Protect against intentional (editted) and unintentional (bit rot) alterations
* Examples
  * Digital Signatures (Symmetric and Assymetric)
    * Symmetric (HMAC - Hash-based Message Authentication Code) -> Your input to the hash is the plaintext + a shared secret, so the received can recalculate the hash, as they have the same secret.
    * Assymetric
      * You sign with a private key, and the receiver verifies with a public key, but also used for **authentication**. 2-in-1.
  * Hash Functions - But anyone can recalculate the hash, in case the hash function and input params are known

### Authentication

* Verifies the claimed identity between users.
  * Proof who you are, but not used to state if you did something or not.
  * With a password you can claim it was stolen, but it wasn't.

### Non-repudiation

* The receiver can verify that a message was sent by the actuel sender, not someone impersonating.
  * Sender signs with private key
  * Receiver validates with public key
* _Prevents the sender from claiming they never sent the message (repudiating)._
* Can only be done with assymetric encryption.

## Cryptographic Concepts
### Cryptographic Keys
### Ciphers
## Modern Cryptography
### Cryptographic Secrecy
### Symmetric Key Algorithms
### Asymmetric Key Algorithms
### Hashing Algorithms
## Symmetric Cryptography
### Data Encryption Standard
### Advanced Encryption Standard
### Symmetric Key Management
## Asymmetric Cryptography
### RSA
### Elliptic Curve
## Hash Functions
### SHA
### MD5
## Digital Signatures
### HMAC
## Public Key Infrastructure
### Certificates
### Certificate Authorities
### Certificate Generation and Destruction
### Certificate Formats
## Asymmetric Key Management
## Cryptographic Attacks
### Brute Force
### Frequency Analysis
### Known Plain Text
### Chosen Plain Text
### Related Key Attack
### Birthday Attack
### Downgrade Attack
### Hashing, Salting, and Key Stretching Exploiting Weak Keys Exploiting Human Error
## Emerging Issues in Cryptography
### Tor and the Dark Web
### Blockchain
### Lightweight Cryptography Homomorphic Encryption
### Quantum Computing
