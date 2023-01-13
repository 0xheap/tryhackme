# DNS in Detail

## Task 1 - What is DNS?

- DNS (Domain Name System) provides a simple way for us to communicate with devices on the internet without remembering complex numbers.

## Task 2 - Domain Hierarchy

- There are 3 types of domain:

```
*) Root Domain

1) Sub Domain
2) Top-Level Domains => gTLD (Generic TLD), ccTLD (Country Code TLD)
3) Second-Level Domains

For Example:

   Second-Level Domain
          |    
          | 	 ccTLD
          |        |
          |        |
chrome.google.com.tr
  |            | 
  |            | 
  |	  gTLD (Commerce)
  |	
Sub Domain
```

- The second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

- A subdomain name has the same creation restrictions as a Second-Level Domain.

- You can use multiple subdomains split with periods to create longer names. (For example: example.chrome.google.com), But the length must be kept to 253 characters or less.

## Task 3 - Record Types:

### A Record:

- These records resolve to IPv4 addresses, for example 8.8.8.8

### AAAA Record:

- These records resolve to IPv6 addresses, for example 1306:3900:10::681a:be5

### CNAME Record:

- CNAME records must always point to another domain name, never directly to an IP address. 

```
NAME                    TYPE   VALUE
--------------------------------------------------
bar.example.com.        CNAME  foo.example.com.
foo.example.com.        A      192.0.2.23
```

- When an A record lookup for bar.example.com is carried out, the resolver will see a CNAME record and restart the checking at foo.example.com and will then return 192.0.2.23

### MX Record:

- These records resolve to the address of the servers that handle the email for the domain you are querying.

- Example MX record response: alt1.aspmx.l.google.com

### TXT Record:

- TXT records are free text fields where any text-based data can be stored.

- The TXT record was originally intended as a place for human-readable notes. 

- However, now it is also possible to put some machine-readable data into TXT records.

- Spammers often try to fake or forge the domains from which they send their email messages.

- TXT records are a key component of several different email authentication methods that help an email server determine if a message is from a trusted source.

## Task 4 - Making a Request:

```
	       BROWSER
		  |
		  |
		  v
	    RECURSIVE DNS <-----
		  |         	|
		  |	    	|
		  v	    	|
	      ROOT DNS	    	|
		  |	    	|
		  |	   	|
		  v	    	|
          AUTHORITATIVE DNS ----

```
- When you request a domain name, your computer first checks its local cache to see if you've previously looked up the address recently; if not, a request to your Recursive DNS Server will be made.

- A Recursive DNS Server is usually provided by your ISP, but you can also choose your own. If the request can't be found locally, a request to your Root DNS Server will be made.

- The root servers redirect you to the correct Top Level Domain Server, depending on your request. It'll get the TLD of the domain and refer you to the correct TLD server.

- The TLD server holds records for where to find the authoritative server to answer the DNS request. The authoritative server is often also known as the nameserver for the domain. (ns1 and ns2)

- An authoritative DNS server is the server that is responsible for storing the DNS records for a particular domain name and where any updates to your domain name DNS records would be made.

- Depending on the record type, the DNS record is then sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client that made the request.

- Time to live (TTL) refers to the amount of time or “hops” that a packet is set to exist inside a network before being discarded by a router.

