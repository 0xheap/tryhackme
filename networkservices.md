# Network Services

## Understanding SMB

- SMB (Server Message Block Protocol) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.

- Samba, an open source server that supports the SMB protocol, was released for Unix systems.

- Clients connect with TCP

## Enumerating SMB

- Enum4linux is automation tool used to enumerate SMB shares on both Windows and Linux systems

## Understanding FTP

- In an Active FTP connection, the client opens a port and listens. The server is required to actively connect to it.

- In a Passive FTP connection, the server opens a port and listens (passively) and the client connects to it.

## Exploiting FTP

- Hydra is a password cracker tool.

- `hydra -t 4 -l user -P /usr/share/wordlists/rockyou.txt -vV target_ip ftp`

- `get file.txt -` to show file content.
