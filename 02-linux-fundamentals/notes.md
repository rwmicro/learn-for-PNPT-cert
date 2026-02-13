# Linux Fundamentals

## Commandes essentielles

```bash
# Navigation
pwd                     # repertoire courant
ls -la                  # lister fichiers (details + caches)
cd /chemin              # changer de repertoire

# Fichiers
cat fichier             # afficher contenu
less fichier            # afficher page par page
find / -name "*.conf"   # chercher des fichiers
locate fichier          # recherche rapide (base de donnees)
grep -ri "motif" /dir   # recherche dans fichiers

# Permissions
chmod 755 fichier       # rwxr-xr-x
chown user:group fic    # changer proprietaire
```

## Permissions

```
r = 4, w = 2, x = 1
rwx = 7, rw- = 6, r-x = 5, r-- = 4
```

## Fichiers importants

| Fichier              | Description                     |
|----------------------|---------------------------------|
| `/etc/passwd`        | Utilisateurs du systeme         |
| `/etc/shadow`        | Hash des mots de passe          |
| `/etc/hosts`         | Resolution DNS locale           |
| `/etc/crontab`       | Taches planifiees               |
| `/etc/sudoers`       | Regles sudo                     |
| `/tmp`               | Fichiers temporaires (world-writable) |
| `/var/log`           | Logs systeme                    |

## Services

```bash
systemctl start/stop/status service
service service start/stop/status
```

## Transfert de fichiers

```bash
# Serveur HTTP rapide
python3 -m http.server 80

# Wget / Curl
wget http://ip/fichier
curl http://ip/fichier -o output

# SCP
scp fichier user@ip:/chemin
```
