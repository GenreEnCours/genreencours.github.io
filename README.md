# Code source des pages du projet Genre en Cours

Ce dépôt contient le **contenu** et la **customisation** du site. Au moment du
build, `build_site.sh` clone le dépôt de code, puis surcharge certains fichiers à
partir de `scripts/resources/` (voir `scripts/resources/to_replace`). La plupart
des réglages se font donc dans `scripts/resources/siteConfig.json`, sans toucher
au code.

## Ajouter un nouveau partenariat

Les partenariats sont définis dans `scripts/resources/siteConfig.json`, sous la
clé `partnerships`. Chaque entrée associe un **tag d'article** à un logo et un
lien. Le logo s'affiche en bas des articles portant ce tag.

1. Déposer l'image du logo dans `scripts/resources/LogosPartenariats/`.
2. Ajouter une entrée dans `partnerships` :

   ```json
   "partnerships": {
     "partenariat MNHN": {
       "name": "MNHN",
       "logo": "MNHN-logo.jpg",
       "url": "https://www.mnhn.fr/fr"
     }
   }
   ```

   - la **clé** (`"partenariat MNHN"`) doit correspondre exactement au tag utilisé
     dans les articles ;
   - `logo` est le **nom du fichier** déposé à l'étape 1 ;
   - `name` sert de texte alternatif, `url` est le lien cliquable.

3. Dans le frontmatter des articles concernés, ajouter ce tag dans `tags`.

Au build, les logos de `LogosPartenariats/` sont copiés dans `static/` du site et
servis automatiquement. Aucune modification de code n'est nécessaire.

## Modifier le texte défilant de la page d'accueil

Le grand titre de la page d'accueil se configure dans
`scripts/resources/siteConfig.json`, sous la clé `home` :

```json
"home": {
  "heading": "Outils et ressources pour",
  "rotatingWords": [
    "apprendre",
    "bricoler ensemble",
    "se former",
    "s'informer",
    "transformer nos pratiques"
  ],
  "additional": "du collège à l'université"
}
```

- `heading` : le début du titre, fixe.
- `rotatingWords` : la liste des mots qui défilent l'un après l'autre. Le premier
  mot est celui affiché au chargement. Ajouter / retirer / réordonner librement.
- `additional` *(optionnel)* : texte complémentaire affiché en italique et centré
  sous le mot défilant. S'il est défini, des points de suspension (`...`) sont
  ajoutés automatiquement à la fin du mot défilant et au début de ce texte.
  Laisser une chaîne vide (`""`) ou retirer la clé pour ne rien afficher.
