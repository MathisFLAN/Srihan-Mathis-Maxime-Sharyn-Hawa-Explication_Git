# 7. Stratégies de merge

Les plateformes proposent généralement plusieurs façons d'intégrer une PR.

## 7.1 Merge commit

```text
A---B---C------M
     \        /
      D---E---
```

Un commit de merge relie les deux historiques.

### Avantages

- conserve explicitement la structure des branches ;
- ne nécessite pas de réécrire l'historique de la branche.

### Inconvénients

- peut rendre l'historique plus difficile à lire avec beaucoup de petites branches.

## 7.2 Squash merge

Plusieurs commits de la PR deviennent un seul commit sur la branche cible.

```text
A---B---C---S
```

Exemple :

```text
fix
fix again
tests
cleanup
```

peut devenir :

```text
feat: add payment retry
```

### Avantages

- historique de `main` plus compact ;
- très pratique lorsque les commits de développement sont nombreux ou intermédiaires.

### Inconvénient

- les commits individuels de la branche ne sont plus représentés comme commits séparés dans la branche cible.

## 7.3 Rebase puis fast-forward

Le rebase replace les commits d'une branche au-dessus d'une autre.

```text
Avant :

A---B---C   main
           D---E feature

Après rebase :

A---B---C---D'---E' feature
```

Les commits `D` et `E` deviennent `D'` et `E` car leur historique est réécrit.

## 7.4 Quelle stratégie choisir ?

Il n'existe pas de stratégie universellement correcte.

L'équipe devrait choisir une politique claire et documentée.

Par exemple :

```text
- PR obligatoire
- CI obligatoire
- 1 approval
- squash merge
- branche supprimée après merge
```

Ou une autre politique adaptée au projet.

Le plus important est la **cohérence du workflow**, pas de suivre une stratégie à la mode.

## 7.5 Attention à l'historique réécrit

Un rebase modifie les identifiants des commits.

Sur une branche personnelle non partagée, c'est généralement simple.

Sur une branche utilisée par plusieurs personnes, cela peut provoquer des problèmes.

Avant un force push, vérifier qui travaille sur la branche.

## 7.6 Une politique simple

Pour une équipe qui débute, une politique simple peut être plus facile à comprendre :

```text
main protégée
→ PR obligatoire
→ CI obligatoire
→ review obligatoire
→ squash merge
→ suppression automatique de la branche
```

Cette politique n'est qu'un exemple : elle doit être adaptée au contexte du projet.
