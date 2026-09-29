# 3. Faire une revue de code

## 3.1 Le but d'une review

Une code review cherche principalement à augmenter la confiance dans le changement.

On peut notamment vérifier :

1. Le comportement attendu est-il respecté ?
2. La solution est-elle cohérente avec l'architecture existante ?
3. Y a-t-il un risque de régression ?
4. Les erreurs et cas limites sont-ils traités ?
5. Les tests sont-ils suffisants ?
6. Le code reste-t-il compréhensible et maintenable ?

## 3.2 Lire la PR dans le bon ordre

Une approche efficace :

### 1. Lire le titre et la description

Comprendre le problème avant de regarder chaque ligne.

### 2. Regarder le diff global

Identifier :

- les fichiers concernés ;
- la taille du changement ;
- les zones sensibles.

### 3. Comprendre les changements principaux

Ne pas commencer uniquement par traquer les détails de style.

### 4. Examiner les tests

Les tests permettent souvent de comprendre le comportement attendu.

### 5. Examiner les cas limites

Penser notamment à :

- valeurs nulles ;
- erreurs réseau ;
- permissions ;
- concurrence ;
- données invalides ;
- compatibilité ;
- performances ;
- sécurité.

## 3.3 Comment écrire un commentaire

Un bon commentaire est :

- précis ;
- contextualisé ;
- respectueux ;
- actionnable lorsque nécessaire.

Préférer :

> Est-ce qu'on peut gérer ici le cas où `response` est `null` ? L'API peut retourner ce cas lorsqu'une ressource a été supprimée entre les deux appels.

À éviter :

> Ça ne va pas.

## 3.4 Question ou demande de modification ?

Faire la différence entre :

**Question :**

> Pourquoi utilise-t-on un cache ici plutôt qu'une lecture directe ?

**Suggestion :**

> On pourrait extraire cette logique dans `PaymentService` pour éviter de dupliquer le comportement.

**Bloquant :**

> Ce changement permet à un utilisateur non authentifié d'accéder à cette route. Il faudrait corriger ce point avant le merge.

Les conventions de l'outil peuvent permettre de marquer explicitement un commentaire comme bloquant.

## 3.5 Ne pas transformer la review en débat de style

Si le projet possède un formatter ou un linter, automatiser les règles de style.

La review doit surtout se concentrer sur :

- comportement ;
- conception ;
- sécurité ;
- performance ;
- maintenabilité ;
- cohérence.

## 3.6 Review et ownership

Il est utile de savoir qui est responsable des différentes parties du code.

Mais le reviewer n'a pas besoin d'être la personne qui a initialement écrit le code.

L'objectif est de partager la connaissance du code plutôt que de créer des zones détenues exclusivement par une personne.

## 3.7 Quand approuver ?

Approuver signifie que l'on estime que le changement peut être intégré selon les règles de l'équipe.

Avant d'approuver, vérifier au minimum :

- le comportement ;
- les risques importants ;
- les tests ;
- les points de sécurité pertinents ;
- les commentaires laissés précédemment.

Une review n'est pas nécessairement une garantie que le code est parfait.

## 3.8 Après les corrections

L'auteur peut répondre aux commentaires et pousser de nouveaux commits.

Le reviewer doit ensuite vérifier les modifications demandées.

Éviter de considérer automatiquement :

> « J'ai répondu au commentaire »

comme :

> « Le problème est résolu ».

Il faut vérifier le changement dans le code.
