# Ambiances sonores (`audio/`) - optionnel

Dossier optionnel pour une musique/ambiance Star Wars jouée pendant l'écran de chargement, en plus
de la vidéo (qui reste `muted`). Non utilisé si vous laissez `audio: null` dans `MAP_DATA`
(`index.html`) - c'est le cas par défaut, aucun fichier n'est fourni ici.

## Utilisation

1. Déposez un fichier `.mp3` ou `.ogg` ici (ex : `audio/coruscant.mp3`).
2. Renseignez son chemin dans l'entrée correspondante de `MAP_DATA` :

```js
"rp_coruscant_v1": {
    video: "videos/coruscant.webm",
    title: "Arrivée dans le secteur de Coruscant",
    desc: "Capitale de la République",
    audio: "audio/coruscant.mp3"
}
```

## À savoir

- La plupart des navigateurs/WebView bloquent l'autoplay AVEC son si l'utilisateur n'a jamais
  interagi avec la page - `index.html` tente `audio.play()` et ignore silencieusement un refus
  (`.catch(() => {})`), donc rien ne plante si le son ne démarre pas automatiquement : attendez-vous
  à ce qu'il soit silencieux pour certains joueurs selon leur navigateur interne GMod.
- Gardez les fichiers courts et légers (même remarque que pour les vidéos, voir `videos/README.md`) :
  cette page se charge pendant la connexion, pas après.
- Volume fixé à 35% dans `index.html` (`audio.volume = 0.35`) - ajustez cette valeur si besoin.
