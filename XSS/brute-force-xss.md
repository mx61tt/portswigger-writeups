### Brute force XSS

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

1. Copy tags to clipboard and then use Intruder to check which one is valid. Format:

```
%3C§tag_here§%3E
```

2. If find any tag valid, copy events to clipboard and then use again Intruder to check which one trigger the alert. Format:

```
%3Cimg%20§event_here§=alert(1)%3E
```
