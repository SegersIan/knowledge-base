# Streams and Networking
These are notes based on the Frontend Masters course by James Holiday (aka Substack).
Link [here](https://frontendmasters.com/courses/networking-streams/)

## Networking, servers, and clients

### Networking and Packets

* Servers and clients
  * Any networked computer can be a server
  * Aby networked computer can be a client
  These are roles rather.
* A payload is often broken up in multiple packets. Which you can receive out of order.

* TCP vs UDP
  * TCP : Reliable transport; If no ACK (acknowledged) came from the other end, we RESENT it.
  * UDP : Unreliable transport; Fire and forget, there is no confirmation from the other end if a packet was received.
    * Use case : Streaming audio/video (some use TCP now), games

### Protocols and Ports

Language that computes programs speak to each other, examples of protocols:

* HTTP - Browse web pages (port 80) 
* HTTPS - Browse web pages with encryption (port 443)
* SMPT - Send an receive emails (port 25)
* IMAP, POP3 - Load emails from an inbox
* IRC - Chat (port 6667)
* FTP - File transfer (port 21 for control)
* SSH - Remote shell over an encrypted connection (port 22)
* SSL - Low-level secure data transfer (used by HTTPS)

Most services have (often) one or many default ports. A computer can have many services, ports differentiate
between the services on a system. (range 1 - 65535). We can have a service listen to any port, but we have custom, 
default assignments.

* mysql - 3306
* postgresl - 5432
* couchdb - 5984

By default, systems can only listen to ports below 1024 as the root user.

### Servers and Clients

* A server means you are listening for incoming connections.
* Clients initiate the connections and connects to servers.
* P2P : This is a third role, aside of client and server. Here clients establish connections directly with other clients.
  There are no fixes servers.
  * Example is webrtc : Usually use for video and audio chat. Else you get latency if it all goes through a centralized server.

### Netcat

* Plain text server
* start server: `nc -l 5000`
* start client: `nc localhost 5000`
* Happy chatting

### HTTP and Headers

* HTTP : Hyper Text Transfer Protocol, how web servers and web browsers communicate.
* HTTP requests begin with a VERB
  * GET - Fetch document
  * POST - Submit a form
  * HEAD - Fetch metadata about a document
  * PUT - Upload a file
* Headers
  * Key value `key: value`, colon separated, space not mandatory
  * Example of creating a HTTP conform message
    ```
        $ nc google.com
        GET / HTTP/1.0
        HOST: google.com   --> A server might serve multiple domains, or LB.
    ```
* The format is a bit like this plain text snippet, notice the 2 returns before the body starts:
    ```
        VERB PATH HTTPVERSION
        HEADERS ...
        
        BODY ...
    ```
    and the response like
    ```
        HTTPVERSION STATUSCODE STATUSMESSAGE
        HEADERS ...
        
        BODY ...
    ```

### HTTP Post

Taken the following response
```
    HTTP/1.1 200 OK
    Date: Mon, 12 Jan 2015 06:37:51 GMT
    Connection: keep-alive
    Transfer-Encoding: chunked <- Gonna send body in chunks, send links for chunks. Server doesn't know in advance how long the response will be.
    
    3  <-- Hex value of the cuncked part
    oi <-- payload
    4  <-- Hex value of the cuncked part
    ok <-- payload
    
    0 <-- End, finished
```

### Curl

```
    $ curl -s http://substack.net        <-- Do GET and print body
    $ curl -i http://substack.net        <-- Print body and headers
    $ curl -I http://substack.net        <-- Print only headers
    # -s gets rid of progress output
    # Use -X ti set the HTTP VERB and -d for form paramters
    $ curl -X POST http://substack.net       
    $ curl -X POST http://substack.net -d title=whatever -d date=10000
    # You can set headers with the -H flag
    $ curl http://substack.net -H 'Content-Type: application/json'
    
```

### SMTP

* Similar to HTTP as it has status codes and such.
* Like HTTP, you have a first block with "headers", so all the metadata, from, to , subject, and then there is a body
  What we're actually sending. Body is ended with a line with only a `.` and new line.

### IRC

Another text based protocol. So HTTP, SMTP and IRC are all plain text protocols that just follow a certain text layout
and a port to listen on.

* IRC commands
  * nick - identify as a user
  * user - also identify as user
  * join - join a channel
  * privemsg - send a message to a channel
  
### Binary Protocols and Inspecting Protocols

* Test based protocols are easy to inspect with a sniffer and such
* With Binary protocols you can't messages plain text sadly. We need to write programs that unpack the incoming bytes,
  and pack the outgoing bytes according to given specification.
* Examples of binary
  * ssh (except from initial greeting)
  
* Inspecting protocols
  * For in/out local eth/wifi card
    * Wireshark for GUI
    * tcpdump for CLI 
      * `$ sudo tcpdump -X    --> start listening`;  
      * `$ sudo tcpdump -A    --> start listening with other formatting`;  
      * `$ sudo tcpdump 'tcp port 80' '-X     -> string contains a query/filter`;  

## Streams



## Stream Types

## Core Streams

## Web Socket

## Stream Modules

## Remote Procedure Call and Multiplex

## Wrapping up
