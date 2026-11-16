# LaborIA - Bac à sable des outils

Ce dépôt contient le site statique qui rassemble des outils interactifs développés dans le cadre des travaux du LaborIA autour de l'intelligence artificielle et du travail. Il s'agit du bac à sable des outils, et non du site institutionnel du LaborIA : [laboria.ai](https://www.laboria.ai/).

## Outils

Les outils actuellement proposés sur la page d'accueil sont :

- **Autoportrait : l'IA dans mon quotidien** - un autodiagnostic individuel (environ 30 à 45 minutes) pour examiner ses usages de l'IA générative, leurs effets sur le travail et les questions qu'ils soulèvent. Le parcours comprend trois parties et un bilan.
- **Le travail réel de l'IA** - un jeu de rôle (environ 30 à 45 minutes, seul ou en binôme) pour décrire trois tâches, mesurer la place de l'IA et réfléchir aux transformations du travail réel.

Le parcours **Mon métier se transforme** est toujours présent dans le dépôt et inclus dans le build, mais il n'est pas proposé sur la page d'accueil car obsolète.

## Prérequis et installation

Le projet utilise Vite et nécessite Node.js (la publication automatique utilise Node.js 22).

```bash
npm install
```

## Développement

```bash
npm run dev
```

Ouvrez l'adresse locale affichée par Vite, généralement <http://localhost:5173>.

Pour vérifier le build de production en local :

```bash
npm run build
npm run preview
```

Le site généré se trouve dans `dist/`.

## Données utilisateurs

Les réponses des outils Autoportrait et Travail réel sont enregistrées dans le `localStorage` du navigateur. Elles ne sont pas envoyées à un serveur. Les deux outils permettent d'exporter une sauvegarde et de la réimporter depuis leur notice ; l'Autoportrait propose également un récapitulatif imprimable et un export texte.

## Structure du dépôt

```text
.
├── index.html                    # Accueil et registre des outils affichés
├── package.json                  # Dépendances et commandes npm
├── vite.config.js                # Entrées HTML du build multi-pages
├── public/
│   ├── assets/                   # Logos et illustrations
│   ├── data/
│   │   └── arbre_decision.csv    # Contenu de l'arbre de décision
│   └── CNAME                     # Domaine personnalisé du site publié
├── src/
│   ├── css/style.css             # Styles communs
│   └── js/
│       ├── home.js, tools.js     # Page d'accueil et registre des outils
│       ├── autoportrait/         # Logique de l'autodiagnostic
│       ├── travail-reel/         # Logique du jeu de rôle
│       └── mon-metier/           # Logique de l'arbre de décision (archivé)
├── tools/
│   ├── autoportrait-ia/          # Notice, parties 1 à 3 et ressources
│   ├── travail-reel-ia/          # Notice, étapes 1 à 4 et ressources
│   └── mon-metier-se-transforme/ # Présentation, tâches, arbre et exploration
└── .github/workflows/deploy.yml  # Build et déploiement GitHub Pages
```

## Déploiement

Le workflow [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) construit et publie le site sur GitHub Pages à chaque push sur `main`. Il peut aussi être lancé manuellement depuis l'onglet **Actions**.

Dans **Settings → Pages**, configurez **Source : GitHub Actions**. Le domaine personnalisé est défini par `public/CNAME`, que Vite copie dans `dist/`.

Une publication manuelle est aussi disponible avec :

```bash
npm run deploy
```

Cette commande construit le site puis publie `dist/` avec `gh-pages`.
