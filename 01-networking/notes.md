# Networking Fundamentals

## Modele OSI (7 couches)

| Couche | Nom          | Protocoles / Concepts         |
|--------|--------------|-------------------------------|
| 7      | Application  | HTTP, FTP, SSH, DNS, SMTP     |
| 6      | Presentation | SSL/TLS, JPEG, ASCII          |
| 5      | Session      | NetBIOS, RPC                  |
| 4      | Transport    | TCP, UDP                      |
| 3      | Network      | IP, ICMP, ARP                 |
| 2      | Data Link    | Ethernet, MAC addresses       |
| 1      | Physical     | Cables, hubs, signaux         |

## TCP vs UDP

- **TCP** : orienté connexion, fiable (3-way handshake : SYN, SYN-ACK, ACK)
- **UDP** : sans connexion, rapide, pas de garantie de livraison

## Ports courants

| Port  | Service        |
|-------|----------------|
| 21    | FTP            |
| 22    | SSH            |
| 23    | Telnet         |
| 25    | SMTP           |
| 53    | DNS            |
| 80    | HTTP           |
| 88    | Kerberos       |
| 110   | POP3           |
| 135   | MSRPC          |
| 139   | NetBIOS        |
| 143   | IMAP           |
| 389   | LDAP           |
| 443   | HTTPS          |
| 445   | SMB            |
| 636   | LDAPS          |
| 3306  | MySQL          |
| 3389  | RDP            |
| 5985  | WinRM (HTTP)   |
| 5986  | WinRM (HTTPS)  |

## Subnetting

- `/24` = 255.255.255.0 = 256 adresses (254 utilisables)
- `/16` = 255.255.0.0 = 65 536 adresses
- `/8`  = 255.0.0.0 = 16 777 216 adresses

### Plages privees

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`
