# 2. Créer une Pull Request

## 2.1 Avant de créer la PR

Vérifier localement :

```bash
git status
git diff
git log --oneline
```

Puis exécuter les tests et outils du projet.

Exemple :

```bash
npm test
npm run lint
```

ou :

```bash
pytest
```

Les commandes dépendent évidemment du projet.

## 2.2 Mettre sa branche à jour

Avant d'ouvrir ou de finaliser une PR, vérifier si la branche cible a évolué.

Exemple avec merge :

```bash
git fetch origin
git merge origin/main
```

Ou avec rebase, si c'est la convention de l'équipe :

```bash
git fetch origin
git rebase origin/main
```

Il faut suivre la convention du projet plutôt que choisir individuellement une stratégie.

## 2.3 Pousser la branche

```bash
git push -u origin feature/ma-feature
```

Les noms de branches doivent suivre une convention d'équipe.

Exemples :

```text
feature/add-login
fix/payment-timeout
refactor/http-client
chore/update-dependencies
```

## 2.4 Le titre

Un bon titre est court et décrit l'intention.

Mauvais :

```text
Fix
```

```text
Changes
```

```text
Update code
```

Meilleur :

```text
Add OAuth login
```

```text
Handle payment timeout
```

Si l'équipe utilise des conventions de tickets :

```text
[PAY-142] Handle payment timeout
```

## 2.5 La description

Une description utile peut suivre ce modèle :

```markdown
## Contexte

Pourquoi ce changement est-il nécessaire ?

## Changements

- Ajout de ...
- Modification de ...
- Suppression de ...

## Tests

- [x] Tests unitaires
- [x] Tests d'intégration
- [ ] Tests manuels

## Points d'attention

Le nouveau cache peut modifier le comportement de ...

## Ticket

PAY-142
```

L'objectif n'est pas de remplir un formulaire artificiellement : il faut donner au reviewer les informations qu'il ne peut pas déduire du diff.

## 2.6 Draft PR

Utiliser une Draft PR lorsque le travail est encore en cours mais qu'un retour anticipé est utile.

Exemples :

- demander un avis sur une architecture ;
- vérifier une approche ;
- partager un travail en cours ;
- détecter tôt un problème de conception.

Une Draft PR ne doit pas être utilisée simplement pour contourner l'attente d'avoir un changement suffisamment présentable.

## 2.7 Choisir les reviewers

Choisir des personnes pertinentes pour le changement.

Exemples :

- propriétaire du composant ;
- personne connaissant le domaine ;
- mainteneur d'une librairie interne ;
- personne responsable de la sécurité pour un changement sensible.

Éviter de sélectionner un grand nombre de reviewers uniquement pour « être couvert ».

## 2.8 Une PR prête à être reviewée

Avant de demander une review :

- le titre est explicite ;
- la description explique le contexte ;
- les changements inutiles ont été retirés ;
- les tests pertinents passent ;
- les checks CI sont en cours ou terminés ;
- les conflits éventuels sont traités ;
- la branche cible est correcte ;
- les reviewers pertinents sont sélectionnés.
