Virtual hosts - web server configs that allows multiple sites/apps on one server
Subdomains - Extensions of a domain name (ex. blog.domain.com), and they typically have their own DNS record

If virtual host doesn't have a DNS record, hosts file can be modified to map to an IP address

Webhosts have subdomains not in DNS records, can be found by vhost fuzzing

###### Types of Virutal Hosting
1. Name-based: Relies on HTTP Host Header to distinguish between websites
2. IP-based: Server decides which website to host depending on which IP the request was sent to
3. Port-based: Server serves the site based on the port used for the request

##### Tools

|Tool|Description|Features|
|---|---|---|
|[gobuster](https://github.com/OJ/gobuster)|A multi-purpose tool often used for directory/file brute-forcing, but also effective for virtual host discovery.|Fast, supports multiple HTTP methods, can use custom wordlists.|
|[Feroxbuster](https://github.com/epi052/feroxbuster)|Similar to Gobuster, but with a Rust-based implementation, known for its speed and flexibility.|Supports recursion, wildcard discovery, and various filters.|
|[ffuf](https://github.com/ffuf/ffuf)|Another fast web fuzzer that can be used for virtual host discovery by fuzzing the `Host` header.|Customizable wordlist input and filtering options.|