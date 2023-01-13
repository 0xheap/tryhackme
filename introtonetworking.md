# Introductory Networking

## Task 2 - The OSI Model:

```
7.  Application layer
6.  Presentation layer
5.  Session layer
4.  Transport layer
3.  Network layer
2.  Data link layer
1.  Physical layer
```

### Layer 7 - Application Layer:

- The application layer is where the user inputs data and data is output to the user.

- Example Services: FTP, TelNet, Browser...

### Layer 6 - Presentation Layer:

- The presentation layer is where the operating system lies.

- This operating system could be Windows, OS X, a Unix based operating system or one of the many others available.

### Layer 5 - Session Layer:

- The session layer is responsible for creating and maintaining sessions between the operating system on the presentation layer and other, third party machines.

### Layer 4 - Transport Layer:

- The transport layer is responsible for the logistics of the session.

- TCP/UDP is best example.

### Layer 3 - Network Layer:

- The network layer is where routers operate.

- A router is a hardware device that forwards packets of information between computers on a network.

### Layer 2 - Data link Layer:

- The data link layer is where switches operate and provides a reliable link between two directly connected nodes.

- The data link layer is also responsible for detecting and possibly fixing any packet errors that may form on the physical layer.

### Layer 1 — Physical Layer:

- The physical layer is literally the physical hardware that makes up the network.

- Defines physical specifications, protocols, the network’s topology.

## Task 3 - Encapsulation:

- Takes information from a higher layer and adds a header to it, treating the higher layer information as data

- When the message is received by the second computer, it reverses the process so It's de-encapsulation.

```
7.  Application layer - DATA
6.  Presentation layer - DATA 
5.  Session layer - DATA
4.  Transport layer - DATA (SEGMENTS/DATAGRAMS)
3.  Network layer - DATA (PACKETS)
2.  Data link layer - DATA (FRAMES) - TRAILER
1.  Physical layer - DATA (BITS)
```

## Task 4 - TCP/IP Model:

```
APPLICATION
TRANSPORT
INTERNET
NETWORK INTERFACE
```

- Comparing TCP/IP and OSI Model:

```
7.  Application layer ------ APPLICATION
6.  Presentation layer ----- APPLICATION
5.  Session layer ---------- APPLICATION
4.  Transport layer -------- TRANSPORT
3.  Network layer ---------- INTERNET
2.  Data link layer -------- NETWORK INTERFACE
1.  Physical layer --------- NETWORK INTERFACE
```

- TCP is a connection-based protocol, before you send any data via TCP, you must first form a stable connection between the two computers.

- The process of forming this connection is called the three-way handshake.

```
Client              Server
______              ______

SYN ---------------> *
*   <--------------- SYN-ACK
ACK ---------------> *
```

- TCP/IP model is the standard upon which modern networking is based.

## Task 5 - Ping (Networking Tools):

```
Usage
  ping [options] <destination>

Options:
  <destination>      dns name or ip address
  -a                 use audible ping
  -A                 use adaptive ping
  -B                 sticky source address
  -c <count>         stop after <count> replies
  -C                 call connect() syscall on socket creation
  -D                 print timestamps
  -d                 use SO_DEBUG socket option
  -e <identifier>    define identifier for ping session, default is random for
                     SOCK_RAW and kernel defined for SOCK_DGRAM
                     Imply using SOCK_RAW (for IPv4 only for identifier 0)
  -f                 flood ping
  -h                 print help and exit
  -I <interface>     either interface name or address
  -i <interval>      seconds between sending each packet
  -L                 suppress loopback of multicast packets
  -l <preload>       send <preload> number of packages while waiting replies
  -m <mark>          tag the packets going out
  -M <pmtud opt>     define mtu discovery, can be one of <do|dont|want>
  -n                 no dns name resolution
  -O                 report outstanding replies
  -p <pattern>       contents of padding byte
  -q                 quiet output
  -Q <tclass>        use quality of service <tclass> bits
  -s <size>          use <size> as number of data bytes to be sent
  -S <size>          use <size> as SO_SNDBUF socket option value
  -t <ttl>           define time to live
  -U                 print user-to-user latency
  -v                 verbose output
  -V                 print version and exit
  -w <deadline>      reply wait <deadline> in seconds
  -W <timeout>       time to wait for response

IPv4 options:
  -4                 use IPv4
  -b                 allow pinging broadcast
  -R                 record route
  -T <timestamp>     define timestamp, can be one of <tsonly|tsandaddr|tsprespec>

IPv6 options:
  -6                 use IPv6
  -F <flowlabel>     define flow label, default is random
  -N <nodeinfo opt>  use icmp6 node info query, try <help> as argument
```

## Task 6 - Traceroute (Networking Tools):

- Traceroute allows you to see every intermediate step between your computer and the resource that you requested.

```
Usage:
  traceroute [ -46dFITnreAUDV ] [ -f first_ttl ] [ -g gate,... ] [ -i device ] [ -m max_ttl ] [ -N squeries ] [ -p port ] [ -t tos ] [ -l flow_label ] [ -w MAX,HERE,NEAR ] [ -q nqueries ] [ -s src_addr ] [ -z sendwait ] [ --fwmark=num ] host [ packetlen ]
Options:
  -4                          Use IPv4
  -6                          Use IPv6
  -d  --debug                 Enable socket level debugging
  -F  --dont-fragment         Do not fragment packets
  -f first_ttl  --first=first_ttl
                              Start from the first_ttl hop (instead from 1)
  -g gate,...  --gateway=gate,...
                              Route packets through the specified gateway
                              (maximum 8 for IPv4 and 127 for IPv6)
  -I  --icmp                  Use ICMP ECHO for tracerouting
  -T  --tcp                   Use TCP SYN for tracerouting (default port is 80)
  -i device  --interface=device
                              Specify a network interface to operate with
  -m max_ttl  --max-hops=max_ttl
                              Set the max number of hops (max TTL to be
                              reached). Default is 30
  -N squeries  --sim-queries=squeries
                              Set the number of probes to be tried
                              simultaneously (default is 16)
  -n                          Do not resolve IP addresses to their domain names
  -p port  --port=port        Set the destination port to use. It is either
                              initial udp port value for "default" method
                              (incremented by each probe, default is 33434), or
                              initial seq for "icmp" (incremented as well,
                              default from 1), or some constant destination
                              port for other methods (with default of 80 for
                              "tcp", 53 for "udp", etc.)
  -t tos  --tos=tos           Set the TOS (IPv4 type of service) or TC (IPv6
                              traffic class) value for outgoing packets
  -l flow_label  --flowlabel=flow_label
                              Use specified flow_label for IPv6 packets
  -w MAX,HERE,NEAR  --wait=MAX,HERE,NEAR
                              Wait for a probe no more than HERE (default 3)
                              times longer than a response from the same hop,
                              or no more than NEAR (default 10) times than some
                              next hop, or MAX (default 5.0) seconds (float
                              point values allowed too)
  -q nqueries  --queries=nqueries
                              Set the number of probes per each hop. Default is
                              3
  -r                          Bypass the normal routing and send directly to a
                              host on an attached network
  -s src_addr  --source=src_addr
                              Use source src_addr for outgoing packets
  -z sendwait  --sendwait=sendwait
                              Minimal time interval between probes (default 0).
                              If the value is more than 10, then it specifies a
                              number in milliseconds, else it is a number of
                              seconds (float point values allowed too)
  -e  --extensions            Show ICMP extensions (if present), including MPLS
  -A  --as-path-lookups       Perform AS path lookups in routing registries and
                              print results directly after the corresponding
                              addresses
  -M name  --module=name      Use specified module (either builtin or external)
                              for traceroute operations. Most methods have
                              their shortcuts (`-I' means `-M icmp' etc.)
  -O OPTS,...  --options=OPTS,...
                              Use module-specific option OPTS for the
                              traceroute module. Several OPTS allowed,
                              separated by comma. If OPTS is "help", print info
                              about available options
  --sport=num                 Use source port num for outgoing packets. Implies
                              `-N 1'
  --fwmark=num                Set firewall mark for outgoing packets
  -U  --udp                   Use UDP to particular port for tracerouting
                              (instead of increasing the port per each probe),
                              default port is 53
  -UL                         Use UDPLITE for tracerouting (default dest port
                              is 53)
  -D  --dccp                  Use DCCP Request for tracerouting (default port
                              is 33434)
  -P prot  --protocol=prot    Use raw packet of protocol prot for tracerouting
  --mtu                       Discover MTU along the path being traced. Implies
                              `-F -N 1'
  --back                      Guess the number of hops in the backward path and
                              print if it differs
  -V  --version               Print version info and exit
  --help                      Read this help and exit

Arguments:
+     host          The host to traceroute to
      packetlen     The full packet length (default is the length of an IP
                    header plus 40). Can be ignored or increased to a minimal
                    allowed value
```

## Task 7 - WHOIS (Networking Tools):

- Domains are used to point and save IP addresses so that they can be easily accessed.

- *whois* is a tool to query who a domain name is registered to.

- https://www.whois.com/whois/ is web version of whois tool.

## Task 8 - dig (Networking Tools):

- Dig allows us to manually query recursive DNS servers of our choice for information about domains.

- It is a very useful tool for network troubleshooting.

- Details for a recursive DNS server are stored in your router.

- First place a computer would look to find the IP address of a domain is *local cache*.

- If the domain isn't stored in the cache, the recursive server will pass the request on to a *root name* server.

- When a TLD server receives your request for information, the server passes it down to an appropriate Authoritative name server.

- Authoritative name servers are used to store DNS records for domains directly.

- The **TTL** (Time To Live in seconds) of the record tells your computer when to stop considering the record as being valid.

- Top-Level Domain (TLD) servers are split up into extensions. For example: `.com`, `.co.uk`


