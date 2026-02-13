# PNPT Exam Tips & Strategie

## Format de l'examen

| Element              | Detail                                      |
|----------------------|---------------------------------------------|
| Duree pentest        | **5 jours** (120 heures)                    |
| Duree rapport        | **2 jours** supplementaires                 |
| Debrief              | **15 minutes** en video                     |
| Proctoring           | Aucun (non supervise)                       |
| Outils               | **Tous autorises** (Metasploit, scripts...) |
| Flags / QCM          | **Aucun** - c'est un vrai pentest           |
| Retake               | **1 gratuit** inclus avec le voucher        |
| Expiration            | La certification **n'expire jamais**        |

## Objectif de l'examen

Compromettre le **Domain Controller** en partant de l'exterieur :
1. OSINT sur la cible
2. Acces initial au reseau
3. Enumeration interne
4. Mouvement lateral
5. Escalade de privileges
6. Compromission du Domain Controller
7. Rapport professionnel
8. Debrief client

## Gestion du temps (5 jours)

### Jour 1 : Recon & OSINT
- Lire attentivement la **lettre d'engagement** (scope, regles)
- OSINT sur la cible
- Scan externe
- Identifier les points d'entree

### Jours 2-3 : Exploitation & AD
- Obtenir un acces initial
- Enumeration interne (BloodHound)
- Attaques AD (Kerberoast, relay, etc.)
- Mouvement lateral
- Escalade de privileges

### Jour 4 : Compromission & Verification
- Compromettre le Domain Controller
- Verifier et documenter tout le chemin d'attaque
- Tenter des chemins alternatifs
- Prendre les derniers screenshots

### Jour 5 : Rapport (debut)
- Commencer la redaction
- Organiser les preuves

### Jours 6-7 : Rapport & Debrief
- Finaliser le rapport
- Relire et corriger
- Preparer la presentation pour le debrief

## Conseils critiques

### Pendant le pentest

- **Lire le scope attentivement** : ne pas attaquer hors perimetre
- **Documenter TOUT** en temps reel : commandes, outputs, screenshots
- **Ne pas s'acharner** sur une piste pendant des heures : si ca semble trop complique, explorer d'autres voies
- **Ce n'est PAS un CTF** : c'est un environnement AD realiste
- **Enumerer, enumerer, enumerer** : la cle est dans l'enumeration
- **Tester ses payloads** avant de les envoyer (AV evasion)
- Utiliser **CherryTree, Obsidian ou des notes markdown** pour tout noter

### Pour le rapport

- **Screenshots a chaque etape** (avant/apres exploitation)
- Montrer le **chemin d'attaque complet**
- **Executive summary** non technique
- **Remediations realistes** pour chaque trouvaille
- Relire pour les fautes d'orthographe
- Utiliser un format professionnel

### Pour le debrief

- **15 minutes max**, pas plus
- Presenter comme a un **client non technique**
- Connaitre son rapport par coeur
- Avoir des **remediations solides**
- Etre pret aux questions

## Erreurs courantes

- Ne pas lire le scope correctement
- Passer trop de temps sur une seule piste
- Ne pas prendre de screenshots
- Rapport trop technique sans executive summary
- Oublier les remediations dans le rapport
- Depasser le temps du debrief
- Payloads detectes par l'AV (pas de bypass)

## Labs de pratique recommandes

### TryHackMe

- **Attacking Active Directory** (parcours)
- **Hacking Active Directory** (room)
- **Wreath** (pivoting)
- **Blue / Ice / Alfred / Steel Mountain** (rooms Windows)

### HackTheBox

- Machines AD : Forest, Sauna, Cascade, Monteverde, Resolute, Blackfield
- **Search** (AV evasion + Nishang)
- **Active, Mantis** (Kerberos)
- **Pro Labs : Offshore, RastaLabs** (si budget)

### TCM Security Labs

- Les labs inclus dans les cours PEH sont **directement alignes** avec l'examen
- **Faire et refaire les labs AD** du cours Practical Ethical Hacking

### Autres

- **VulnHub** : machines AD
- **DVWA** : pratique web basique
- **PortSwigger Web Security Academy** : SQLi, XSS, etc.

## Checklist avant l'examen

- [ ] Cours PEH termine et labs faits
- [ ] A l'aise avec les attaques AD (relay, Kerberoast, etc.)
- [ ] Capable de bypass AV basique
- [ ] Capable d'utiliser BloodHound
- [ ] Maitrise de l'enumeration (Nmap, enum4linux, crackmapexec)
- [ ] Pivoting fonctionnel (Chisel ou Ligolo)
- [ ] Sait ecrire un rapport professionnel
- [ ] A pratique le debrief oral
- [ ] Notes / cheatsheets pretes
- [ ] VM Kali a jour avec tous les outils installes
