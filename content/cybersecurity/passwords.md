---
title: "Passwords"
---
# Passwords

## Advice
* **Best practices**
  * Show password to prevent typos, password managers, store secrets with salts and secure hashing methods, locking after multiple attempts and MFA
* **Guideliness** - [NIST 800-63](https://pages.nist.gov/800-63-3/)
  * Reduce password complexity requirements and instead emphasize length.
  * Not require special characters
  * Allow ASCII and Unicode
  * Allow pasting into passwords fields (for password managers)
  * Monitor new passwords to ensure that easily compromised ones are not used
  * Eleminate Password Hints
* **Recomendations**
  * Length is the best defense against brute force
  * Complexity - prevent repeated characters and common words
  * Reuse limitations
  * Expiration dates to force renewal
  * Age limitations - Sometimes people keep resetting till the "reuse" limitation is circumvented.
* **Password Managers**
  * Good stuff
  * [Lastpass Breach Recommendation](https://blog.lastpass.com/posts/security-incident-update-recommended-actions)
* **Passwordless**
  * Instead depending on `what you know` primarily, it focuses on `what you have` (security tokens, certificates,...)
  * An option: `hardware security key` (like UbiKey)
    * Protocols: FIDO, Universal 2nd Factor (U2F), ..
    * FIDO: Open Authentication Standard supporting W3C Web Authentication and Client to Authenticator Protocol (CTAP)
  * Goal is to remove friction

## Default Passwords
* [Online Database](https://cirt.net/passwords/)

## Password Attacks
### Brute-Force - Iterate through passwords until they find one that works
* This can include using lists with generic commonly used passwords or tailored to the target
* Many passwords attempts for a single user
### Password Spraying - a brute-force variation
* Few passwords attempts but for many users
* Example: On a sports fan website, most likely one user, uses the teams name or player as password
### Dictionairy Attacks - a brute-force variation
* Uses a distinct list of words
* Popular Tool: [John The Ripper](https://www.openwall.com/john/) and [Tutorials](https://openwall.info/wiki/john/tutorials)
* Envirment
* Online: Run and test passwords against life system with risk getting blocked/caught
* Offline: You have the hashes or offline copy and you can in all peace go at it.
  * For example a precomputed list of hashes (Rainbow table attack)
    * Hash salts and peper is used to counter rainbow table attack
