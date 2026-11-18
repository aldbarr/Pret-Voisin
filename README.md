# Prêt’Voisin — maquette PWA (V8)

Plateforme locale de prêt et de dons gratuits entre voisins. **Maquette frontend uniquement** : pas de backend, pas d’authentification, aucune donnée envoyée à un serveur. Les annonces et messages créés disparaissent au rechargement.

## Structure

```
index.html            page unique de l’application
styles.css            styles
app.js                logique (données de démo, rendu, FR/EN)
sw.js                 Service Worker (cache hors connexion)
manifest.webmanifest  manifeste PWA
icons/                icônes 192 et 512 px
netlify.toml          configuration Netlify (en-têtes, cache)
```

## Tester en local

Le Service Worker ne fonctionne pas en ouvrant `index.html` par double-clic.

```bash
python3 -m http.server 8080
# puis http://localhost:8080
```

## Mettre sur GitHub

```bash
git init
git add .
git commit -m "Prêt'Voisin V8 — maquette PWA"
git branch -M main
git remote add origin https://github.com/<votre-compte>/pret-voisin.git
git push -u origin main
```

Sans terminal : créez un dépôt vide sur github.com, puis **Add file → Upload files** et glissez tout le contenu du dossier (y compris `icons/` et `netlify.toml`).

## Déployer sur Netlify

1. app.netlify.com → **Add new site → Import an existing project → GitHub**.
2. Choisissez le dépôt `pret-voisin`.
3. Build command : *(vide)* — Publish directory : `.`  (déjà défini dans `netlify.toml`).
4. **Deploy**. Chaque `git push` sur `main` redéploie automatiquement.
5. Optionnel : *Site configuration → Change site name* pour une URL du type `pret-voisin.netlify.app`.

### À chaque mise à jour

Incrémentez `VERSION` dans `sw.js` (ex. `v8` → `v9`) pour que les téléphones ayant installé l’app récupèrent bien les nouveaux fichiers.

### Installer sur mobile

- **iPhone / iPad** : Safari → Partager → *Sur l’écran d’accueil*.
- **Android** : Chrome → menu ⋮ → *Installer l’application*.

## Confidentialité de la maquette

Le site est marqué `noindex` (non référencé par Google). Il reste toutefois public pour qui a le lien. Pour restreindre l’accès : Netlify *Site configuration → Access control → Password protection* (offre payante) ou ne partager l’URL qu’aux testeurs.

## Vers le vrai MVP

Frontend PWA (React/Next.js) · API Node.js/NestJS · PostgreSQL · stockage photos S3 hébergé en Suisse · auth e-mail + téléphone · WebSocket pour la messagerie · back-office de modération · hébergement suisse (Infomaniak, Exoscale) avec staging + production.

Données : nLPD (registre des traitements, politique de confidentialité, durées de conservation, export/suppression, sous-traitants, art. 16 LPD en cas de transfert à l’étranger). Garder la logique métier côté backend pour réutiliser la même API dans de futures apps iOS/Android.

La charte de prêt (`app.js`, `charterSections`) est un projet à faire valider par un juriste suisse.
