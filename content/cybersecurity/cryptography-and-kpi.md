# Cryptography and the PKI

## An Overview of Cryptography

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

* **Cryptology** - 2 fields
  * **Cryptography** - Art of creating and implementing secret codes and ciphers.
  * **Cryptoanalysis** - The art of defeating codes and ciphers.

* **Plain text (P)** - The actual text
* **Ciphertext (C)** - The encoded version of your text
* **Algorithm** - The method/technique to obfuscate/encode the text.
* **Cipher** - The more specific implementation of the algoritm, li ke RSA with 2048-bit keys.
* **Cipher Suit** - A set of ciphers that a system (e.g. a browser, server, OS) supports.
* **Key (K)** - The key to encode/decode between the Ciphertext (C) and Plant Text (P) using a given Cipher.
  * Sometimes refered to as `cryptovariables`.

* **Kerckhoff's Principle** - A cryptographic system should be secured even if everything about the system, except the key, is public knowledge
  * Allows algorithms known and public - allowing for public scruteny and testing.
  * If you don't follow it, Kerckhoff argues you do `Security through Obscurity`
  * Note: Bit off an OSS argument.

### Cryptographic Keys

* **Key Space** - The range of values that are valid for a key for a given algorithm. (e.g. 0 - 100)
  * Usually the upperbound is a 2^N value, cause the lower boundary are all binary `0` and lower boundary are all `1` for that given key space (e.g. 128 bit).

### Ciphers

* Categories:
  * **Block Ciphers** - Chunks the message in fixed size blocks (e.g. 8 bytes) and applied the cipher to that block.
    * TLS is a good example, you will chunck a message in small blocks to send over the internet, so you cipher per block.
  * **Stream Ciphers** - Operate on a one character or bit of message at a time.
    * You can use this as a block cipher, by just waiting for a buffer of fixed block size to fill up before you then "flush" it.

## Modern Cryptography

* The longer a key, the harder (more compute power) it is to break it.
* The key length should always be longer than what is possible to break/calculate, this changes over time.

### Cryptographic Secrecy

* **Secret ciphers** - Don't make sense, better to have public scruteny
* **Columnar Transposition** - Has too many weaknesses and is therefore not used in modern secure communication.

### Symmetric Key Algorithms

* Also Known as:
  * **Secret Key Cryptography**
  * **Private Key Cryptography** - but confuses with Public/Private key pairs.
* Out-band-exchange
* Shared secret between all participants
* Pro: It's fast! So it works well in hardware implementations and "large data transfes*
  * This is why TLS communication first goes through assymetric to then create a symmetric session token.
* Con
  * **Key Exchange is a major problem** - How to securily shared this in advance?
    * Some secure online channel
    * Some offline, out-of-band exchange
  * **Does not implement non-repudiation**
  * **Not scalable** - Cause you need to provide this key to every new user. so it's a key exchange scaling problem.
  * **Keys regenerate often** - When someone should be excluded from communication, the key needs to be regenerated and redistributed again.

### Asymmetric Key Algorithms

* Also Known as:
  * **Public Key Algorithms**
* In-band-exchange
* If the public key encrypts, only the private key can decrypt
* If the private key encrypts, only the public key can decrypt
* Can also support digital signature technologies
* Pro:
  * **Key Exchange is simple** - you can share your public key over a insecure schannel
  * **Scales well**
    * Adding one user requires generating only one new public/private key pair.
  * **Little to regenerations**
    * Users can be removed by a simple key recovation system.
    * When a private key is compromised, only that key needs to be regenerated.
  * **Multi-Purpose**
    * Confidentiality
    * Integrity
    * Authentication
    * Non-Repudiation
  * **No preexisting communication links needs to exist**
* Con
  * It is slow (slower than symmetric)

### Hashing Algorithms

* Message digestg - summary of a message in hash.
* **Collisions** - When 2 different inputs results in identical hash

## Common Symmetric Cryptography Systems

### Data Encryption Standard (DES)
* From US Government (1977) - Not secure anymore
* 3DES used the algorithm with 3 different keys - Still considered insecure and expired

### Advanced Encryption Standard (AES)
* By NIST (National Institute of Standards and Technology)
* Rijndael Block cipher
* Key Strengths:
  * 128 bits - 10 rounds of encryption
  * 192 bits - 12 rounds of encryption
  * 256 bits - 14 rounds of encryption
* Block Size: 128 bit

### Symmetric Key Management

* Security practices to protect keys.
* **Creation and Distribution** - How do we exchange these keys securely ?
  * _*Offline Distribution*_ - Via a hardware format (paper, ubikeys, ...), but that's sensitive to many risks
  * _*Public Key Encryption*_ - Like TLS, do first public/key handshake, agree a key and then proceed with a symmetric key (e.g. a session token for TLS). Come with some benefits to also authenticate and so before exchanging the key.
  * _*Diffie-Hellman*_ - When hardware is not possible and PKI is missing.
    * Allows two parties to establish a shared secret over an insecure channel
    * Foundation for many secure protocols
    * Uses asymmetric crypto principles but creates symmetric keys
    * more info see page `210` of the CompTia Security+ study book.
* **Storage and Desctruction**
  * Never store en cryption key on same system where the encrypted data resides
  * _*SPlit Knowledge*_ 2 people with each half of the key
    * When one leaves, do regeneration
* **Key Escrow and Recovery**
  * What if the key is forgotten/lost or the one who encrypted it leaves?
  * **Key Escrow** - A third party store a protected copy of these keys and follow a _key recovery_ policy to request a lost key.

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
