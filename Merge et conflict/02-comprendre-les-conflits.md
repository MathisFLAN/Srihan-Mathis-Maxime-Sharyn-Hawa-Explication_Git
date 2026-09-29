# 2. Comprendre les conflits

## 2.1 Qu'est-ce qu'un conflit ?

Git sait généralement fusionner automatiquement deux branches lorsque les modifications concernent des parties différentes du code.

Un conflit apparaît lorsque Git ne peut pas déterminer automatiquement quel résultat produire.

Exemple :

```text
main :
<h1>Bienvenue sur le site</h1>

feature/page-accueil :
<h1>Bienvenue sur notre projet</h1>
```

Les deux branches ont modifié la même zone.

Git ne peut pas décider quelle version doit être conservée.

## 2.2 Pourquoi Git ne choisit-il pas ?

Git ne connaît pas l'intention du développeur.

Il peut savoir que deux lignes sont différentes, mais pas nécessairement si :

- une ligne doit remplacer l'autre ;
- les deux changements doivent être conservés ;
- les deux changements doivent être combinés ;
- l'une des modifications est devenue obsolète.

La résolution d'un conflit est donc une **décision fonctionnelle et technique**, pas seulement une opération Git.

## 2.3 À quoi ressemble un conflit ?

Git peut ajouter des marqueurs dans le fichier :

```text
<<<<<<< HEAD
<h1>Bienvenue sur notre site</h1>
=======
<h1>Bienvenue sur le projet Git</h1>
>>>>>>> main
```

Dans cet exemple :

- `<<<<<<< HEAD` marque le début de la première version ;
- `=======` sépare les deux versions ;
- `>>>>>>> main` marque la fin de la seconde version.

Dans un merge, `HEAD` représente la branche actuellement checkoutée, c'est-à-dire la branche dans laquelle on réalise le merge.

## 2.4 Le résultat final

Il faut modifier le fichier pour obtenir le comportement souhaité.

Par exemple :

```html
<h1>Bienvenue sur notre projet Git</h1>
```

Ou, si les deux informations sont pertinentes :

```html
<h1>Bienvenue sur notre site, le projet Git</h1>
```

Le résultat dépend du besoin fonctionnel.

## 2.5 Les marqueurs doivent disparaître

Après résolution, le fichier ne doit plus contenir :

```text
<<<<<<<
=======
>>>>>>>
```

Il faut également vérifier qu'aucune modification voulue n'a été supprimée accidentellement.

## 2.6 Une Pull Request avec conflit

Lorsqu'une PR présente un conflit avec sa branche cible, elle doit être remise dans un état cohérent avant son intégration.

Une manière courante de procéder est de mettre à jour sa branche avec les dernières modifications de `main`, puis de résoudre les conflits localement.

Le workflow peut être résumé ainsi :

```text
main évolue
   ↓
la branche feature devient en retard
   ↓
merge/rebase de main dans la branche
   ↓
conflit éventuel
   ↓
résolution
   ↓
tests
   ↓
push
   ↓
PR mise à jour
```
