# Les branches avec git

Une branche Git sert à travailler sur une version différente d'un projet sans modifier la branche principale.

La branche principale est appelée main. On créer une nouvelle branche pour développer une fonctionnalité, corriger un bug ou faire des tests.

## Quelques commandes utiles

``` md
# Créer une branche
git branch ma-branche

# Se déplacer sur une branche
git switch ma-branche / git checkout ma-branche

# Créer et se déplacer directement sur une branche
git switch -c ma-branche

# Voir les branches existantes
git branch

# Fusionner une branche avec la branche actuelle
git merge ma-branche

# Supprimer une branche
git branch -d ma-branche
```

## Exemple

On part de main, on créer une branche develop avec des features et une branche bug fix :

```
main
 │
 ├── develop
 │      ├── feature-1
 │      └── feature-2
 │
 └── bug-fix
```

Une fois la fonctionnalité terminée et testée, on peut fusionner (merge) la branche develop dans main.

On peut donc travailler à plusieurs et de développer différentes fonctionnalités en parallèle, tout en gardant une branche principale stable.

## Chez nous

Dans notre entreprise, seul le chef du projet est autorisé a toucher a la branche main.

Les développeurs doivent créet une branche a partir de develop nommé : 
feature-nom_de_l'ajout (ex : feature-disconnect_button)