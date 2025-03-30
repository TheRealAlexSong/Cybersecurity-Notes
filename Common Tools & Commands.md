
# SSH
Basic usage: $ ==ssh [user]@[host]==

# Netcat
Basic usage: $ ==nc -\[flags] \[host] \[port]==
Flags:
	Verbose: v
	Do not resolve IP: n
# Nmap
Basic usage: $ ==nmap \[flags] \[host] ==
Flags:
	Get more info -sC
	Version scan -sV
	Scan all ports -p-
	Specify port -p \[ports, comma separated]
	Return only open ports --open
	Output greppable format -oG
	Verbose output -v
	Output all scan formats -oA \[filename]
	Use script --script=\[script name]

#### Nmap Scripts
http-enum used to enumerate common web app directories

# Tmux
Open tmux commands: \[CTRL + B], then:
	New window: C
	Switch to window #: \[#]
	Split window vertically: \[SHIFT + %]
	Split window horizontally: \[SHIFT + "]
	Switch between panes: \[arrow keys]

# Vim
Create a new file: $ ==vim \[file path and file]==
Insert mode: I
Normal code: \[Esc]
	cut character: x
	cut word: dw
	cut full line: dd
	copy word: yw
	copy full line: yy
	paste: p
Command mode: \[:]
	Write/save: :w
	Quit :q
	Quit no save :q!
	Write/quit :wq

# Whatweb
Basic usage: $ ==whatweb \[host]==

# Curl
Basic command: $ curl \[address]
Flags:
	-O output content into file (use remote filename)
	-o output content into file (specify filename)
	-s silent mode
	-h show options
	-k skip SSL certificate check
	-v verbose mode (to see http request and response headers)
	-vvv extra verbose
	-I sends a HEAD request and only displays response headers
	-i sends any request specified and displays both headers and response body
	-A change user agent
	-H set header value
	-X change method
	-d add data
	-L follow redirection
	-b set cookie

Examples:
```shell
$ curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'
```

```shell
$ curl http://83.136.251.19:59586/keys.php -X POST -d "key=API_p3n_73571n6_15_fun"
```
# dig
| Command                                     | Description                                                                                                                                                                                          |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `dig domain.com`                            | Performs a default A record lookup for the domain.                                                                                                                                                   |
| `dig domain.com A`                          | Retrieves the IPv4 address (A record) associated with the domain.                                                                                                                                    |
| `dig domain.com AAAA`                       | Retrieves the IPv6 address (AAAA record) associated with the domain.                                                                                                                                 |
| `dig domain.com MX`                         | Finds the mail servers (MX records) responsible for the domain.                                                                                                                                      |
| `dig domain.com NS`                         | Identifies the authoritative name servers for the domain.                                                                                                                                            |
| `dig domain.com TXT`                        | Retrieves any TXT records associated with the domain.                                                                                                                                                |
| `dig domain.com CNAME`                      | Retrieves the canonical name (CNAME) record for the domain.                                                                                                                                          |
| `dig domain.com SOA`                        | Retrieves the start of authority (SOA) record for the domain.                                                                                                                                        |
| `dig @1.1.1.1 domain.com`                   | Specifies a specific name server to query; in this case 1.1.1.1                                                                                                                                      |
| `dig +trace domain.com`                     | Shows the full path of DNS resolution.                                                                                                                                                               |
| `dig -x 192.168.1.1`                        | Performs a reverse lookup on the IP address 192.168.1.1 to find the associated host name. You may need to specify a name server.                                                                     |
| `dig +short domain.com`                     | Provides a short, concise answer to the query.                                                                                                                                                       |
| `dig +noall +answer domain.com`             | Displays only the answer section of the query output.                                                                                                                                                |
| `dig domain.com ANY`                        | Retrieves all available DNS records for the domain (Note: Many DNS servers ignore `ANY` queries to reduce load and prevent abuse, as per [RFC 8482](https://datatracker.ietf.org/doc/html/rfc8482)). |
| dig axfr @nsztm1.digi.ninja zonetransfer.me | Performs a zone transfer for the domain zonetransfer.me on its DNS server nsztm1.digi.ninja                                                                                                          |
|                                             |                                                                                                                                                                                                      |
# gobuster
Basic usage: 
```$ gobuster vhost -u http://<target_IP_address> -w <wordlist_file> --append-domain```
Flags:
	-t increases # of threads
	-k ignores SSL/TLS certificate errors
	-o save output 

# crt.sh API call
Example: 
```shell
$ curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[]
 | select(.name_value | contains("dev")) | .name_value' | sort -u

	curl -s "https://crt.sh/?q=facebook.com&output=json"
	This command fetches the JSON output from crt.sh for certificates matching the domain `facebook.com`

	jq -r '.[] | select(.name_value | contains("dev")) | .name_value'
	This part filters the JSON results, selecting only entries where the `name_value` field (which contains the domain or subdomain) includes the string "`dev`". The `-r` flag tells `jq` to output raw strings.

	sort -u
	This sorts the results alphabetically and removes duplicates
```

## ffuf
Can be used to bruteforce and spider website directories and pages/files, subdomains and vhosts, website/URL parameters using GET or POST, and parameter values

#### Basic usage: 

```shell
$ ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ

	note the ":FUZZ" and "FUZZ" keyword usage
```
#### Usage with flags:

```shell
$ ffuf -w /opt/useful/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://academy.htb:38784/indexFUZZ
```

```shell
$ ffuf -w /opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```

```shell
$ ffuf -w /opt/useful/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb'
```

```shell
$ ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx
```

```shell
$ ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx`
```

```shell
$ ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

Flags:
	-recursion -recursion-depth xx
		toggle recursion and specify depth
	-e .php
		specify file extension
	-v
		output full URL
	-H 'Host: FUZZ.academy.htb'
		specify host to scan for vhosts
	-fs xxx
		exclude results with size xxx bytes
	-d
		fuzz data
	-X POST
		send POST requests

# xsstrike
#### Basic usage:
```shell
$ python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test" 
```

```shell-session
<HtMl%09onPoIntERENTER+=+confirm()>
```