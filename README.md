# PMS Manager — L'Océane

Code source du PMS (Property Management System) de la Résidence Hôtelière L'Océane (Kribi), extrait depuis le Worker Cloudflare en production.

## Architecture

- **Déploiement actuel (production) :** Worker Cloudflare nommé `pms`, servi sur `pms.kmertubes.com/oceane`.
- **Structure :** une seule page HTML (`src/app.html`, ~470 Ko) contenant HTML + CSS + JS, sans framework ni étape de build. Elle est injectée telle quelle dans le Worker comme chaîne de caractères (`src/worker.js`).
- **Backend de données :** Supabase, projet `ahsjgydituniiiregecc` (tables : `clients`, `reservations`, `ventes`, `vente_lignes`, `paiements`, `achats`, `achat_lignes`, `clotures`, `mouvements_caisse`, `produits`, `formules`, `espaces`, `caisses`, `poles`, `articles_stock`, `sessions_caisse`, `factures`).
- **Deux pôles gérés par l'app :**
  - **Résidence** (L'Océane) — Hébergement, Bar, Piscine, Restaurant, Restaurant mobile, Loisirs.
  - **Luxury Beauty - Paris / Institut** — Institut Soins, Institut Boutique.

## ⚠️ Règle absolue

**Ne jamais modifier quoi que ce soit lié à l'Institut / Luxury Beauty - Paris** (pôle, caisses, écrans, requêtes). Tout développement doit rester strictement scopé à la Résidence.

## Fichiers

- `src/worker.js` — Worker Cloudflare complet (export par défaut, gère `/icon.svg`, `/manifest.json`, et sert `HTML` en catch-all).
- `src/app.html` — Version lisible (non échappée) du contenu HTML/JS embarqué dans le Worker. C'est le fichier à éditer pour toute évolution de l'interface.

## Méthode de travail

1. Toute modification se fait d'abord ici, dans ce dépôt.
2. Déploiement sur un **Worker de staging séparé** (pas `pms` en production) pour validation par Daniel.
3. Déploiement en production sur `pms` uniquement après validation explicite.

## Prochaine étape en cours

Ajout d'un tableau de bord natif (pas de dépendance externe à Claude) affichant, pour la Résidence : Date, Report, Hébergement, Bar, Piscine, Resto, Crédits, Dépenses, Versement, Solde en caisse — avec répartition Cash / Orange Money / MoMo / Acomptes, et historique consultable ligne par ligne (édition réservée à Daniel).
