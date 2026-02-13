# Report Writing

## Structure d'un rapport de pentest

### 1. Page de garde
- Nom du client
- Type de test (externe, interne, AD)
- Dates du test
- Classification (confidentiel)

### 2. Resume executif (Executive Summary)
- Resume non technique pour la direction
- Posture de securite globale
- Risques principaux identifies
- Recommandations prioritaires

### 3. Methodologie
- Approche utilisee (OWASP, PTES, etc.)
- Outils utilises
- Scope et limitations

### 4. Trouvailles (Findings)

Pour chaque vulnerabilite :

| Element            | Description                              |
|--------------------|------------------------------------------|
| **Titre**          | Nom clair de la vulnerabilite            |
| **Severite**       | Critique / Haute / Moyenne / Basse / Info |
| **CVSS Score**     | Score numerique si applicable            |
| **Description**    | Explication de la vulnerabilite          |
| **Impact**         | Consequences si exploitee                |
| **Systemes**       | Machines / services affectes             |
| **Preuve**         | Screenshots, commandes, outputs          |
| **Remediation**    | Comment corriger                         |
| **References**     | CVE, liens utiles                        |

### 5. Annexes
- Liste complete des IPs/domaines testes
- Outputs de scans
- Liste des outils et versions

## Conseils pour l'examen PNPT

- Le rapport est une partie **critique** de l'examen
- Prendre des **screenshots de chaque etape**
- Documenter les **commandes exactes** utilisees
- Etre clair et professionnel
- Montrer le **chemin d'attaque complet** (de la recon au DA)
- Proposer des **remediations realistes**
- Relire et corriger les fautes

## Severite des vulnerabilites

| Severite  | Exemples                                              |
|-----------|-------------------------------------------------------|
| Critique  | RCE, acces admin, compromise du domaine               |
| Haute     | SQLi, credentials par defaut, privesc                  |
| Moyenne   | XSS stocke, information disclosure sensible            |
| Basse     | XSS reflecte, headers de securite manquants            |
| Info      | Versions exposees, bonnes pratiques non suivies         |

## Outils pour le rapport

- **Markdown** ou **Word/LibreOffice** pour la redaction
- **Flameshot / Greenshot** pour les screenshots
- **CherryTree / Obsidian** pour les notes pendant le test
- **Pwndoc** : generateur de rapports de pentest
