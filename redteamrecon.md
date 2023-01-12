**Task 2 - Taxonomy of Reconnaissance:**

_Active Recon:_ Information gathering by interacting the target.

_Passive recon:_ Information gathering that does not require interaction and can be easily accomplished by searching social media, etc.

_External Active Recon:_ Information besides that outside of the target's network.

_Internal Active Recon:_ Information besides that inside of the target's network, localized.

**Task 3 - Built-in Tools**

_dig:_ stands for Domain Information Groper

_nslookup:_ stands for Name Server Lookup, It shows assigned IPs to the domain
_traceroute:_ It shows the paths of a packet going into the domain

_whois:_ Detailed DNS Lookup (Records, Registrant Informations, Date of Creation etc.)

_host:_ It simply shows the IP of a domain

**Task 4 - Advanced Searching**

_Double Quotes "word" =_ Show only the results that contain the word "word"

_word filetype:pdf =_ Show pdf files associated with "word"

_word site:tryhackme.com =_ Display only results associated with "word" on the tryhackme.com website

_word -site:tryhackme.com =_ Display results associated with "word" but exclude tryhackme.com website

_word intitle:Hello =_ Show results for "word" that include "Hello" in the website title

_word inurl:Hello =_ Show results for "word" that include "Hello" in the URL

**Task 5 - Specialized Search Engines**

_VidewDNS.info_ : Reverse IP Lookup, Reverse whois Lookup etc.

_search.censys.io_ : Advanced DNS Lookup

_www.shodan.io_ : Mostly used to look up IoT Devices

**Task 6 - Recon-NG**

- _recon-ng:_ Web Recon application which uses modules to gather information

> workspaces create thm

> marketplace install google_site_web

> modules load google_site_web

> run

- That gives us subdomains of thmredteam.com which is 

`clinic.thmredteam.com` and `cafe.thmredteam.com`

- So what basically google_site_web is doing? We can see it by typing:

> back

> marketplace info google_site_web

```
  +---------------------------------------------------------------------------------------------------------------------------------+
  | path          | recon/domains-hosts/google_site_web                                                                             |
  | name          | Google Hostname Enumerator                                                                                      |
  | author        | Tim Tomes (@lanmaster53)                                                                                        |
  | version       | 1.0                                                                                                             |
  | last_updated  | 2019-06-24                                                                                                      |
  | description   | Harvests hosts from Google.com by using the 'site' search operator. Updates the 'hosts' table with the results. |
  | required_keys | []                                                                                                              |
  | dependencies  | []                                                                                                              |
  | files         | []                                                                                                              |
  | status        | installed                                                                                                       |
  +---------------------------------------------------------------------------------------------------
```


**Task 6.2**:

> marketplace search virustotal

```
[*] Searching module index for 'virustotal'...

  +---------------------------------------------------------------------------------+
  |               Path               | Version |     Status    |  Updated   | D | K |
  +---------------------------------------------------------------------------------+
  | recon/hosts-hosts/virustotal     | 1.0     | not installed | 2019-06-24 |   | * |
  | recon/netblocks-hosts/virustotal | 1.0     | not installed | 2019-06-24 |   | * |
  +---------------------------------------------------------------------------------+
```

**Task 6.4**: 

> marketplace info censys_email_address

```
  +-----------------------------------------------------------------------------------------------------------------------------------+
  | path          | recon/companies-contacts/censys_email_address                                                                     |
  | name          | Censys emails by company                                                                                          |
  | author        | Censys Team                                                                                                       |
  | version       | 2.0                                                                                                               |
  | last_updated  | 2021-05-11                                                                                                        |
  | description   | Retrieves email addresses from the TLS certificates for a company. Updates the 'contacts' table with the results. |
  | required_keys | ['censysio_id', 'censysio_secret']                                                                                |
  | dependencies  | ['censys>=2.0.0']                                                                                                 |
  | files         | []                                                                                                                |
  | status        | not installed                                                                                                     |
  +-----------------------------------------------------------------------------------------------------------------------------------+
```

**Task 7 - Maltego**

- Application Maltego manages information graphically and you can transform data with `transforms`

- https://www.maltego.com/transform-hub/
