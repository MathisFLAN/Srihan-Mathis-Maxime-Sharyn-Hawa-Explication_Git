# 4. Bonnes pratiques

## 4.1 Faire des commits cohérents

Un commit devrait représenter une unité logique.

Éviter :

```text
commit: modifications diverses
```

Préférer :

```text
feat: add OAuth callback
test: cover OAuth callback errors
docs: document OAuth configuration
```

La convention exacte (`feat`, `fix`, etc.) doit être définie par l'équipe si elle est utilisée.

## 4.2 Éviter les commits inutiles

Exemples de commits qui peuvent être nettoyés avant une PR :

```text
fix
fix 2
fix again
oops
final
final-final
```

Si le workflow le permet, l'historique peut être nettoyé avant le merge.

Mais il ne faut pas réécrire l'historique d'une branche partagée sans comprendre les conséquences.

## 4.3 Garder les PR petites

Si une fonctionnalité est importante, la découper lorsque cela est possible.

Exemple :

```text
PR 1 → Ajouter le modèle de données
PR 2 → Ajouter l'API
PR 3 → Ajouter l'interface
PR 4 → Activer la fonctionnalité
```

Le découpage doit rester logique et ne pas rendre les changements artificiellement compliqués.

## 4.4 Ne pas mélanger refactoring et fonctionnalité

Éviter :

```text
PR :
- nouvelle fonctionnalité
- renommage de 150 fichiers
- changement de formatter
- refactoring complet
```

Préférer des PR séparées lorsque cela est raisonnable.

Cela facilite la review et réduit les conflits.

## 4.5 Automatiser ce qui peut l'être

La CI peut vérifier automatiquement :

- formatting ;
- lint ;
- tests ;
- compilation ;
- couverture ;
- sécurité ;
- conventions de commits.

Plus une règle est mécanique, moins elle devrait dépendre de l'attention du reviewer.

## 4.6 Protéger les branches importantes

Pour une branche comme `main`, une équipe peut imposer :

- PR obligatoire ;
- CI obligatoire ;
- approvals obligatoires ;
- branche à jour avant merge ;
- interdiction du push direct ;
- restrictions sur le force push.

Les règles exactes doivent être adaptées au niveau de risque du projet.

## 4.7 Éviter les PR « surprises »

Prévenir l'équipe lorsqu'une PR :

- est exceptionnellement grande ;
- touche une partie critique ;
- modifie une API publique ;
- change une migration de base de données ;
- nécessite une coordination de déploiement.

Un message en amont peut éviter plusieurs heures de review inutile.

## 4.8 Respecter le temps des reviewers

Une PR est une demande de temps adressée à d'autres personnes.

Pour faciliter la review :

- expliquer le contexte ;
- garder le diff raisonnable ;
- signaler les points complexes ;
- fournir les résultats des tests ;
- éviter les changements sans rapport.

## 4.9 Ne pas utiliser la review comme unique contrôle qualité

Une PR ne remplace pas :

- les tests ;
- la CI ;
- les outils de sécurité ;
- les tests d'intégration ;
- les procédures de déploiement ;
- la supervision.

La review est une couche supplémentaire de confiance.
