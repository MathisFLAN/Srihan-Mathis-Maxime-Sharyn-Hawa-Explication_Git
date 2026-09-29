# 6. Commandes et cas particuliers

## 6.1 Commandes essentielles

### Voir la branche courante

```bash
git branch --show-current
```

### Voir l'état du dépôt

```bash
git status
```

### Récupérer les modifications distantes

```bash
git fetch origin
```

### Mettre à jour `main`

```bash
git switch main
git pull --ff-only
```

### Créer une branche

```bash
git switch -c feature/ma-feature
```

### Fusionner `main` dans sa branche

```bash
git fetch origin
git merge origin/main
```

### Voir les fichiers en conflit

```bash
git status
```

### Marquer un fichier comme résolu

```bash
git add fichier
```

### Finaliser un merge classique

```bash
git commit
```

### Pousser la branche

```bash
git push
```

### Annuler un merge en cours

```bash
git merge --abort
```

## 6.2 Merge de `main` vs rebase de `main`

### Merge

```bash
git fetch origin
git merge origin/main
```

Historique :

```text
A---B---C---M
     \     /
      D---E
```

Avantage principal : pas de réécriture des commits existants de la branche.

### Rebase

```bash
git fetch origin
git rebase origin/main
```

Historique :

```text
A---B---C---D'---E'
```

Avantage principal : historique linéaire.

Inconvénient : le rebase réécrit les commits de la branche.

Le choix doit suivre la politique de l'équipe.

## 6.3 Résoudre avec un outil graphique

Les éditeurs modernes proposent souvent des interfaces de résolution de conflits.

Elles peuvent afficher :

```text
Current Change
Incoming Change
Result
```

Ces outils facilitent l'édition, mais ils ne remplacent pas la compréhension du conflit.

## 6.4 Vérifier les différences avant de merger

On peut comparer sa branche à `main` :

```bash
git diff origin/main...HEAD
```

Cela permet de voir les changements propres à la branche.

## 6.5 Voir l'historique graphique

```bash
git log --oneline --graph --decorate --all
```

Très utile pour comprendre la situation lorsqu'un historique devient complexe.

## 6.6 Cas : modifications locales non commitées

Si :

```bash
git status
```

indique des modifications non commitées, il faut éviter de lancer un merge sans comprendre l'état du working tree.

Selon le contexte :

- committer les modifications si elles sont prêtes ;
- les mettre temporairement de côté avec `git stash` si cela correspond au workflow ;
- ou terminer/annuler le travail en cours.

Exemple :

```bash
git stash push -m "work in progress"
```

Puis :

```bash
git merge origin/main
```

Après le travail :

```bash
git stash pop
```

Il faut toutefois vérifier les éventuels conflits du `stash pop`.

## 6.7 Cas : le conflit est trop complexe

Ne pas hésiter à :

1. annuler le merge ;
2. discuter avec l'auteur de l'autre modification ;
3. comprendre les comportements attendus ;
4. refaire la fusion ;
5. tester.

Une résolution rapide mais incorrecte coûte souvent plus cher qu'une résolution soigneuse.

## 6.8 Cas : la PR reste en conflit après un push

Vérifier :

```bash
git status
git log --oneline --graph --decorate -n 15
```

Puis vérifier que la branche contient bien les dernières modifications de `main`.

Si nécessaire :

```bash
git fetch origin
git merge origin/main
```

résoudre les conflits, tester et :

```bash
git push
```
