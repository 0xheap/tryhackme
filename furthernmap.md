**Task 2 - Introduction:**

- There are a total of 65535 ports, which is the size of a 16-byte integer.

- Here is the most common 20 ports and its services:

```
21: ftp
22: ssh
23: telnet
25: smtp
53: domain name system
80: http
110: pop3
111: rpcbind
135: msrpc
139: netbios-ssn
143: imap
443: https
445: microsoft-ds
993: imaps
995: pop3s
1723: pptp
3306: mysql
3389: ms-wbt-server
5900: vnc
8080: http-proxy
```

**Task 5 - Scan Types (TCP Connect Scans):**

- "-sT": TCP Connect scan switch

- TCP Connect requires tree-way handshake which is:

```
Client              Server
______              ______

SYN ---------------> *
*   <--------------- SYN-ACK
ACK ---------------> *
```

- If, however, the request is sent to an open port, the target will respond with a TCP packet with the SYN/ACK flags set. Otherwise The server would send a RST flag if the packet wasn't dropped by the firewall.


**Task 6 - Scan Types (Syn Scans):**

- SYN Scans can be made with the flag `-sS`

- SYN Scans are sometimes called as "Half-open" or "Stealth" Scans.

- Advantages of SYN Scans:

```
- It's not logged by applications that is listening on the open ports.
- It can bypass old Intrusion Detection systems.
- It's Faster compared to TCP Scans.
```

- Disadvantages of SYN Scans:

```
- In order to create raw packets, It requires sudo permissions.
- It will cause problems on the target machine as we need to keep it in a production environment.
```

**Task 7 - Scan Types (UDP Scans):**

- Unlike TCP, UDP doesn't check if the packet was gone.

- UDP is stateless

- If the server doesn't respond to a UDP packet for a certain time, nmap will flag it as `open or filtered`

- NMAP will send empty raw UDP packets unless the port is mostly known, and then it will send that service's payload.

- When you send a packet to a closed UDP Port, response "port unreachable" will be sent with ICMP protocol.



**Task 8 - Scan Types (NULL, FIN and XMAS):**

- `-sN` sends a NULL Packet

- `-sF` sends a packet with flag FIN

- `-sX` sends a packet with flags (FIN,URG,PSH) and it's called XMAS scan. It's called XMAS because Sniffed Packets look like Christmas Tree.

- if the port is protected by a firewall scans will only ever identify ports as being open|filtered, closed, or filtered

- If the respond packet was *icmp port unreachable*, It would be identified as filtered.

- Purpose of these scans is to bypass some firewalls because they drop TCP packets with SYN Flag set.

**Task 9 - Scan Types (ICMP Scanning):**

- `-sn` is a switch for forcing nmap not to scan ports but ICMP echo packets or ARP packets.

- This switch will cause sending TCP-SYN packet to 443 port and TCP-ACK to 80 port.

- to Scan IPs between 192.168.0.0 and 192.168.0.255:

```
nmap -sn 192.168.0.1-254
or
nmap -sn 192.168.0.0/24
```

- Netmasks and Wildcards for CIDR Notation:

```
Slash 	Netmask 	     Wildcard mask
/32 	255.255.255.255 	0.0.0.0
/31 	255.255.255.254 	0.0.0.1
/30 	255.255.255.252 	0.0.0.3
/29 	255.255.255.248 	0.0.0.7
/28 	255.255.255.240 	0.0.0.15
/27 	255.255.255.224 	0.0.0.31
/26 	255.255.255.192 	0.0.0.63
/25 	255.255.255.128 	0.0.0.127
/24 	255.255.255.0           0.0.0.255
/23 	255.255.254.0           0.0.1.255
/22 	255.255.252.0           0.0.3.255
/21 	255.255.248.0           0.0.7.255
/20 	255.255.240.0           0.0.15.255
/19 	255.255.224.0           0.0.31.255
/18 	255.255.192.0           0.0.63.255
/17 	255.255.128.0           0.0.127.255
/16 	255.255.0.0 	        0.0.255.255
/15 	255.254.0.0 	        0.1.255.255
/14 	255.252.0.0 	        0.3.255.255
/13 	255.248.0.0 	        0.7.255.255
/12 	255.240.0.0 	        0.15.255.255
/11 	255.224.0.0 	        0.31.255.255
/10 	255.192.0.0 	        0.63.255.255
/9 	255.128.0.0 	        0.127.255.255
/8 	255.0.0.0 	        0.255.255.255
/7 	254.0.0.0 	        1.255.255.255
/6 	252.0.0.0 	        3.255.255.255
/5 	248.0.0.0 	        7.255.255.255
/4 	240.0.0.0 	        15.255.255.255
/3 	224.0.0.0 	        31.255.255.255
/2 	192.0.0.0 	        63.255.255.255
/1 	128.0.0.0 	        127.255.255.255
/0 	0.0.0.0 	        255.255.255.255 
```



**Task 10 - NSE Scripts (Overview):**

- There are nmap scripts that are used to improve scans or exploitation. These are called NSE (Nmap Scripting Engine) Scripts.

- NSE scripts use Lua as programming language.

- Useful Categories of scripts:

```
safe:- Won't affect the target
intrusive:- Not safe: likely to affect the target
vuln:- Scan for vulnerabilities
exploit:- Attempt to exploit a vulnerability
auth:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
brute:- Attempt to bruteforce credentials for running services
discovery:- Attempt to query running services for further information about the network (e.g. query an SNMP server).
```


**Task 11 - NSE Scripts (Working with The NSE):**

- To run a specific script, we use `--script=<script-name>`

- `nmap --script-help <script-name>` to see information about certain script

**Task 11.1**: What optional argument can the ftp-anon.nse script take?

- Let's use this command `nmap --script-help ftp-anon` to get information.

```
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-10 18:24 EST

ftp-anon
Categories: default auth safe
https://nmap.org/nsedoc/scripts/ftp-anon.html
  Checks if an FTP server allows anonymous logins.

  If anonymous is allowed, gets a directory listing of the root directory
  and highlights writeable files.
```

- For detailed information, I'll head into the link `https://nmap.org/nsedoc/scripts/ftp-anon.html`

- And I see:

```
Script Arguments

ftp-anon.maxlist

    The maximum number of files to return in the directory listing. By default it is 20, or unlimited if verbosity is enabled. Use a negative number to disable the limit, or 0 to disable the listing entirely.
```


**Task 12 - NSE Scripts (Searching for Scripts):**

- NMAP stores script names and categories in `/usr/share/nmap/scripts/script.db`

- If this directory is missing: ``sudo apt update && sudo apt install nmap`` to fix

- To download scripts manually: `sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`

- To update script database: `nmap --script-updatedb`

**Task 12.1**: Search for "smb" scripts in the /usr/share/nmap/scripts/ directory using either of the demonstrated methods.
What is the filename of the script which determines the underlying OS of the SMB server?

```
# grep "smb" /usr/share/nmap/scripts/script.db                                                       
Entry { filename = "smb-brute.nse", categories = { "brute", "intrusive", } }
Entry { filename = "smb-double-pulsar-backdoor.nse", categories = { "malware", "safe", "vuln", } }
Entry { filename = "smb-enum-domains.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-enum-groups.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-enum-processes.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-enum-services.nse", categories = { "discovery", "intrusive", "safe", } }
Entry { filename = "smb-enum-sessions.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-enum-shares.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-enum-users.nse", categories = { "auth", "intrusive", } }
Entry { filename = "smb-flood.nse", categories = { "dos", "intrusive", } }
Entry { filename = "smb-ls.nse", categories = { "discovery", "safe", } }
Entry { filename = "smb-mbenum.nse", categories = { "discovery", "safe", } }
Entry { filename = "smb-os-discovery.nse", categories = { "default", "discovery", "safe", } }
Entry { filename = "smb-print-text.nse", categories = { "intrusive", } }
Entry { filename = "smb-protocols.nse", categories = { "discovery", "safe", } }
Entry { filename = "smb-psexec.nse", categories = { "intrusive", } }
Entry { filename = "smb-security-mode.nse", categories = { "default", "discovery", "safe", } }
Entry { filename = "smb-server-stats.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-system-info.nse", categories = { "discovery", "intrusive", } }
Entry { filename = "smb-vuln-conficker.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-cve-2017-7494.nse", categories = { "intrusive", "vuln", } }
Entry { filename = "smb-vuln-cve2009-3103.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms06-025.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms07-029.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms08-067.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms10-054.nse", categories = { "dos", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms10-061.nse", categories = { "intrusive", "vuln", } }
Entry { filename = "smb-vuln-ms17-010.nse", categories = { "safe", "vuln", } }
Entry { filename = "smb-vuln-regsvc-dos.nse", categories = { "dos", "exploit", "intrusive", "vuln", } }
Entry { filename = "smb-vuln-webexec.nse", categories = { "intrusive", "vuln", } }
Entry { filename = "smb-webexec-exploit.nse", categories = { "exploit", "intrusive", } }
Entry { filename = "smb2-capabilities.nse", categories = { "discovery", "safe", } }
Entry { filename = "smb2-security-mode.nse", categories = { "default", "discovery", "safe", } }
Entry { filename = "smb2-time.nse", categories = { "default", "discovery", "safe", } }
Entry { filename = "smb2-vuln-uptime.nse", categories = { "safe", "vuln", } }
``` 

**Task 12.2**: Read through this script. What does it depend on?

```
cat /usr/share/nmap/scripts/smb-os-discovery.nse | grep "dependencies"
dependencies = {"smb-brute"}
```

**Task 13 - Firewall Evasion:**

- When the target host disables ICMP pings, nmap does not bother scanning ports. To prevent this, we use `-Pn` flag.

- Useful notes of Switches:

```
-f:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
An alternative to -f, but providing more control over the size of the packets: --mtu <number>, accepts a maximum transmission unit size to use for the packets sent. This must be a multiple of 8.
--scan-delay <time>ms:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
--badsum:- this is used to generate in invalid checksum for packets.
Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet.
As such, this switch can be used to determine the presence of a firewall/IDS.
```

**Task 13.2**: [Research] Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?

- The argument --data-length <# of bytes> tells Nmap to generate random bytes and append them as data in the requests.

**Task 14 - Practical:**

**Task 14.1**: Does the target (10.10.208.179)respond to ICMP (ping) requests (Y/N)?

- Let's make a normal nmap scan:

```
# nmap -sV 10.10.208.179
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-11 07:53 EST
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 3.29 seconds
```

**Task 14.2**: Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?

```
# nmap -sX -Pn -p 1-999 10.10.208.179 -vv
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-11 08:08 EST
Initiating Parallel DNS resolution of 1 host. at 08:08
Completed Parallel DNS resolution of 1 host. at 08:08, 1.17s elapsed
Initiating XMAS Scan at 08:08
Scanning 10.10.208.179 [999 ports]
XMAS Scan Timing: About 15.52% done; ETC: 08:11 (0:02:49 remaining)
XMAS Scan Timing: About 30.53% done; ETC: 08:11 (0:02:19 remaining)
XMAS Scan Timing: About 45.55% done; ETC: 08:11 (0:01:49 remaining)
XMAS Scan Timing: About 60.56% done; ETC: 08:11 (0:01:19 remaining)
XMAS Scan Timing: About 75.08% done; ETC: 08:11 (0:00:50 remaining)
Completed XMAS Scan at 08:11, 201.40s elapsed (999 total ports)
Nmap scan report for 10.10.208.179
Host is up, received user-set.
Scanned at 2023-01-11 08:08:18 EST for 202s
All 999 scanned ports on 10.10.208.179 are in ignored states.
Not shown: 999 open|filtered tcp ports (no-response)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 202.65 seconds
           Raw packets sent: 1998 (79.920KB) | Rcvd: 0 (0B)
```

**Task 14.4**: Perform a TCP SYN scan on the first 5000 ports of the target -- how many ports are shown to be open?


```
nmap -sS -Pn 10.10.62.146 -p 1-5000
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-11 09:06 EST
Nmap scan report for 10.10.62.146
Host is up (0.13s latency).
Not shown: 4995 filtered tcp ports (no-response)
PORT     STATE SERVICE
21/tcp   open  ftp
53/tcp   open  domain
80/tcp   open  http
135/tcp  open  msrpc
3389/tcp open  ms-wbt-server

Nmap done: 1 IP address (1 host up) scanned in 37.16 seconds
```

- *Open Wireshark (see Cryillic's Wireshark Room for instructions) and perform a TCP Connect scan against port 80 on the target, monitoring the results. Make sure you understand what's going on.*

- So I examined the packets passing through the tun0 interface and discovered that my machine receives a **RST** packet for the open ports but no response for the other ports. 

**Task 14.5**: Deploy the ftp-anon script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N)

```
# nmap --script=ftp-anon 10.10.62.146 -Pn -p 21
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-11 10:07 EST
Nmap scan report for 10.10.62.146
Host is up (0.080s latency).

PORT   STATE SERVICE
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT

Nmap done: 1 IP address (1 host up) scanned in 32.03 seconds
```
