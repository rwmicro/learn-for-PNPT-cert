# Windows Fundamentals

## Commandes utiles

```powershell
# Informations systeme
systeminfo
hostname
whoami /all
net user
net localgroup administrators

# Reseau
ipconfig /all
netstat -ano
arp -a
route print

# Services
sc query
tasklist /svc
wmic service list brief
```

## Fichiers / Emplacements importants

| Chemin                                    | Description              |
|-------------------------------------------|--------------------------|
| `C:\Windows\System32\config\SAM`          | Base SAM (hashes locaux) |
| `C:\Windows\System32\drivers\etc\hosts`   | Resolution DNS locale    |
| `C:\Users\<user>\AppData`                 | Donnees applicatives     |
| `C:\Windows\Temp`                         | Fichiers temporaires     |

## Registre Windows

```
HKLM\SAM                 # Hashes locaux
HKLM\SYSTEM              # Cle de boot (pour dechiffrer SAM)
HKLM\SOFTWARE            # Config logiciels
HKCU\                    # Config utilisateur courant
```

## PowerShell utile

```powershell
# Telecharger un fichier
Invoke-WebRequest -Uri http://ip/fichier -OutFile C:\Temp\fichier
(New-Object Net.WebClient).DownloadFile('http://ip/fichier','C:\Temp\fichier')

# Execution de scripts
Set-ExecutionPolicy Bypass -Scope Process
powershell -ep bypass

# Enumeration AD basique
Get-ADUser -Filter *
Get-ADComputer -Filter *
Get-ADGroup -Filter *
```
