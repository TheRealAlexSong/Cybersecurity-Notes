
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

## Well-Known URIs
Standardized directory on a webserver (normally /.well-known/) containing critical metadata

| URI Suffix                     | Description                                                                                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `security.txt`                 | Contains contact information for security researchers to report vulnerabilitie                                                                                |
| `/.well-known/change-password` | Provides a standard URL for directing users to a password change pa                                                                                           |
| `openid-configuration`       Defines configuration details for OpenID Connect, an identity layer on top of the OAuth 2.0 protocol. \*Shows endpoints, auth methods, token issuance, etc\* ds,  |
| `assetlinks.json`              | Used for verifying ownership of digital assets (e.g., apps) associated with a do                                                                              |
| `mta-sts.txt`                  | Specifies the policy for SMTP MTA Strict Transport Security (MTA-STS) to enhance email sec                                                                    |

## Crawler Tools
- Burp Suite Spider
- OWASP ZAP
- Scrapy (python framework) - used for building custom crawlers
- Apache Nutch (scalable crawler) - java-based, highly scalable for very large crawls

## Search Operators (generic)

| Operator                | Operator Description                                         | Example                                             | Example Description                                                                     |
| ----------------------- | ------------------------------------------------------------ | --------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `site:`                 | Limits results to a specific website or domain.              | `site:example.com`                                  | Find all publicly accessible pages on example.com.                                      |
| `inurl:`                | Finds pages with a specific term in the URL.                 | `inurl:login`                                       | Search for login pages on any website.                                                  |
| `filetype:`             | Searches for files of a particular type.                     | `filetype:pdf`                                      | Find downloadable PDF documents.                                                        |
| `intitle:`              | Finds pages with a specific term in the title.               | `intitle:"confidential report"`                     | Look for documents titled "confidential report" or similar variations.                  |
| `intext:` or `inbody:`  | Searches for a term within the body text of pages.           | `intext:"password reset"`                           | Identify webpages containing the term “password reset”.                                 |
| `cache:`                | Displays the cached version of a webpage (if available).     | `cache:example.com`                                 | View the cached version of example.com to see its previous content.                     |
| `link:`                 | Finds pages that link to a specific webpage.                 | `link:example.com`                                  | Identify websites linking to example.com.                                               |
| `related:`              | Finds websites related to a specific webpage.                | `related:example.com`                               | Discover websites similar to example.com.                                               |
| `info:`                 | Provides a summary of information about a webpage.           | `info:example.com`                                  | Get basic details about example.com, such as its title and description.                 |
| `define:`               | Provides definitions of a word or phrase.                    | `define:phishing`                                   | Get a definition of "phishing" from various sources.                                    |
| `numrange:`             | Searches for numbers within a specific range.                | `site:example.com numrange:1000-2000`               | Find pages on example.com containing numbers between 1000 and 2000.                     |
| `allintext:`            | Finds pages containing all specified words in the body text. | `allintext:admin password reset`                    | Search for pages containing both "admin" and "password reset" in the body text.         |
| `allinurl:`             | Finds pages containing all specified words in the URL.       | `allinurl:admin panel`                              | Look for pages with "admin" and "panel" in the URL.                                     |
| `allintitle:`           | Finds pages containing all specified words in the title.     | `allintitle:confidential report 2023`               | Search for pages with "confidential," "report," and "2023" in the title.                |
| `AND`                   | Narrows results by requiring all terms to be present.        | `site:example.com AND (inurl:admin OR inurl:login)` | Find admin or login pages specifically on example.com.                                  |
| `OR`                    | Broadens results by including pages with any of the terms.   | `"linux" OR "ubuntu" OR "debian"`                   | Search for webpages mentioning Linux, Ubuntu, or Debian.                                |
| `NOT`                   | Excludes results containing the specified term.              | `site:bank.com NOT inurl:login`                     | Find pages on bank.com excluding login pages.                                           |
| `*` (wildcard)          | Represents any character or word.                            | `site:socialnetwork.com filetype:pdf user* manual`  | Search for user manuals (user guide, user handbook) in PDF format on socialnetwork.com. |
| `..` (range search)     | Finds results within a specified numerical range.            | `site:ecommerce.com "price" 100..500`               | Look for products priced between 100 and 500 on an e-commerce website.                  |
| `" "` (quotation marks) | Searches for exact phrases.                                  | `"information security policy"`                     | Find documents mentioning the exact phrase "information security policy".               |
| `-` (minus sign)        | Excludes terms from the search results.                      | `site:news.com -inurl:sports`                       | Search for news articles on news.com excluding sports-related content.                  |

## Google Dorking

Examples:
- Finding Login Pages:
    - `site:example.com inurl:login`
    - `site:example.com (inurl:login OR inurl:admin)`
- Identifying Exposed Files:
    - `site:example.com filetype:pdf`
    - `site:example.com (filetype:xls OR filetype:docx)`
- Uncovering Configuration Files:
    - `site:example.com inurl:config.php`
    - `site:example.com (ext:conf OR ext:cnf)` (searches for extensions commonly used for configuration files)
- Locating Database Backups:
    - `site:example.com inurl:backup`
    - `site:example.com filetype:sql`

More: https://www.exploit-db.com/google-hacking-database


## Recon Frameworks
- [FinalRecon](https://github.com/thewhiteh4t/FinalRecon): A Python-based reconnaissance tool offering a range of modules for different tasks like SSL certificate checking, Whois information gathering, header analysis, and crawling. Its modular structure enables easy customisation for specific needs.
- [Recon-ng](https://github.com/lanmaster53/recon-ng): A powerful framework written in Python that offers a modular structure with various modules for different reconnaissance tasks. It can perform DNS enumeration, subdomain discovery, port scanning, web crawling, and even exploit known vulnerabilities.
- [theHarvester](https://github.com/laramies/theHarvester): Specifically designed for gathering email addresses, subdomains, hosts, employee names, open ports, and banners from different public sources like search engines, PGP key servers, and the SHODAN database. It is a command-line tool written in Python.
- [SpiderFoot](https://github.com/smicallef/spiderfoot): An open-source intelligence automation tool that integrates with various data sources to collect information about a target, including IP addresses, domain names, email addresses, and social media profiles. It can perform DNS lookups, web crawling, port scanning, and more.
- [OSINT Framework](https://osintframework.com/): A collection of various tools and resources for open-source intelligence gathering. It covers a wide range of information sources, including social media, search engines, public records, and more.