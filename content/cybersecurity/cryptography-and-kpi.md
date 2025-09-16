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

**Key length** is very different based on cryptosystem. A 1024bit RSA is equally safes as a 160-bit ECC.

### RSA
* Created in 1977 by Ronald **R**ivest, Adi **S**hamir, and Leanord **A**dleman.
* Initially proprietary, today public domain
* Based on factoring large prime numbers

### Elliptic Curve Cryptography (ECC)
* Created 1985 by Neal Koblits and Victor Miller
* It's harder to break, so you don't need such a long key length to get the same effect as with RSA.

## Hash Functions
* A hash can be called `message digest` can be used for
  * hash, hash value, hash total, CRC, fingerprint, checkstum, digital ID.
* Recalculating the hash and compare original message/provided hash.
  * Even the smallest difference results in a very different hash
* Digital Signature algorithm
* **5 Requirements**
  * Accept an input of any length
  * Produce an output of fixed length, unrelated to the input.
  * Relatively easy to compute
  * One way, can't be reversed
  * Collision Free

### SHA

* By NIST
* AKA Secure Hash Standard (SHS), AKA FIPS 180.
* **Secure Hashing Algorithm**
  * Successors: SHA-1, SHA-2, SHA-3
* SHA-1
  * Input of very high upper bound limit (like 2 000 000 terabyte)
  * Produces 160bit digest
  * Processes in 512 bit blocks, if a block can't be filled it's padded woth extra data.
  * SHA-1 has shown **weaknessess**, therefore SHA-2
* SHA-2
  * Generally secure, still similar SHA-1 weakness, so ideally SHA-3 to be used
  * 4 Variants
    * SHA-256 - 256 bit message digest - 512 bit block size
    * SHA-224 - 224 bit message digest - 512 bit block size - Truncated version of SHA-256
    * SHA-512 - 512 bit message digest - 1024 bit block size
    * SHA-384 - 284 bit message digest - 1024 bit block size - Truncated version of SHA-512
    * SHA-<digest_size> is general pattern

### MD5

* 128 bit message digest - 512 bit block size
* four distinct rounds of computatioin to product the message digest
* Researchers have found collision risk, so **don't use it for message integrity**

## Digital Signatures

* **Goals**
  * Assures the receiver, that the message truly came from the claimed sender.
  * Assures the receiver, that the messages was not altered.
* **Combined**
  * Goal 1: Public Key Cryptography
  * Goal 2: Hash Functions
* **How It Works**
  * 1. Alice `hashes` the `plaintext` and gets a `message digest` (e.g. SHA3-512)
  * 2. Alice `encrypts` the `message digest` with her `own private key` this result is the `digital signature`.
  * 3. Alice `appends` the `digital signature` to the `plaintext`.
  * 4. Alice `sends` the `appended plaintext` to BOB
  * Now bob needs to reverse that:
  * 1. Bob `decrypts` the `digital signature` with `Alice's public key` and has the `message digest`
  * 2. Bob now recalculated the `message digest` from the `plaintext`
  * 3. Bob now compares the `self calculated message digest` with the provided one.
    * Bob has verified now that Alice has sent this message, as claimed.
    * Bob has verified now that the messages was not altered.
  * **NOTE** there was no Privacy/confidentiallity, to do that:
    * Alices should `encrypt` the `appended plaintext` with `Bob's public key`, so at the end you encrypt the whole package. Else the original message is visible + the signature.
* **Example Use Cases**
  * Authenticate code that's distributed
  * Sent messages
  * ...

### HMAC

* **Hash-Based Message Authentication Code**
* **Provides integrity check, but not non-repudiation**
  * I know the message was not altered, cause in transit, the one who would alter it, doesn't have the secret to make sure the right hash value would be calcualted.
* **Formula**
  * Any hashing function
  * A private key
  * The `plaintext` + `private key` results in a `message digest` that can be only recalculated by anyone having the same `private key`.
* **Good for**
  * Speed & efficiency
* **Examples**
  * API Authentication:
    * The API Key (secret) is shared between the client and API.
    * Many messages/API calls are sent.
    * Only need to know message integrity (hash) and that it comes from Client X => `Message + secret`
    * Typical 1-1 communication, no 3th party of many people who will access this, compared to a digitally signed binary.

## Which Key Should I Use

* **When sending messages**
  * You `send and encrypt` - use `receivers public key` (cause there is only one specific individual that should be able to read it)
  * you `receive and decrypt` - use `own private key`
* **When digitally signing**
  * You `send and sign` - use `own private key` (cause now the receiver could be ANYONE, not a specific person, so better to share your public key so anyone can verify.)
  * You `receive and verify` - use `senders public key`.

## Public Key Infrastructure (PKI)

* **A hierarchy of trust relationships.**
* **Combines** almost all cryptography elements.
  * Assymetric cryptography
  * Symmetric cryptography
  * Hashing
  * Digital Certificates (~ Digitan Signatures-ish)

### Certificates

* **Assurance that people you are communicating with are trulu who they claim to be** - Authentication
  * ***endoresed*** copies of an indivuals ***public key*** (We endorse this public key can be trust and is of person x)
  * Done by verifying that a certificate was signed by a Trusted Certificate Authority (CA), they know the public key is legitimate.
    * Cause the public key is good for someone to send a private message to that one person, but therefore we don't know if that person is who they claim to be (authentication).
* **X.509** is a container/format standard for certificates
  * Attributes
    * `X.509` version
    * `Serial Number` from the certificate creator
    * `Signature Algorithm Identifier` what algorithm was used to sign the signature (so others can verify)
    * `Subjects Issuer Name` of the CA that issues this certificate.
    * `Validity Period` specifying a start and end date.
    * `Common Name (CN)` that states the certificate owner (e.g. `ian.com` or `blog.ian.com`)
      * wildcards for first level subdomains `e.g. *.ian.com`
    * \[Optional\] `Subject Alternative Names (SANS)` that specify additional items (IP Addresses, domain names, ...)
    * `Subjects Public Key` the actual public key
  * Version 3
    * Supports extensions/customized variables containing data (metadata) from the CA
    * Examples
      * A signing key used by CA for the certificate
      * Email Addresses
      * Use signature only for signing, to encryption
      * ...

### Certificate Authorities (CA)

* Neutral organizations that act as a "notary" for digital services.
* To get a certificate you have to identify with these notaries
* Examples: IdenTrust, Amazon Web Services, DigiCert Group, GlobalSign, Let's Encrypt, GoDaddy
* Anyone can start an CA, if you don't know the CA, don't trust anything they issue.
* Browsers come preloaded with ahh the major CA's their root certificats.
* **Registration Authorities** - Assist CA's with virifying user's identities before they get a certificate issued. Basically an identity verification authority/service/
* **Root Certificate** - The core/top level certificate of a CA, which is usally **kept offline** (if this is compromised, all the children are)
* **Intermediate Certicificate** - **kept online** to serve as the online CA and to issue certificates routinely.
* **Certificate Chaining** - Certificates create certificates for others, and those others could then create certificates from there, creating a trust chain of certificates.
  * A browser should validate all certicicates in the chain.
* **CA's dont need to be third party** - You can be a CA for your own organization and use it to create certificates across your oganization, it will only not be trusted by externals that visit your site, but for that you can use a third party one. This saves money and time.

### Certificate Generation and Destruction

* **Enrollment**
  * Prove your Identity to CA - Appear in person, organizational documentation, etc..
  * `Certificate Signiung Request (CSR)` which is your raw public key.
  * The CA creates a X.509 certificate and signs it with CA's private key.
  * Distribute your certificate
  * Based on the identity verification it can issue different certicite types:
    * **Dommain Validation (DV)** - Yes, the subject has control over the domain
    * **Extended Validation (EX)** - Yes, the subjet is a legitimate business
* **Verification**
  * First you verify a certificate with the public key of the CA.
  * Then you check if the certificate is not on **Certificate Revocation List (CRL)** or **Online Certificate Status Protocol (OCSP)**
  * Now we can assume it's *authentic* if it checks
    * Digital Signature of CA is authentic
    * You trust the CA
    * Certificate not liste on CRL or OSCP
    * Certificate contains the data you're trusting.
      * Example: If certifcate only contains the email of a user but not the full name, you cab only trust the email.
  * **Certificate Pinning** - Hard-coding which specific certificate (or CA) your application will trust, rather than trusting the entire OS certificate store.
* **Revocation**
  * Request Grace Period - Max response time to which a CA will peform a revocation.
  * Certicicate Practice Statement (CPS) - The detailed operational manual that describes exactly how a Certificate Authority runs its business.
  * Reasons
    * Certificate was compromised (private key leaked)
    * Certificate erroneously issued
    * Details of certificate changed
    * Security association changed (user left the organization)
  * Techniques
    * **Certificate Revocation List (CRL)** - Maintained by the CAs
      * Contains all serial numbers of issued and also revoked with the date and time of revocation.
      * Requires to be downloaded/cross-checked periodically, causes latency
    * **Online Certificate Status Protocol (OCSP)**
      * Fast/realtime
      * When you get a certificate, send an OCSP request to the CA's OCSP server and you get "good", "revoked" or "unknown" status.
      * Huge burden on OCSP servers
    * **Certificate Stapling**
      * Extension to OCSP
      * The server sends it's certificate with the "Stapled" OCSP response
      * Browser can then verify the stappled OCSP response
      * A timestamp is included, to make sure the OCSP response is recent enough
      * This mostly helps if you have many concurrent users, so then there is only one OCSP request for all those users for a given time interval.

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
