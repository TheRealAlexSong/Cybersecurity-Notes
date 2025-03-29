Hosts file - on Windows C:\windows\system32\drivers\etc\hosts; on Linux /etc/hosts

Always check for vhosts. If found, add to hosts file. Then check for vhosts on the vhost, sometimes they are nested!

If a URL does not load, try performing curl

When performing curl on a directory, ensure the URL contains the following forward slash

Quick add to /etc/hosts:
```shell
$ sudo sh -c 'echo "SERVER_IP  academy.htb" >> /etc/hosts'
```

[[Common Commands#ffuf]]
