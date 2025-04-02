# What happens when we type a url in the browser

Example: https://www.google.com/facebook

The url is divided into 3 parts:  

    https - The scheme/protocol which browser will use while connecting  
    www.google.com - domain  
    facebook - the path

## DNS Lookup

So when we type the urls in the browser(OS), from a  `Domain name server(DNS) ` happens first to convert the url from human readable format to an ip address that is browser readable.

> www.google.com  --------> 142.250.176.206

The browser then establishes a `Transmission Control Protocol (TCP) `connection with the server.

After TCP connection, browser send a request, how?  
In this case, its a `GET` request.

    GET: [http](https://www.google.com/facebook)  
    Host: www.google.com -header  
    Connection: keep-alive -header

Header are the instructions to the server  
HTTP specifies how to pack the data, what to do before, during, and after the request.

## What server does when a request is sent

Server parses the message, understands and Loads the request file from either the local disk, or from a database or returns an error if there was an error/mistake in the request url.

### Sending the request back

The loaded information file from server is wrapped into `HTTP Response` and is sent back on the same TCP connection.

How?  

    HTTP : 200 . OK(If successful) or 404(error)  
    Content-Type : eg text/html/JSON,etc..  
    content-Length :2000 (in bytes) 
    body( The real content eg html body)  

### Browser upon receiving the response

Browser parses the message/response and renders it in the browser and incase of file that browser does kno how to open, eg. a pdf, it downloads it locally.

If  the response is linked to other files such as CSS files, Image tags it fetches the additional files by repeating the whole process but incase of JavaScript code, the browser starts executing it.
ucdsvbdf
