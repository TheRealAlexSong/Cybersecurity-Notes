
## DNS
- Can uncover subdomains, mail servers, etc
- Can give clues on network infrastructure (name servers, load balancers)
- Monitor for record changes to see what they're up to
#### Tools
- dig - dns lookup tool
- nslookup - simpler dns lookup tool
- host - streamlined dns lookup tool
- dnsenum - enumeration tool with dictionary attack, brute force, zone transfers
- fierce - recon and subdomain enumeration
- dnsrecon - combines multiple dns recon techniques
- theHarvester - OSINT tool that gathers multi-source info (including DNS records)

## Certificate Transparency (CT) logs
- CT logs offer historical view of certs issued for domains and subdomains

#### Tools to search CT logs
- crt.sh 
- search.censys.io

## Fingerprinting
- Banner grabbing
- Analyzing HTTP headers
- Probing for responses (crafting requests and looking for unique responses)
- Analyze page content (structure, scripts)

#### Tools
- Wappalyzer
- BuiltWith
- WhatWeb
- nmap
- Netcraft
- wafw00f - CLI tool for fingerprinting web application firewalls (WAFs)
- Nikto - open source web server scanner