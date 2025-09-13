# Password attacks

* **Brute-Force** - Iterate through passwords until they find one that works
  * This can include using lists with generic commonly used passwords or tailored to the target
  * Many passwords attempts for a single user
* **Password Spraying** - a brute-force variation
  * Few passwords attempts but for many users
  * Example: On a sports fan website, most likely one user, uses the teams name or player as password
* **Dictionairy Attacks** - a brute-force variation
  * Uses a distinct list of words
* Popular Tool: [John The Ripper](https://www.openwall.com/john/) and [Tutorials](https://openwall.info/wiki/john/tutorials)
* Envirment
  * Online: Run and test passwords against life system with risk getting blocked/caught
  * Offline: You have the hashes or offline copy and you can in all peace go at it.
    * For example a precomputed list of hashes (Rainbow table attack)
      * Hash salts and peper is used to counter rainbow table attack
