# ⚙️ N8N Workflows

> Une sélection de mes workflows n8n, construits pour des cas réels en entreprise, puis nettoyés de toute donnée sensible pour pouvoir être réutilisés.

**Auteur :** [Mourad AMOUSSA](https://mourad2511.github.io) · AI & Automation Engineer
**Contexte :** ces workflows viennent de mon alternance chez Ekstere (vélos reconditionnés, 3 sites, 50 000 références), où mes automatisations font gagner **40 à 50 heures par semaine** aux équipes, avec **100 % d'adoption**.

---

## 📂 Contenu

| Workflow | Ce qu'il fait | Nœuds | Résultat |
|:--|:--|:--:|:--|
| **Annonces produit automatisées** | Photos déposées, récupération de la fiche technique via l'API Magento, rédaction SEO par Gemini, extraction des attributs par OpenAI, contrôles qualité, publication | 75 | **-85 %** de temps de création, **×8** annonces publiées, 95 % des vélos en ligne en moins de 24 h |
| **Enrichissement de fiches produit par LLM** | Recherche web automatisée, score de confiance par site, nettoyage HTML, extraction structurée par champ, relecture humaine ciblée (orchestrateur + sous-workflow) | 24 + 52 | **0,02 €** par référence au lieu de 2 €, sur 50 000 références |
| **Assistant IA interne multi-agents (RAG)** | Question posée dans Google Chat, classification d'intention, orchestration LangGraph vers 4 agents (marketing, SEO, comptes rendus, support), recherche dans la documentation interne | multi-agents | Réponse en **moins de 5 s**, **plus de 60 %** des demandes traitées sans intervention, 100 % d'adoption |
| **Surveillance quotidienne des prix** | Lecture paginée du catalogue Magento, comparaison à l'historique, règles métier de détection des écarts, classement par urgence, alerte envoyée au bon site | 66 + 30 | Erreurs de prix repérées chaque matin, **sans aucun contrôle manuel** |
| **Prospection B2B (Apollo + IA + CRM)** | Recherche d'entreprises, enrichissement, scoring IA sur 100 selon une grille métier, recherche des décideurs, création des fiches dans le CRM | 19 | Chaîne complète testée de bout en bout, jusqu'aux leads qualifiés dans le CRM |

---

## 🔍 Exemple : prospection B2B

```mermaid
flowchart LR
    A[Apollo<br/>recherche d'entreprises] --> B[Enrichissement<br/>des fiches]
    B --> C[Agent IA<br/>scoring /100]
    C -->|score ≥ 60| D[Décideurs<br/>emails vérifiés]
    D --> E[Dédoublonnage<br/>1 fiche par entreprise]
    E --> F[Création des leads<br/>dans le CRM]
    F -.-> G[Séquence email<br/>après validation humaine]
```

- **Scoring par IA** : l'agent note chaque entreprise sur 6 critères métier et justifie sa note. Seules les entreprises à 60 ou plus continuent.
- **Qualité des données** : seuls les emails vérifiés sont gardés, et les doublons sont fusionnés.
- **Contrôle humain** : l'inscription aux séquences email reste désactivée tant qu'un commercial n'a pas validé les leads.

---

## 🚀 Importer un workflow dans n8n

1. Télécharge le fichier `.json` du workflow.
2. Dans n8n, clique sur **Workflows → Import from File** et choisis le fichier.
3. Recrée tes propres identifiants (**Credentials**) : clés OpenAI, Apollo, CRM, Google… Aucun identifiant n'est fourni dans ce dépôt.
4. Remplace les valeurs marquées `A_REMPLACER` (identifiants de séquence, adresse d'envoi…).
5. Lance d'abord le workflow avec le nœud **Limite test** pour vérifier le résultat sur quelques éléments.

---

## 🔒 Données et sécurité

- Les exports ne contiennent **aucun mot de passe, token ni clé API**.
- Les données de test (noms, emails de prospects) ont été **supprimées**.
- Les identifiants sont gérés dans les Credentials de n8n, jamais en dur dans les nœuds.

---

## 🧰 Stack

`n8n` · `JavaScript` · `LangGraph` · `OpenAI` · `Gemini` · `Redis` · `Magento` · `Apify` · `Apollo` · `Close CRM` · `API REST` · `Google Workspace`

📬 [Portfolio](https://mourad2511.github.io) · [GitHub](https://github.com/Mourad2511) · [LinkedIn](https://www.linkedin.com/in/mourad-amoussa) · mourad1.amoussa@outlook.com
