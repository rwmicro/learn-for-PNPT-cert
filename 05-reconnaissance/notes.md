# Reconnaissance

## Reconnaissance passive

Pas de contact direct avec la cible.

- Whois, DNS public, Google Dorks
- Shodan, Censys
- Reseaux sociaux, LinkedIn
- Voir section OSINT pour les details

## Reconnaissance active

Contact direct avec la cible (detectable).

### Decouverte d'hotes

```bash
# Ping sweep
nmap -sn 192.168.1.0/24

# ARP scan (reseau local)
arp-scan -l
netdiscover -r 192.168.1.0/24
```

### Scan de ports

```bash
# Scan rapide
nmap -T4 -p- IP

# Scan avec detection de services et scripts
nmap -sC -sV -p PORTS IP

# Scan UDP
nmap -sU --top-ports 50 IP

# Scan furtif (SYN)
nmap -sS IP
```

### Enumeration DNS

```bash
# Zone transfer
dig axfr @ns.cible.com cible.com
host -t axfr cible.com ns.cible.com

# Brute force sous-domaines
dnsenum cible.com
fierce --domain cible.com
```

### Enumeration web

```bash
# Directory brute force
gobuster dir -u http://IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
feroxbuster -u http://IP -w wordlist.txt
dirb http://IP

# Scan de vulnerabilites web
nikto -h http://IP
```
