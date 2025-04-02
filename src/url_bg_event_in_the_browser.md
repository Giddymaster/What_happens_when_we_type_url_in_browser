# What happens when we type a url in the browser

Example: <https://www.google.com/facebook/gideon>

The url is divided into 4 parts:  

    https - The scheme/protocol which browser will use while connecting  
    www.google.com - domain (`.com`  top-level domain  + second-level `google`) 
    facebook - the path
    gideon - resource

## DNS Lookup

The browser first checks `local cache` (recently visited domains).  
OS checks hosts file (manual overrides) and local DNS cache.  
Query sent to `recursive Google DNS` resolver (Google’s 8.8.8.8).  
Google DNS then queries `root DNS servers` which responds by giving  the (.com) servers called `TLD; Top-Level-Domain servers` .  
Google DNS queries TLD for the second level domain,through the help of domain registrar hands over the `authoritative DNS servers` for Google DNS to query there.The authoritative DNS servers responds by giving the `ip address` of facebook.  
IP returned `172.217.0.46` and cached at multiple levels by Google DNS.

>More resources:  <https://www.youtube.com/watch?v=NiQTs9DbtW4&t=487s&ab_channel=NetworkChuck>

### Handshake (TCP)

The browser then establishes a `Transmission Control Protocol (TCP)` connection with the server.The handshake is like an agreement of how data will be transmitted between client and server.

### HTTP Request

After TCP connection, browser send a request, how?  
In this case, its a `GET` request.

    GET: /facebook HTTP/1.1  
    Host: www.google.com -header  
    Accept: text/html
    Cookie: session_id=abc123

Header are the instructions to the server  
HTTP specifies how to pack the data, what to do before, during, and after the request.

## What server does when a request is sent

Server parses the message, understands and Loads the request file from either the local disk, or from a database or returns an error if there was an error/mistake in the request url.

### Sending the request back

The loaded information file from server is wrapped into `HTTP Response` and is sent back on the same TCP connection.The server processes the request and sends back the response. For a successful response, the status code is 200. There are 3 parts in the response: HTML, CSS and Javascript.

How?  

    HTTP/1/1  200  OK(If successful) or 404(error)  
    Content-Type : eg text/html/JSON,etc..  
    content-Length :2000 (in bytes) 
    <html> body( The real content eg html body) </html> 

### Browser upon receiving the response

The browser parses HTML and generates DOM tree. It also parses CSS and generates CSSOM tree. It then combines DOM tree and CSSOM tree to render tree. The browser renders the content and display to the user.  

Incase of file that browser does kno how to open, eg. a pdf, it downloads it locally.

If  the response is linked to other files such as CSS files, Image tags it fetches the additional files by repeating the whole process but incase of JavaScript code, the browser starts executing it.
