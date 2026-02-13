# Scanning & Enumeration

## Nmap - Cheat Sheet

```bash
nmap -sC -sV -oN scan.txt IP        # Scan standard + output
nmap -T4 -p- IP                      # Tous les ports
nmap -sU --top-ports 20 IP           # UDP
nmap -A IP                           # Agressif (OS + scripts + traceroute)
nmap --script=vuln IP                # Scripts de vulnerabilites
```

## Enumeration par service

### SMB (445)

```bash
smbclient -L //IP/ -N                        # Lister les shares (anonyme)
smbclient //IP/share -N                      # Se connecter a un share
smbmap -H IP                                 # Permissions des shares
enum4linux -a IP                             # Enumeration complete
crackmapexec smb IP --shares                 # Lister shares
crackmapexec smb IP -u '' -p '' --shares     # Acces anonyme
```

### HTTP/HTTPS (80/443)

```bash
whatweb http://IP                             # Technologies web
gobuster dir -u http://IP -w wordlist        # Directories
wfuzz -c -w wordlist -u http://IP/FUZZ       # Fuzzing
```

### FTP (21)

```bash
ftp IP                   # Connexion (essayer anonymous:anonymous)
nmap --script=ftp-anon IP
```

### SSH (22)

```bash
ssh user@IP
hydra -l user -P wordlist.txt ssh://IP       # Brute force
```

### DNS (53)

```bash
dig axfr @IP domaine.com                     # Zone transfer
dnsrecon -d domaine.com -t axfr
```

### SMTP (25)

```bash
smtp-user-enum -M VRFY -U users.txt -t IP    # Enumeration d'utilisateurs
nmap --script=smtp-enum-users IP
```

### SNMP (161 UDP)

```bash
snmpwalk -v2c -c public IP
onesixtyone -c community.txt IP
```

### LDAP (389)

```bash
ldapsearch -x -H ldap://IP -b "dc=domaine,dc=com"
nmap --script=ldap-search IP
```

### RPC (135)

```bash
rpcclient -U "" -N IP
  > enumdomusers
  > enumdomgroups
  > queryuser 0x1f4
```
