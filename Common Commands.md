
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
	