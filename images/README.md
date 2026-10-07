# Images d'arrière-plan (`images/`)

Placez ici un fichier image par carte référencée dans `MAP_DATA` (`index.html`), plus
**`default.jpg`** (obligatoire - utilisé pour toute carte absente de la table, ou si l'image
d'une carte échoue à charger).

Fichiers attendus pour la configuration fournie par défaut :

```
images/
├── default.jpg      (obligatoire)
├── coruscant.jpg
├── kamino.jpg
└── tatooine.jpg
```

## Recommandations techniques

- **Format** : JPG ou WebP conseillés (compression avec perte, poids réduit pour une simple image
  de fond) ; PNG possible mais plus lourd sans réel bénéfice ici.
- **Résolution** : 1920×1080 suffit (`background-size: cover` dans `index.html` adapte à n'importe
  quel écran, en recadrant si besoin).
- **Poids** : visez moins de 300-500 Ko par image - cette page se charge PENDANT la connexion au
  serveur, un fichier trop lourd retarde l'affichage du secteur plutôt que de l'accélérer.
- L'extension n'a pas besoin de correspondre exactement à ce qui est écrit dans `MAP_DATA` : seul
  le chemin complet compte (`images/coruscant.webp` fonctionne aussi bien que `.jpg`, tant que le
  champ `image` de l'entrée correspondante dans `index.html` pointe vers le bon fichier).

## Ajouter une nouvelle carte

1. Déposez le fichier ici (ex : `images/kashyyyk.jpg`).
2. Ajoutez une entrée dans `MAP_DATA` (`index.html`) avec le nom EXACT de la carte GMod
   (`rp_kashyyyk_v1`, sensible à la casse) :

```js
"rp_kashyyyk_v1": {
    image: "images/kashyyyk.jpg",
    title: "Atterrissage sur Kashyyyk",
    desc: "Monde forestier - Patrie des Wookiees",
    audio: null
}
```

Aucune image n'est fournie avec ce dossier (fichiers binaires) : ajoutez les vôtres.
