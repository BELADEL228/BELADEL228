# Guide d'installation

Ce guide explique comment mettre ce kit en place sur ton propre profil GitHub, étape par étape.

## 1. Où placer chaque fichier

Le profil GitHub spécial (celui qui s'affiche en haut de `github.com/BELADEL228`) doit vivre dans **un dépôt qui porte exactement le même nom que ton pseudo GitHub**.

```
BELADEL228/                     ← nom du dépôt = ton pseudo GitHub
├── README.md                   ← affiché automatiquement sur ton profil
├── LICENSE
├── assets/
│   ├── banner.svg               ← bannière animée
│   ├── logo.svg                 ← monogramme "AB"
│   ├── background.svg           ← texture de fond réutilisable
│   └── metrics.svg              ← généré automatiquement (ne pas éditer à la main)
├── .github/
│   └── workflows/
│       ├── snake.yml
│       ├── metrics.yml
│       └── update.yml
└── docs/
    └── SETUP.md                 ← ce fichier
```

## 2. Créer le dépôt spécial

1. Sur GitHub, crée un nouveau dépôt **public** nommé exactement `BELADEL228` (identique à ton pseudo).
2. GitHub affichera automatiquement un encart "Add a README to your profile" — c'est le signe que le nom est correct.
3. Copie l'intégralité de ce kit (README, `assets/`, `.github/`, `LICENSE`, `docs/`) à la racine du dépôt.
4. Commit puis push sur la branche `main`.

```bash
git init
git remote add origin https://github.com/BELADEL228/BELADEL228.git
git add .
git commit -m "feat: profil GitHub premium"
git branch -M main
git push -u origin main
```

## 3. Activer GitHub Actions

1. Dans le dépôt, va dans l'onglet **Settings → Actions → General**.
2. Sous *Actions permissions*, sélectionne **Allow all actions and reusable workflows**.
3. Sous *Workflow permissions*, sélectionne **Read and write permissions** — les workflows `snake.yml`, `metrics.yml` et `update.yml` ont besoin d'écrire dans le dépôt (commit du serpent, des métriques, de l'activité récente).
4. Enregistre.

## 4. Générer automatiquement le serpent (`snake.yml`)

Ce workflow transforme ton calendrier de contributions en une animation de serpent, publiée sur une branche `output`.

- Il se déclenche automatiquement chaque jour à 03h00 UTC, à chaque `push` sur `main`, et peut être lancé manuellement (`Actions → Generate Snake Animation → Run workflow`).
- La première exécution crée la branche `output` toute seule — tu n'as rien à faire de plus.
- Le README pointe déjà vers `https://raw.githubusercontent.com/BELADEL228/BELADEL228/output/snake-dark.svg` : une fois le workflow exécuté une première fois, l'animation apparaît automatiquement.

## 5. Mettre à jour les statistiques (`metrics.yml`)

Ce workflow régénère `assets/metrics.svg`, le tableau de bord affiché dans la section **Tableau de métriques** du README.

1. Crée un **Personal Access Token (classic)** sur `github.com/settings/tokens` avec le scope `repo` (et `read:user` si demandé).
2. Dans le dépôt, va dans **Settings → Secrets and variables → Actions → New repository secret**.
3. Nomme le secret `METRICS_TOKEN` et colle le token généré.
4. Le workflow tourne automatiquement chaque jour à 04h00 UTC, ou manuellement via `Actions → Generate GitHub Metrics → Run workflow`.

> Sans ce secret, le workflow s'exécutera avec des permissions limitées et certains plugins (langages, activité) peuvent échouer.

## 6. Rafraîchir l'activité récente (`update.yml`)

Ce workflow remplit automatiquement la section **Activité récente** du README, entre les balises :

```html
<!--START_SECTION:activity-->
<!--END_SECTION:activity-->
```

Il tourne toutes les 30 minutes sans configuration supplémentaire — le `GITHUB_TOKEN` fourni par défaut par GitHub Actions suffit.

## 7. Personnaliser

- **Liens de contact** : remplace les URL d'exemple (email, LinkedIn, X) dans la section *Me contacter* du README par tes vrais profils.
- **Projets** : ajuste les liens `github.com/BELADEL228/...` de la section *Projets phares* si le nom réel de tes dépôts diffère.
- **Palette** : les couleurs (`#05070C`, `#0B1220`, `#3D7DFF`, `#F5F7FA`) sont centralisées dans les fichiers SVG (`assets/`) et dans les paramètres d'URL des badges/widgets du README — modifie-les aux deux endroits si tu changes de palette.
- **Bannière / logo** : `assets/banner.svg` et `assets/logo.svg` sont des SVG lisibles et modifiables dans n'importe quel éditeur de texte ou dans Figma/Illustrator (import SVG).

## 8. Vérifier que tout fonctionne

- [ ] Le dépôt s'appelle exactement `BELADEL228`
- [ ] Le README s'affiche sur `github.com/BELADEL228`
- [ ] Les trois workflows sont visibles et verts dans l'onglet **Actions**
- [ ] La branche `output` existe et contient `snake-dark.svg`
- [ ] `assets/metrics.svg` a été commité automatiquement par le workflow
- [ ] La section *Activité récente* du README n'est plus vide
