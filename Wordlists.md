Bash command to create a file with sequential numbers 1 to 1000
```shell
$ for i in $(seq 1 1000); do echo $i >> ids.txt; done
```

In pwnbox, wordlists available in /opt/useful/seclists/