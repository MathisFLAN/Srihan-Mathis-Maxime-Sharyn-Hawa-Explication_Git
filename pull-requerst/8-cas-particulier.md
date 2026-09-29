# 8. Cas particuliers

## 8.1 PR trop grosse

Signes :

- plusieurs centaines de fichiers ;
- plusieurs fonctionnalités ;
- changements de comportement + refactoring massif ;
- review très difficile.

Actions possibles :

- découper la PR ;
- séparer le refactoring ;
- utiliser une feature flag ;
- faire plusieurs PR dépendantes.

## 8.2 PR dépendante d'une autre

Exemple :

```text
PR #101 → ajoute l'API
PR #102 → utilise l'API
```

Si #102 dépend de #101, il faut le documenter explicitement.

On peut aussi utiliser des branches empilées selon les outils et conventions de l'équipe.

## 8.3 Hotfix

Pour une correction urgente :

```text
main
  │
  └── hotfix/payment-crash
             │
             └── PR → main
```

Même en urgence, conserver autant que possible :

- une review ;
- des tests ;
- une trace dans la PR ;
- les contrôles de sécurité nécessaires.

Les règles d'urgence doivent être définies à l'avance.

## 8.4 PR abandonnée

Une PR peut devenir obsolète.

Exemples :

- fonctionnalité abandonnée ;
- ticket annulé ;
- autre PR ayant déjà résolu le problème ;
- approche devenue incorrecte.

La fermer avec une explication est préférable à la laisser ouverte sans contexte.

## 8.5 PR après un gros changement de `main`

Si beaucoup de changements ont été intégrés depuis la création de la branche :

1. récupérer `main` ;
2. mettre à jour la branche selon le workflow de l'équipe ;
3. résoudre les conflits ;
4. lancer les tests ;
5. vérifier à nouveau le diff.

## 8.6 Modification d'une base de données

Les PR contenant des migrations demandent une attention particulière.

Vérifier :

- compatibilité avec la version précédente ;
- ordre de déploiement ;
- rollback éventuel ;
- données existantes ;
- durée de migration ;
- verrouillage éventuel ;
- compatibilité entre ancienne et nouvelle version de l'application.

## 8.7 Sécurité

Pour un changement sensible :

- authentification ;
- autorisation ;
- secrets ;
- paiements ;
- données personnelles ;
- permissions ;

prévoir les reviewers et contrôles adaptés.

Ne jamais mettre de secrets dans une PR ou dans Git.

Si un secret a été accidentellement commité, le supprimer du fichier ne suffit pas nécessairement : il faut considérer le secret comme compromis et suivre la procédure de rotation de l'entreprise.

## 8.8 PR uniquement pour changer du formatting

Éviter autant que possible de mélanger un changement de formatting massif avec une fonctionnalité.

Un changement global de formatting peut rendre les futurs diffs beaucoup plus difficiles à analyser.

## 8.9 PR urgente sans review complète

Une procédure d'urgence peut exister, mais elle doit être explicite.

Par exemple :

```text
incident
  ↓
hotfix
  ↓
check automatique
  ↓
review disponible
  ↓
déploiement
  ↓
review complémentaire / post-mortem
```

Le processus exact dépend du niveau de criticité du système.
