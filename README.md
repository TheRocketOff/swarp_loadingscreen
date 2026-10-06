# Écran de chargement web (`sv_loadingurl`)

Page HTML chargée par le CLIENT pendant qu'il se connecte au serveur (avant même que le personnage
ne soit sélectionné) - totalement indépendante du reste du schéma SWARP (c'est une page web
statique, pas du code Lua). Deux versions sont disponibles dans ce dossier :

- **`index.html`** (recommandée) : vidéo d'arrière-plan qui change selon la carte chargée, overlay
  HUD Star Wars, barre de progression de téléchargement. C'est celle-ci que la configuration
  ci-dessous utilise.
- **`loading.html`** (ancienne version) : fond étoilé animé en Canvas, sans vidéo - conservée au
  cas où vous préférez une version plus légère/sans fichiers vidéo à héberger. Remplacez simplement
  `index.html` par `loading.html` dans l'URL ci-dessous pour l'utiliser à la place.

## 1. Héberger les fichiers

Hébergez **tout ce dossier** (`index.html`, `videos/`, `audio/`) sur un serveur web, HTTPS conseillé
(GitHub Pages, Netlify, votre hébergeur...). Ajoutez vos propres vidéos dans `videos/` avant de
mettre en ligne - voir `videos/README.md` (aucune vidéo n'est fournie, ce sont des fichiers
binaires que vous devez déposer vous-même).

## 2. `server.cfg`

GMod remplace automatiquement `%m` par le nom de la carte en cours et `%s` par le SteamID du joueur
dans la valeur de `sv_loadingurl` (voir [wiki.facepunch.com/gmod/Loading_URL](https://wiki.facepunch.com/gmod/Loading_URL)) -
c'est ce qui permet à `index.html` de savoir quelle vidéo afficher dès son chargement, via
`?mapname=%m` :

```
sv_loadingurl "https://votre-domaine.tld/swarp/index.html?mapname=%m"
```

Variante avec le SteamID en plus (non utilisé par `index.html` actuellement, mais disponible si
vous voulez l'exploiter plus tard - ex : afficher le pseudo Steam) :

```
sv_loadingurl "https://votre-domaine.tld/swarp/index.html?mapname=%m&steamid=%s"
```

**Filet de sécurité** : même sans `%m` dans l'URL (oubli, ou si vous gardez une URL fixe),
`index.html` reçoit quand même le nom de la carte via `GameDetails(...)`, une fonction que GMod
appelle directement une fois connecté (mécanisme standard de l'écran de chargement, indépendant de
l'URL) - la vidéo par défaut (`videos/default.webm`) s'affiche simplement un peu plus longtemps
avant de basculer sur la bonne.

## 3. Redémarrer

Redémarrez le serveur, ou tapez `sv_loadingurl "..."` en console puis reconnectez-vous pour tester.

## Personnalisation

- **Table des cartes** (`MAP_DATA` en haut du `<script>` d'`index.html`) : associez chaque carte
  GMod (nom EXACT, sensible à la casse - ex : `rp_coruscant_v1`) à une vidéo, un titre et une
  description. Toute carte absente retombe sur `DEFAULT_ENTRY` (`videos/default.webm`).
- **Couleur d'accent** : variable CSS `--accent` en haut d'`index.html`.
- **Nom/sous-titre du serveur** : `#server-name` / `#server-sub` (également écrasés en direct par
  `GameDetails` si `servername` est fourni par GMod).
- **Ambiance sonore par carte** (optionnel) : voir `audio/README.md`.

## Test en local

Ouvrez `index.html` directement dans un navigateur ; pour simuler une carte précise, ouvrez-le avec
`?mapname=rp_coruscant_v1` dans l'URL. Pour simuler la progression du téléchargement, tapez dans la
console du navigateur :

```js
SetFilesTotal(100); SetFilesNeeded(40); DownloadingFile("models/test.mdl");
```
