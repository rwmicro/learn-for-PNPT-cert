# Client Debrief / Presentation

## Format de l'examen PNPT

Apres les 5 jours de pentest et 2 jours de redaction :
- **Debrief de 15 minutes** en video avec les assesseurs de TCM Security
- Les assesseurs sont des **pentesters seniors**
- Ils peuvent poser des **questions** sur tes trouvailles et remediations

## Preparer sa presentation

### Structure recommandee (15 min max)

1. **Introduction** (1-2 min)
   - Se presenter brievement
   - Rappeler le scope de l'engagement
   - Resume de l'approche

2. **Resume executif** (2-3 min)
   - Posture de securite globale du client
   - Risques principaux identifies
   - Niveau de severite global

3. **Chemin d'attaque** (5-7 min)
   - Presenter le chemin complet : recon -> acces initial -> privesc -> DA
   - Montrer les etapes cles avec des captures d'ecran
   - Expliquer l'impact de chaque etape
   - **Utiliser un langage non technique** (c'est un debrief CLIENT)

4. **Remediations** (3-4 min)
   - Recommandations prioritaires
   - Quick wins vs changements long terme
   - Montrer que tu comprends le contexte business

5. **Questions** (2-3 min)
   - Etre pret a justifier tes choix techniques
   - Etre pret a expliquer des remediations alternatives

### Support de presentation

- **PowerPoint / Google Slides** ou directement ton rapport
- Garder les slides simples et visuels
- Inclure des screenshots cles
- Pas trop de texte par slide
- Schema du chemin d'attaque (attack chain) tres apprecie

## Conseils cles

### Langage

- Parler comme si tu presentais a un **dirigeant non technique**
- Eviter le jargon technique excessif
- Expliquer l'**impact business** : "Un attaquant pourrait acceder a toutes les donnees de l'entreprise" plutot que "J'ai DCSync le hash du krbtgt"
- Rester **professionnel et confiant**

### Ce qui est evalue

- Capacite a communiquer clairement
- Comprehension des trouvailles (pas juste copier-coller des commandes)
- Qualite des remediations proposees
- Professionnalisme

### Erreurs a eviter

- Depasser les 15 minutes
- Etre trop technique sans expliquer l'impact
- Ne pas avoir de remediations
- Lire ses notes mot pour mot
- Ne pas connaitre son propre rapport

## Entrainement

- **Apres chaque lab**, rediger un mini executive summary
- **S'enregistrer** en presentant pour travailler le timing
- **Presenter a un ami** non technique pour verifier la clarte
- Preparer des **reponses aux questions classiques** :
  - "Quelle est la vulnerabilite la plus critique ?"
  - "Par ou commenceriez-vous la remediation ?"
  - "Combien de temps un attaquant mettrait-il ?"
  - "Comment avez-vous contourne l'antivirus ?"
