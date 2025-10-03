# Ludovic Gacquer – Portfolio (Single Page)

Ce dépôt contient une page web unique (`index.html`) servant de portfolio professionnel pour **Ludovic Gacquer – Acteur · Réalisateur · Monteur**.

## Contenu de la page
- En-tête avec navigation fluide (scroll doux)
- Section Hero (identité + rôles + CTA showreel)
- Showreel / vidéo principale (YouTube)
- Biographie
- Compétences (acteur, réalisation, montage, narration…)
- Filmographie / Timeline (crédits structurés)
- Galerie de vidéos filtrable (chargée dynamiquement via l'API YouTube ou liste manuelle de secours)
- Témoignages (placeholder)
- Distinctions / Sélections (placeholder)
- Contact (formulaire + liens sociaux)
- Mentions légales / droits

## Intégration automatique des vidéos YouTube
La page peut interroger l'API YouTube Data v3 côté client (recherche publique) pour récupérer toutes les vidéos mentionnant « Ludovic Gacquer » dans le titre ou la description (avec variantes : acteur, réalisateur, monteur, interview, bande annonce).

### Obtenir une clé API YouTube
1. Rendez-vous sur https://console.cloud.google.com/
2. Créez un projet ou réutilisez un existant.
3. Activez l'API « YouTube Data API v3 ».
4. Créez une clé API (API Key) et restreignez-la (HTTP referrers : votre domaine de production).
5. Copiez cette clé.

### Injection de la clé (méthode simple pour test local)
Ouvrez `index.html` et remplacez la valeur vide de `const YOUTUBE_API_KEY = ''` par votre clé (ne pas versionner une clé sensible sur un dépôt public). Pour production, utilisez un *build step* qui injecte la clé depuis une variable d'environnement ou un proxy serveur.

### Cache local
Les résultats sont mis en cache dans `localStorage` (clé: `lg_videos_cache`) avec une durée configurable (par défaut 6h) pour réduire le quota API.

### Limites & Sécurité
- La clé API exposée côté client peut être abusée si non restreinte : RESTREIGNEZ les referrers.
- L’API YouTube impose des quotas (coût d’une requête search.list : 100 unités). La configuration réduit les appels.
- Pour une robustesse accrue, on peut ultérieurement ajouter un micro-service (Node / Cloudflare Worker) qui agrège et nettoie les résultats.

## Liste manuelle de secours
Dans le script inline, un tableau `manualVideos` peut être renseigné (IDs YouTube) si vous ne souhaitez pas utiliser l'API ou en cas de quota dépassé.

## Personnalisation rapide
Cherchez les marqueurs `TODO:` dans `index.html` pour modifier :
- Biographie
- Compétences / pourcentages
- Filmographie (données JSON embarquées)
- Témoignages & Distinctions
- Liens sociaux / contact

## Déploiement statique
Vous pouvez héberger simplement :
- GitHub Pages
- Netlify / Vercel (drag & drop)
- Hébergement mutualisé (upload du fichier)

## Ouvrir localement (Windows PowerShell)
```pwsh
Start-Process .\index.html
```

## Améliorations futures suggérées
- Génération statique préalable des vidéos (script Node) pour SEO complet.
- Micro-schema JSON-LD pour chaque crédit de film.
- Intégration Vimeo / Allociné / IMDb via scraping ou API (où licence autorisée).
- Internationalisation (fr / en) via attribut `data-i18n`.

## Licence
Contenu (textes, médias) © Ludovic Gacquer. Code front-end sous licence MIT (adapter si nécessaire).

---
Voir `index.html` pour l’implémentation complète.
