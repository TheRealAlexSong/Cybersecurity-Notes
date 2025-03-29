
#### JavaScript Deobfuscation
##### Beautify
Can use browser dev tools, [Prettier](https://prettier.io/playground/) or [Beautifier](https://beautifier.io/)
##### Javascript Deobfuscation Tools
[UnPacker](https://matthewfl.com/unPacker.html)

#### Base 64 Encode/Decode
Encode:
```shell
$ echo https://www.hackthebox.eu/ | base64  

aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K
```
Decode:
```shell
$ echo aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K | base64 -d

https://www.hackthebox.eu/
```

#### Hex Encode/Decode
Encode:
```
$ echo https://www.hackthebox.eu/ | xxd -p  

68747470733a2f2f7777772e6861636b746865626f782e65752f0a
```
Decode:
```
$ echo 68747470733a2f2f7777772e6861636b746865626f782e65752f0a | xxd -p -r  

https://www.hackthebox.eu/
```

#### Caesar/Rot13
Caesar shifts all characters by a fixed number - Rot13 shifts 13 characters forward
Tip: in Rot13, in rot13, http://www becomes uggc://jjj

Rot13 encode:
```shell
$ echo https://www.hackthebox.eu/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'

uggcf://jjj.unpxgurobk.rh/
```
Rot13 decode:
```shell
$ echo uggcf://jjj.unpxgurobk.rh/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'

https://www.hackthebox.eu/
```

#### Tools
 [Cipher Identifier](https://www.boxentriq.com/code-breaking/cipher-identifier)

