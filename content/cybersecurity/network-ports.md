---
title: "Common Network Ports"
---

# Commong Network Portds

| Unsecure protocol | Original port   | Secure protocol option(s) | Secure port   | Notes |
|-------------------|-----------------|---------------------------|---------------| --- |
| DNS   | UDP/TCP 53      | DNSSEC   | UDP/TCP 53                                       | |
| FTP   | TCP 21 (and 20) | FTPS     | TCP 21 (explicit mode) / TCP 990 (implicit mode) |  Using TLS |
| FTP   | TCP 21 (and 20) | SFTP     | TCP 22 (SSH)                                     | Using SSH |
| HTTP  | TCP 80          | HTTPS    | TCP 443                                          | Using TLS |
| IMAP  | TCP 143         | IMAPS    | TCP 993                                          | Using TLS, Fetching emails from server, stay in sync. |
| LDAP  | UDP/TCP 389     | LDAPS    | TCP 636                                          | Using TLS |
| POP3  | TCP 110         | POPS     | TCP 995 — Secure POP3                            | Using TLS, Fetching emails and delete on server |
| RTP   | UDP 16384–32767 | SRTP     | UDP 5004                                        | Real Time Protocol |
| SNMP  | UDP 161 and 162 | SNMPv3   | UDP 161 and 162                                 | Simple Network Management Protocol |
| Telnet | TCP 23          | SSH      | TCP 22                                         | Remote Access |
| SMPT   | TCP 25          | SMTPS over TLS | TCP 465                                  | Sending of emails |

## Less Common

* 515 - Network printing services (legacy)