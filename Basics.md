# Web-Servers
All about web servers

### 1. Requests & Responses

#### Tools

brew install nmap  

open two terminal window
ncat -l 9999  
ncat localhost 9999

#### First web server  

python3 -m http.server 8000

#### URI  

https is the scheme;  
en.wikipedia.org is the hostname;  
and /wiki/Fish is the path.  

http://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml

#### DEFAULT PORT  
HTTP:80  
HTTPS is port 443

#### HTTP GET REQUEST

ncat 127.0.0.1 8000  
GET / HTTP/1.1  
Host: localhost

Request headers:
HTTP/1.0 200 OK
Server: SimpleHTTP/0.6 Python/3.5.2
Date: Sat, 19 May 2018 12:52:14 GMT
Content-type: text/html; charset=utf-8
Content-Length: 418

Body:

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">  
<html>
</html>

#### HTTP RESPONSE

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
