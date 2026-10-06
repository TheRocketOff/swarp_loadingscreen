# Vidéos d'arrière-plan (`videos/`)

Placez ici un fichier `.webm` par carte référencée dans `MAP_DATA` (`index.html`), plus
**`default.webm`** (obligatoire - utilisé pour toute carte absente de la table, ou si la vidéo
d'une carte échoue à charger).

Fichiers attendus pour la configuration fournie par défaut :

```
videos/
├── default.webm      (obligatoire)
├── coruscant.webm
├── kamino.webm
└── tatooine.webm
```

## Recommandations techniques

- **Format** : WebM (codec vidéo VP9 conseillé, pas de piste audio nécessaire - la vidéo est
  `muted` dans `index.html` ; utilisez plutôt `audio/` si vous voulez une ambiance sonore).
- **Résolution** : 1920×1080 suffit (`object-fit: cover` adapte à n'importe quel écran).
- **Durée** : 10-20 secondes en boucle (`loop`) suffisent largement ; une boucle plus longue
  alourdit juste le téléchargement initial de la page.
- **Poids** : visez moins de 5-8 Mo par vidéo - cette page se charge PENDANT la connexion au
  serveur, un fichier trop lourd retarde l'affichage du secteur plutôt que de l'accélérer.
- Convertir un MP4 en WebM (ffmpeg) :

```
ffmpeg -i source.mp4 -c:v libvpx-vp9 -b:v 2M -crf 32 -an videos/coruscant.webm
```

## Ajouter une nouvelle carte

1. Déposez le fichier ici (ex : `videos/kashyyyk.webm`).
2. Ajoutez une entrée dans `MAP_DATA` (`index.html`) avec le nom EXACT de la carte GMod
   (`rp_kashyyyk_v1`, sensible à la casse) :

```js
"rp_kashyyyk_v1": {
    video: "videos/kashyyyk.webm",
    title: "Atterrissage sur Kashyyyk",
    desc: "Monde forestier - Patrie des Wookiees",
    audio: null
}
```

Aucune vidéo n'est fournie avec ce dossier (fichiers binaires) : ajoutez les vôtres.
