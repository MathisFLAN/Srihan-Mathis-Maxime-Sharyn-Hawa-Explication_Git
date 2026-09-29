# 1. Les principes des Pull Requests

## 1.1 Qu'est-ce qu'une Pull Request ?

Une Pull Request est une proposition d'intégration d'une série de changements dans une branche cible.

Exemple :

```text
main
  │
  ├── feature/ajout-auth
  │       ├── commit A
  │       ├── commit B
  │       └── commit C
  │
  └── PR → main
```

La PR crée un espace où l'équipe peut :

- voir les différences ;
- discuter du code ;
- demander des modifications ;
- exécuter des checks automatiques ;
- garder une trace de la décision ;
- finalement intégrer le changement.

## 1.2 Une PR n'est pas uniquement une validation

Une mauvaise utilisation consiste à considérer la PR comme une simple étape administrative :

> « J'ai fini, quelqu'un doit cliquer sur Approve. »

Une bonne PR sert plutôt à **faciliter la collaboration**.

Le reviewer doit pouvoir comprendre :

- le problème traité ;
- la solution choisie ;
- les impacts ;
- les points nécessitant une attention particulière ;
- la manière dont le changement a été testé.

## 1.3 Une PR = un objectif

Privilégier :

```text
PR #1 : Ajouter l'authentification OAuth
PR #2 : Corriger le calcul de TVA
PR #3 : Refactorer le client HTTP
```

Éviter :

```text
PR #1 : Auth + refacto HTTP + nouveau système de logs
```

Une PR trop large devient difficile à relire et augmente le risque de laisser passer un problème.

## 1.4 Taille d'une PR

Il n'existe pas de nombre universel de lignes à respecter.

Une PR de 300 lignes peut être très facile à relire si elle est cohérente. Une PR de 80 lignes peut être difficile si elle mélange plusieurs sujets.

Chercher surtout à avoir :

- un périmètre clair ;
- peu de changements non liés ;
- une intention identifiable ;
- des tests adaptés.

## 1.5 PR et branches protégées

Dans une équipe, il est généralement préférable d'empêcher les modifications directes sur les branches importantes comme `main`.

Exemple de règle :

```text
main
 ├── push direct interdit
 ├── PR obligatoire
 ├── CI obligatoire
 └── 1 ou plusieurs approvals
```

Les règles exactes dépendent de la plateforme et de la politique de l'entreprise.

## 1.6 Le rôle de la CI

Une PR peut déclencher automatiquement :

- tests unitaires ;
- tests d'intégration ;
- lint ;
- analyse statique ;
- build ;
- tests de sécurité ;
- génération d'artefacts.

L'objectif est de détecter automatiquement les problèmes répétables avant le merge.

## 1.7 Responsabilité collective

La PR n'est pas seulement la responsabilité de l'auteur.

**Auteur :**

- expliquer le changement ;
- tester ;
- répondre aux commentaires ;
- maintenir la PR dans un état mergeable.

**Reviewer :**

- comprendre l'intention ;
- vérifier la conception et le comportement ;
- identifier les risques ;
- poser des questions utiles ;
- valider lorsque le niveau de confiance est suffisant.

**Équipe :**

- définir des règles communes ;
- automatiser les vérifications ;
- éviter que la review devienne un goulot d'étranglement.
