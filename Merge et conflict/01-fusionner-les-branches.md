# 1. Comment fusionner notre travail

## 1.1 Le principe

Chaque membre de l'équipe travaille sur une branche dédiée à sa tâche.

Par exemple :

```text
main
 ├── feature/page-accueil
 ├── feature/page-contact
 └── fix/menu-mobile
```

L'objectif est d'éviter que plusieurs personnes travaillent directement sur `main`.

## 1.2 Créer sa branche

Depuis une branche à jour :

```bash
git switch main
git pull --ff-only
git switch -c feature/page-accueil
```

La commande :

```bash
git switch -c feature/page-accueil
```

crée la branche et bascule immédiatement dessus.

## 1.3 Développer et créer un commit

On modifie les fichiers puis on vérifie les changements :

```bash
git status
git diff
```

On enregistre ensuite le travail :

```bash
git add .
git commit -m "feat: add home page"
```

Il est recommandé d'utiliser une convention de messages de commit définie par l'équipe.

## 1.4 Envoyer la branche sur GitHub

```bash
git push -u origin feature/page-accueil
```

L'option `-u` configure la branche distante comme branche de suivi. Les prochains `git push` peuvent ensuite être exécutés simplement avec :

```bash
git push
```

## 1.5 Créer une Pull Request

Sur GitHub, créer une Pull Request :

```text
feature/page-accueil → main
```

La PR permet notamment :

- de présenter les changements ;
- de faire relire le code ;
- d'exécuter les tests automatiques ;
- de discuter des modifications ;
- de vérifier les éventuels conflits.

## 1.6 Faire relire la branche

Un autre membre de l'équipe vérifie :

- le code ;
- les tests ;
- le comportement attendu ;
- les éventuels effets de bord.

Si des modifications sont demandées, elles sont faites sur la même branche :

```bash
git add .
git commit -m "fix: update home page review"
git push
```

La Pull Request est automatiquement mise à jour.

## 1.7 Fusionner la Pull Request

Lorsque les conditions définies par l'équipe sont remplies, la PR peut être fusionnée.

Selon la configuration du dépôt, GitHub peut proposer plusieurs stratégies :

- Merge commit ;
- Squash and merge ;
- Rebase and merge.

Le choix doit suivre la convention du projet.

> Une Pull Request est généralement le lieu où l'équipe décide d'intégrer une branche dans `main`. Les commandes `git merge` expliquées dans cette documentation servent notamment à mettre une branche à jour ou à réaliser une fusion directement avec Git.
