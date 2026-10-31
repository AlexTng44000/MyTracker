# Mytracker

Frontend autonome de suivi de films et séries, inspiré du style de MyMangaTracker. React, TypeScript et Vite. Aucun backend, compte utilisateur ou service payant nécessaire.

## Démarrer

Node.js 24 recommandé :

```sh
npm ci
npm run dev
```

Sous Windows PowerShell, utiliser `npm.cmd ci` et `npm.cmd run dev` si les scripts PowerShell sont bloqués.

`npm run lint` vérifie le code ; `npm run build` génère le dossier `dist`. `npm run preview` permet de tester ce build.

## GitHub Pages

Créer un dépôt vide nommé par exemple `Mytracker`, envoyer ces fichiers sur sa branche `main`, puis choisir **Settings → Pages → Build and deployment → Source → GitHub Actions**. Le workflow fourni construit et déploie le site.

Le chemin de base est calculé depuis le nom du dépôt dans GitHub Actions, y compris après un renommage. Les routes utilisent un fragment (`#/work/tv:1396`) pour fonctionner sans serveur de réécriture. Pour un autre hébergeur statique, publier le dossier `dist`.

## Fonctionnalités

- Catalogue local de démonstration : 6 films et 6 séries, recherche et filtres.
- Bibliothèque unifiée, favoris, suppression directe, notes de 1 à 10.
- Statuts et progression des séries sous forme de nombre total d’épisodes vus, toutes saisons confondues.
- Statistiques, français/anglais pour l’interface et affichage adaptatif.
- Barre compacte de filtres flottante sans modification de la hauteur du contenu.
- Sauvegarde JSON exportable et import validé (fusion avec confirmation).

Les descriptions et genres du catalogue sont actuellement en français. Les fiches sont des exemples fixes, sans affiches externes et sans actualisation automatique. Les nombres d’épisodes sont des instantanés hors épisodes spéciaux ; ce n’est pas un catalogue exhaustif. Les liens TMDB ouvrent les fiches correspondantes, sans intégrer son API. L’ajout d’une recherche en ligne pourra faire l’objet d’une prochaine évolution.

## Données personnelles

La bibliothèque est stockée dans le localStorage du navigateur. Elle n’est ni synchronisée entre appareils ni sauvegardée sur GitHub. Une navigation privée, un nettoyage du navigateur ou un changement d’adresse du site peut rendre ces données indisponibles. Exporter régulièrement la bibliothèque, puis importer le JSON sur un autre appareil.

Aucun mot de passe ni clé API nécessaire. Le suivi est manuel : ouvrir une plateforme de streaming ne met pas automatiquement à jour la progression. Les sauvegardes importées remplacent les œuvres de même identifiant et conservent les autres.

## Personnalisation

Le nom provisoire apparaît dans `src/App.tsx`, `index.html` et cette documentation. Couleurs et mise en page : `src/style.css`. Le dépôt MangaTrack d’origine reste indépendant.

## Tests navigateur

Après `npm run build`, lancer `npm run preview -- --host 127.0.0.1 --port 5182` dans un terminal. Dans un second : `npx playwright install chromium`, puis `npm run test:smoke`. Le test couvre le catalogue, la persistance, les filtres, la suppression, la progression, les langues, l’export, le refus d’un import invalide et les largeurs 320 à 1 440 pixels.
