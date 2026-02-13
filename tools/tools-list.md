# Outils pour la PNPT

## Reconnaissance & OSINT

| Outil          | Usage                              |
|----------------|------------------------------------|
| theHarvester   | Collecte emails, sous-domaines     |
| Sublist3r      | Enumeration sous-domaines          |
| Amass          | Enumeration avancee                |
| Sherlock       | Recherche comptes par username     |
| Recon-ng       | Framework OSINT                    |

## Scanning & Enumeration

| Outil          | Usage                              |
|----------------|------------------------------------|
| Nmap           | Scan de ports et services          |
| Masscan        | Scan de ports ultra-rapide         |
| enum4linux     | Enumeration SMB/NetBIOS            |
| smbclient      | Client SMB                         |
| smbmap         | Cartographie SMB                   |
| rpcclient      | Client RPC                         |
| ldapsearch     | Requetes LDAP                      |
| dnsenum        | Enumeration DNS                    |

## Web

| Outil          | Usage                              |
|----------------|------------------------------------|
| Gobuster       | Brute force directories/DNS/vhost  |
| Feroxbuster    | Brute force directories            |
| Nikto          | Scan vulns web                     |
| Burp Suite     | Proxy d'interception               |
| wfuzz          | Fuzzing web                        |

## Exploitation

| Outil          | Usage                              |
|----------------|------------------------------------|
| Metasploit     | Framework d'exploitation           |
| msfvenom       | Generation de payloads             |
| searchsploit   | Recherche d'exploits (ExploitDB)   |

## Post-Exploitation

| Outil          | Usage                              |
|----------------|------------------------------------|
| Mimikatz       | Dump credentials Windows           |
| BloodHound     | Cartographie AD                    |
| PowerView      | Enumeration AD (PowerShell)        |
| Rubeus         | Attaques Kerberos                  |
| SharpHound     | Collecteur pour BloodHound         |

## Cracking

| Outil          | Usage                              |
|----------------|------------------------------------|
| Hashcat        | Cracking de hashes (GPU)           |
| John the Ripper| Cracking de hashes                 |
| Hydra          | Brute force en ligne               |

## Impacket Suite

| Outil           | Usage                             |
|-----------------|-----------------------------------|
| psexec.py       | Execution distante (SMB)          |
| wmiexec.py      | Execution distante (WMI)          |
| smbexec.py      | Execution distante (SMB)          |
| secretsdump.py  | Dump de credentials               |
| GetUserSPNs.py  | Kerberoasting                     |
| GetNPUsers.py   | AS-REP Roasting                   |
| ntlmrelayx.py   | Relay NTLM                        |
| ticketer.py     | Creation de tickets Kerberos      |

## Privilege Escalation

| Outil                     | Usage                        |
|---------------------------|------------------------------|
| LinPEAS                   | Enumeration privesc Linux    |
| WinPEAS                   | Enumeration privesc Windows  |
| PowerUp                   | Privesc Windows (PowerShell) |
| linux-exploit-suggester   | Suggestions kernel exploits  |
| Seatbelt                  | Enumeration securite Windows |
| PrintSpoofer              | Potato attack (SeImpersonate)|

## Pivoting

| Outil          | Usage                              |
|----------------|------------------------------------|
| Chisel         | Tunneling TCP/SOCKS                |
| Ligolo-ng      | Tunneling avance                   |
| sshuttle       | VPN over SSH                       |
| Proxychains    | Routage via proxy SOCKS            |

## Networking

| Outil          | Usage                              |
|----------------|------------------------------------|
| Responder      | LLMNR/NBT-NS poisoning            |
| mitm6          | IPv6 DNS takeover                  |
| CrackMapExec   | Swiss army knife AD                |
| Evil-WinRM     | Shell WinRM                        |

## Notes & Reporting

| Outil          | Usage                              |
|----------------|------------------------------------|
| CherryTree     | Prise de notes                     |
| Obsidian       | Prise de notes markdown            |
| Flameshot      | Screenshots                        |
| Pwndoc         | Generation de rapports             |
