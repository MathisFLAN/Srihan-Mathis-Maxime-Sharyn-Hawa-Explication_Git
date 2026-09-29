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
