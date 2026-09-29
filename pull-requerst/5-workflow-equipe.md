# 5. Workflow d'équipe

Il n'existe pas une seule stratégie Git universelle. Le workflow doit être adapté au projet, à la fréquence de livraison et au niveau de risque.

## 5.1 Workflow simple

Pour beaucoup de projets, un workflow simple peut suffire :

```text
main
 │
 ├── feature/login
 │
 ├── fix/payment-timeout
 │
 └── feature/export
```

Chaque branche de travail passe par une PR vers `main`.

```text
feature/login
      │
      └── PR → main
```

## 5.2 Exemple de workflow quotidien

### 1. Mettre `main` à jour

```bash
git switch main
git pull --ff-only
```

### 2. Créer une branche

```bash
git switch -c feature/add-export
```

### 3. Développer

```bash
git add .
git commit -m "feat: add export endpoint"
```

### 4. Pousser

```bash
git push -u origin feature/add-export
```

### 5. Créer la PR

Décrire :

- le problème ;
- la solution ;
- les tests ;
- les points d'attention.

### 6. Review

Les reviewers commentent et approuvent ou demandent des changements.

### 7. Corriger

```bash
git add .
git commit -m "fix: handle empty export"
git push
```

La PR est mise à jour automatiquement.

### 8. Merge

Lorsque les règles sont satisfaites, la PR est intégrée.

### 9. Nettoyage

Supprimer la branche distante si la plateforme ne le fait pas automatiquement.

```bash
git push origin --delete feature/add-export
```

## 5.3 Mettre une PR à jour

Si `main` a avancé, deux approches courantes existent.

### Merge de `main`

```bash
git fetch origin
git merge origin/main
```

Avantage : ne réécrit pas l'historique de la branche.

### Rebase

```bash
git fetch origin
git rebase origin/main
```

Avantage : historique linéaire.

Inconvénient : le rebase réécrit l'historique de la branche.

Une politique d'équipe claire évite les décisions contradictoires.

## 5.4 Force push

Après un rebase d'une branche déjà poussée, Git peut nécessiter :

```bash
git push --force-with-lease
```

Préférer `--force-with-lease` à :

```bash
git push --force
```

`--force-with-lease` fournit une protection supplémentaire contre l'écrasement involontaire de changements distants.

Attention : même `--force-with-lease` doit être utilisé selon les règles de l'équipe.

## 5.5 Merge queue

Pour les projets avec beaucoup de PR, une merge queue peut permettre de tester les changements dans l'ordre d'intégration prévu.

Cela réduit notamment les situations où plusieurs PR sont individuellement vertes mais deviennent incompatibles lorsqu'elles sont intégrées ensemble.

## 5.6 Trunk-based development

Une équipe peut choisir de travailler principalement avec une branche principale et des branches de courte durée.

```text
main
 ├── feature/a
 ├── feature/b
 └── fix/c
```

Les changements sont intégrés fréquemment.

Ce modèle fonctionne particulièrement bien avec :

- des PR petites ;
- une CI fiable ;
- des feature flags lorsque nécessaire ;
- des déploiements fréquents.

## 5.7 Git Flow

Certaines équipes utilisent plusieurs branches longues durées comme `develop`, `release` et `main`.

Ce modèle peut être pertinent dans certains contextes, mais il ajoute de la complexité.

Le choix doit venir des contraintes du projet plutôt que d'une préférence personnelle.

## 5.8 Définir une politique d'équipe

Documenter explicitement :

- branche cible par défaut ;
- convention de nommage ;
- convention de commits ;
- nombre d'approveurs ;
- checks obligatoires ;
- stratégie de merge ;
- politique de rebase ;
- politique de force push ;
- suppression des branches ;
- gestion des hotfixes.
