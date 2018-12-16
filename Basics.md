# Web-Servers
All about web servers

### 1. Requests & Responses

#### Tools

brew install nmap  

open two terminal window
ncat -l 9999  
ncat localhost 9999

#### First web server  
```
python3 -m http.server 8000
```

#### URI  

http/https/file is the scheme;  
en.wikipedia.org is the hostname;  
and /wiki/Fish is the path.
https://en.wikipedia.org/wiki/Oxygen#Discovery
'#' is a Fragment
https://www.google.com/search?q=fish
?q=fish is a query

http://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml

#### Hostname & Ports
```
host www.google.com
```

Packets - IP address of computer that sent it and computer that receives it
IP - computers
Port - Programs


#### Default Port
HTTP:80  
HTTPS is port 443

#### HTTP GET Request

ncat 127.0.0.1 8000  
GET / HTTP/1.1  
Host: localhost

Request headers:
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.5.2
Date: Sat, 19 May 2018 12:52:14 GMT
Content-type: text/html; charset=utf-8
Content-Length: 418

**cookies** are a Web feature that lets servers store data on the browser, for instance to keep a user logged in. To set a cookie, the server sends the Set-Cookie header. The browser will then send the cookie data back in a Cookie header on subsequent requests.

**Content-type header** indicates the kind of data that the server is sending.

**Content-Length header** which tells the client how long (in bytes) the response body will be.
If the server sends this, then the client can reuse the connection to send another request after it's read the first response. Browsers use this so they can fetch multiple pieces of data (such as images on a web page) without having to reconnect to the server.



Body:

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">  
<html>
</html>

#### HTTP Response

<ol>
<li>status line
<li>some headers
<li>response body
</ol>

######  Status Line

https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html

<b>1xx — Informational.</b> The request is in progress or there's another step to take.  
<b>2xx — Success!</b>  
<b>3xx — Redirection</b>. The server is telling the client a different URI it should redirect to. The headers will usually contain a Location header with the updated URI.   Different codes tell the client whether a redirect is permanent or temporary.  
<b>4xx — Client error.</b> The server didn't understand the client's request, or can't or won't fill it. Different codes tell the client whether it was a bad URI, a permissions problem, or another sort of error.  
<b>5xx — Server error.</b> Something went wrong on the server side.  

######  Header

HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.5.2
Date: Sat, 19 May 2018 12:52:14 GMT
Content-type: text/html; charset=utf-8
Content-Length: 418

######  Run a server
 ncat localhost 9999  
 open the URI in browser  
 HTTP/1.1 307 redirect
Location: https://www.google.com
(Enter)
(Enter) Twice

-Redirects to google.com


### 2. Web from python

**Encode**   
If you want to send a string over the HTTP connection, you have to encode the string into a bytes object

```
>>> len('ねこ')
2
>>> len('ねこ'.encode())
6
```

 if you try to start EchoServer.py while HelloServer.py is still running … or vice versa?
 New server exits with OSError exception   

 ###### Queries

 ```
 >>> from urllib.parse import urlparse, parse_qs
>>> address = 'https://www.google.com/search?q=gray+squirrel&tbm=isch'
>>> parts = urlparse(address)
>>> print(parts)
ParseResult(scheme='https', netloc='www.google.com', path='/search', params='', query='q=gray+squirrel&tbm=isch', fragment='')
>>> print(parts.query)
q=gray+squirrel&tbm=isch
>>> query = parse_qs(parts.query)
>>> query
{'q': ['gray squirrel'], 'tbm': ['isch']}
```

###### URL quoting - URL-encoding or URL-escaping

It means translating a string into a form that doesn't have any special characters in it, but in a way that can be reversed (unquoted) later.

###### HTML and forms

The form action is the URI to which the form fields will be submitted.

###### GET & POST

```
POST / HTTP/1.1
Host: localhost:9999
Connection: keep-alive
Content-Length: 27
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: null
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.80 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9

magic=mystery&secret=spooky%
```
```
GET /?magic=mystery&secret=spooky HTTP/1.1
Host: localhost:9999
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.80 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
```
***
**POST**
When a browser submits a form as a POST request, it doesn't encode the form data in the URI path, the way it does with a GET request. Instead, it sends the form data in the request body, underneath the headers. The request also includes Content-Type and Content-Length headers, which we've previously only seen on HTTP responses.

**Why no GET**
Why don't we want to use GET for submitting the form? Imagine if a user did this. They write a message and press the submit button … and the message text shows up in their URL bar. If they press reload, it sends the message again. If they bookmark that URL and go back to it, it sends the message again. This doesn't seem like such a great experience. So we'll use POST for message submission, and GET to display the main page.

**Note**   
 If there's a request body at all, the browser will send the length of the request body in the Content-Length header.
***
