---
bookCollapseSection: true
---
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

Node.js has a handy interface for shuffling data around called streams.

**Stream Origins**

>    We should have some ways of connecting programs like garden hose screw in another segment when it becomes
>    necessary to massage data in another way. This is the way of IO also.
>    Doug McIlroy, October 11, 1964

Thinks also of how we pipe in *nix systems between programs.

**Why Streeams?**

* We can compose streaming abstractions
* We can operate on data chunk by chunk

**Composition**

Just like how in unix we can pipe commands together, we can pipe streams together

```
    $ cat file > jq -name '.age'> ...
```

### Simple example

a nodejs equivalent what `$ cat` does.
```js
    const fs = require('fs');

    fs.createReadStream(process.argv[2])
      .pipe(process.stdout);
```

### Transform data Example
```js
    const fs = require('fs');
    const through = require('through2');

    fs.createReadStream(process.argv[2])
      .pipe(through(toUpper))
      .pipe(process.stdout);
    
    function toUpper(buf, enc, next){
        // buf is a binary description of the data
        // Output should be a buffer or string
        next(null, buf.toString().toUpperCase())
    }
```

### Read from a file

```js
    const through = require('through2');

    process.stdin
      .pipe(through(toUpper))
      .pipe(process.stdout);
    
    function toUpper(buf, enc, next){
        // buf is a binary description of the data
        // Output should be a buffer or string
        next(null, buf.toString().toUpperCase())
    }
```

### With Node Core

```js
    const { Transform } = require('stream');
    const toUpper = new Transform({
        transform: function(buf, enc, next) {
          next(null, buf.toString().toUpperCase())
        }
        // ... and other hooks
    })

    process.stdin
      .pipe(toUpper)
      .pipe(process.stdout);
  
```

`flush` is what happens when a stream finishes.

### Bit on package through2

With through there are 2 parameters: `write` and `end`.
Both are optional.

`through(write, end)`

* `function write (bug, enc, next) {}`
* `function end () {}`

Call `next()` when you're ready for the next chunk.
If you don't call `next()`, your stream will hang!

Call `this.push(VALUE)` inside the callback to put VALUE into the stream's output.

Use a `VALUE` of `NULL` to end the stream. This can happen when you need to buffer a certain amount of bytes before you 
can do something. If you need 100 Byte, you keep doing `this.push(VALUE)` on each chunk received and just call `next()`
until your buffer size is big enough and take proper actions. 

### Concat stream

`npm install concat-stream`

Concat-steam buffers up all the data in the stream:

```js
    const concat = require('concat-stream');
    process.stdin.pipe(concat(function( body) {
        console.log(body.length);
    }))
```

You can only write to a concat-stream, You can't read from a concat-stream. Keep in mind that all data will be 
in memory.


**GOOD TO KNOW** : When you are listening to a STDIN, it will keep taking input till it receives a `CTRL + D`.


### Example of basic HTTP Server with concat stream

```js
    const concat = require('concat-stream');
    const through = require('through2');
    const http = require('http');
    const qs = require('querystring');
    const SIZE_LIMIT= 20;
    
    var server = http.createServer(function(req, res) {
        req
            .pipe(counter())
            .pipe(concat({encoding: 'string'}, onBody));
    
    
        function counter() {
           var size = 0;
           return through(function(buf, enc, next) {
             size += buf.length;
             if(size > SIZE_LIMIT) {
                 next(null, null);
             }else{
                 next(null, buf);
             }
           })
        }
        
        function onBody (body){
            var params = qs.parse(body);
            console.log(params);
            res.end('ok
');
        }
    });
    server.listen(5000);
```

## Stream Types

* **Readable streams** - Produces data : You can pipe  FROM it
  * `readable.pipe(A)`
  * Key Methods (on each stream you can write to: writeable, transform and duplex)
    * `.write(buf)`
    * `.end()`
    * `.end(buf)`
    * `.on('finish', function () {})`
    * `(...).pipe(stream)`
  * Example
  ```js
    const fs = require('fs');
    const w = fs.createWriteStream('cool.txt');
    w.once('finished', function() {
      console.log('FINISHED');
    });
    w.write('Hi
');
    w.write('Wow
');
    w.end();
  ```

* **Writeable streams** - Consumes data: you can pipe TO it
  * `A.pipe(writeable)`
  * Key Methods
    * `stream.pipe(..)`
    * `stream.once('end, function () {})`
    * `stream.read()`
    * `stream.on('readable, function () {})`
  * Example
  ```js
    const fs = require('fs');
    const r = fs.createReadStream(process.argv[2]);
    r.pipe(process.stdout);
  ```
  * Modes, streams can be in paused or flowing mode. By default all readable are in paused mode.
    * Default with automatic back pressure
    * Data is consumes as soon chunks are available (no back pressure)
    
* **Transform streams** - Consumes data, producing transformed data
  * `A.pipe(transform).pipe(B)`
  * Readable + writeable stream where `input => transform => output`.
  * Key Methods : All the readable AND writeable methods.
  
* **Duplex streams** - Consumes data separately from producing data. (e.g a bidirectional network stream)
  * `A.pipe(duplex).pipe(A)` -> `A` and `duplex` are both gonna be a duplex
  * Readable + writeable stream where input is decoupled from output. Like a telephone!
  * Key Methods : All the readable AND writeable methods.
  * bidirectional connections basically.
  * A duplex stream can pipe in itself. Because read/write is decoupled. Imagine you have one pipe with just two (I and O) lines in it.
    And you just connect them.
  * Example: Echo Server
  ```js
    const net = require('net');
    net.createServer(function(stream) {
       stream.pipe(stream); // This does not create an infinite loop, just a echo server
    }).listen(5000);
  ```
  ```sh
    ▶ nc localhost 5000
    hi
    hi
    there
    there
    ```
  * Ammend Example: Proxy
  ```js
    const net = require('net');
    net.createServer(function(stream) {
        stream
          .pipe(net.connect(5000, 'localhost'))
          .pipe(stream)
    }).listen(5001);
  ```
  ```sh
    ▶ nc localhost 5000
    hi
    hi
    there
    there
    ```
    
### Simple VPN with password

**echo.js**

* Just output what comes in.

```js
    const net = require('net')
    net.createServer(function (stream) {
      stream.pipe(stream)
    }).listen(5000)
```

**vpn.js**

* Connects to the echo server. 
* Takes incoming connections
* Decrypts incoming connection
* Sends it plain text to the echo server
* Get's the plain text response from the echo server
* Encrypts the plain test response
* Returns the encrypted response

```js
    const net = require('net')
    const crypto = require('crypto')
    const pump = require('pump')
    const pw = 'abc123'
    
    net.createServer(function (stream) {
      pump(
        stream,
        crypto.createDecipher('aes192',pw),
        net.connect(5000,'localhost'),
        crypto.createCipher('aes192',pw),
        stream,
        function (err) {
          console.error(err)
        }
      )
    }).listen(5005)
```

**vpn-client.js**

* Connect to stdin
* (Might continue only once a buffer is full)
* Encrypt the plain text from the std in
* Send encrypted request it to the vpn server
* Decrypts the response that came back from the vpn server
* Writes the decrypted response as the plain text to the stdout

```js
    const net = require('net')
    const crypto = require('crypto')
    const pw = 'abc123'
    
    var stream = net.connect(5005,'localhost')
    process.stdin
      .pipe(crypto.createCipher('aes192',pw))
      .pipe(stream)
      .pipe(crypto.createDecipher('aes192',pw))
      .pipe(process.stdout)
```

### Object Streams

Normally you can only read and write buffers and strings with streams. However, if you initialize a stream in `objectMode`,
you can use any kind of object (except for `null`):

```js
    // This can be also done with native modules
    const through = require('through2')
    const tr = through.obj(function(reow, enc, next) {
      next(null, (row.n * 1000) + '
')
    })
    tr.pipe(process.stdout)
    tr.write({n : 5})
    tr.write({n : 10})
    tr.write({n : 3})
    tr.end();
```

When piping a object stream, the consuming stream should also be able to do `objectMode`.

## Core Streams

### APIs

Many of the APIs in node core provide stream interfaces:

* `fs.createReadStream()`
* `fs.createWriteStream()`
* `process.stdin`, `process.stdout`
* `ps.stdin`, `ps.stdout`, `ps.stderr`
* `next.connect()`, `tls.connect()`
* `net.createServer(function(stream) {})`
* `tls.createServer(otps, function(stream) {})`

### Child Process also uses streams

```js
    const { spawn } = require('child_process');
    const ps = spawn('grep', ['potato']);
    ps.stdout.pipe(process.stdout); // We pipe the output of the child process to our stdout
    ps.stdin.write('cheese
');
    ps.stdin.write('potato
');
    ps.stdin.end();
```

### HTTP core streams

```js
    // We receive a request
    // req: readable, res:writeable
    http.createServer((req, res) => ({}))
    
    // We make a request
    // req: writeable, res:readable
    var req = http.request((res) => ({}))
```

### Crypto Streams

* `crypto.createCipher(algo, password)` - transform stream to encrypt
* `crypto.createDecipher(algo, password)` - transform stream to decrypt
* `crypto.createCipheriv(algo, key, iv)` - transform stream to encrypt with iv
* `crypto.createDecipheriv(algo, key, iv)` - transform stream to decrypt with iv
* `crypto.createHash(algo)` - transform stream to output cryptographic hash
* `crypto.createHash(algo, key)` - transform stream to output HMAC digest
* `crypto.createSign(algo)` - Writeable stream to sign messages
* `crypto.createVerify(algo)` - Writeable stream to verify signatures

```js
    const { createHash } = require('crypto');
    
    process.stdin
        .pipe(createHash('sha512', { encoding : 'hex' }))
        .pipe(process.stdout);
```

Don't forget, when you run this, to use `CTRL + D` to get the hash. It basically says, pull my shit.

### Zlib core streams

* `zlib.createGzip(opts)` - transform stream to compress with gzip
* `zlib.createGunzip(opts)` - transform stream to uncompress with gzip
* `zlib.createDeflate(opts)` - transform stream to compress with deflate
* `zlib.createInflate(opts)` - transform stream to uncompress with deflate
* `zlib.createDeflateRaw(opts)` - transform stream to compress with raw deflate
* `zlib.createInflateRaw(opts)` - transform stream to uncompress with raw deflate
* `zlib.createUnzip(opts)` - transform stream to uncompress gzip and deflate

### Split2 use case

Split input on newlines

```js
    const split = require('split2');
    const through = require('through2');
    
    let count = 0;
    process.stdin
        .pipe(split()) // This splits on new lines
        .pipe(through(write, end)); // Now we increase the count per chunk (each being a new line) and log total count
    
    function write(next) {
      count++;
      next();
    }
    
    function end() {
      console.log(count);
    }

```

## Web Socket

### Websocket streams

Streaming websockets in node and the browser.

```js
    const http = require('http');
    const ecstatic = require('ecstatic');
    const through = require('through2');
    
    var server = http.createServer(ecstatic(__dirname + '/public')
    server.listen(3000);
    
    const wsock = require('websocket-stream');
    wsock.createServer({server}, function (stream) {
        // stream is a duplex stream
        stream.pipe(loud()).pipe(stream);
    })
    
    function loud () {
        return through(function(bug, enc, next){
            next(null, buf.toString().toUpperCase());
        });
    }

```

### Websocket Node Client

```js
    const wsock = require('websocket-stream');
    const stream = wsock('ws://localhost:500');
    process.stdin.pipe(stream).pipe(process.stdout);
```

## Stream Modules

### Collect Stream

Collect a stream's output into a single buffer. Useful for unit tests.
For object streams, collect output into an array of objects.

```js
    const collect = require('collect-stream');
    const split = require('split2');
    
    const sp = process.stdin.pipe(split(JSON.parse))
    collect(sp, function(err, rows){
        if(err) console.error(err);
        else console.log(rows)
    })
```

### from2

Create a readable stream with a pull function.
Reminds me a bit of a generator. (Enumeration)

```js
    const from = require('from2');
    const messages = ['hello', 'world
', null];
    
    from(function(size, next) {
      next(null, messages.shift())
    }).pipe(process.stdout);
```

### to2

Create a writable stream with a write and flush function.

```js
    const to = require('to2');
    const split = require('split2');
    
    process.stdin
        .pipe(split())
        .pipe(to(function(buf, next) {
            console.log(buf.length)
            next();
        }))
```

### Duplexify

A logger example

```js
    const duplexify = require('duplexify');
    const mkdirp = require('mkdirp');
    const fs = require('fs');
    
    module.exports = function (name) {
        const d = duplexify();
        mkdirp('logs', function(err) {
          const w = fs.createWriteStream('logs/' + name + '.log');
          d.setWriteable(w);
        })
        return d;
    }
   
```

Usage example

```js
    cont log = require('./logger.js');

    const stream = log('myname');
    stream.write(Date.now() + '
');
    stream.end();
```

### Errors

Streams are also even emitters. So errors can be caught with error listeners.

### Pump

Pump can pipe streams on each other, but gently handles errors.

```js
    const pump = require('pump');

    pump(stream1, stream2, stream3, function onError() {});
```

### Pumpify

Unlike pump, you get back a stream you can write to and from.

### End-of-stream

Reliably detect when a stream is finished. This package is aware of all the obscure ways streams can end.

```js
    const onend = require('end-of-stream');
    const net = require('net');
    
    const server = net.createServer(function(stream) {
      const iv = setInterval(() => {
          stream.write(Date.now() + '
');
      }, 1000);
      onend(stream, function onEndedOrErrorsOut(){
          clearInterval(iv);
      })
    })
    server.listen(5000);
```

## Remote Procedure Call and Multiplex

### RPC-Stream

Call methods defined by a remote endpoint.

### Multiplex

Pack multiple streams into a single stream.
