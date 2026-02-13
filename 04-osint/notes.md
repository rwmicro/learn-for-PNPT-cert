# OSINT (Open Source Intelligence)

## Methodologie

1. Definir la cible et le scope
2. Collecte passive d'informations
3. Analyse et correlation
4. Documentation des trouvailles

## Outils et techniques

### Emails et utilisateurs

- **Hunter.io** : trouver des emails lies a un domaine
- **Phonebook.cz** : recherche d'emails, domaines, URLs
- **theHarvester** : collecte d'emails, sous-domaines, IPs
- **LinkedIn** : enumeration d'employes

### Domaines et sous-domaines

- **Whois** : `whois domaine.com`
- **DNSDumpster** : cartographie DNS
- **Sublist3r** : enumeration de sous-domaines
- **crt.sh** : certificats SSL (sous-domaines)
- **Amass** : enumeration avancee

### Recherche web

- **Google Dorks** :
  - `site:cible.com`
  - `filetype:pdf site:cible.com`
  - `intitle:"index of" site:cible.com`
  - `inurl:admin site:cible.com`
- **Wayback Machine** : archives de sites web

### Reseaux sociaux

- **Sherlock** : recherche de comptes par username
- **Social Searcher** : recherche sur reseaux sociaux

### Breaches et credentials

- **HaveIBeenPwned** : verifier si un email est dans une fuite
- **DeHashed** : recherche dans les breaches

### Images et metadata

- **ExifTool** : extraction de metadonnees
- **Google Reverse Image Search**
- **TinEye**

## Commandes utiles

```bash
# theHarvester
theHarvester -d cible.com -b google,linkedin,bing

# Sublist3r
sublist3r -d cible.com

# Whois
whois cible.com

# DNS
dig cible.com any
nslookup cible.com
```
