
Open ports
80/tcp http Apache/2.4.41 (Ubuntu)
22/tcp ssh SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.1

GetSimple CMS (on/before 2/9/21)

Exploits (working):
exploit(multi/http/getsimplecms_unauth_code_exec)

user mrb3n

[+] We can sudo without supplying a password!
Matching Defaults entries for www-data on gettingstarted:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on gettingstarted:
    (ALL : ALL) NOPASSWD: /usr/bin/php


[+] Possible sudo pwnage!
/usr/bin/php
