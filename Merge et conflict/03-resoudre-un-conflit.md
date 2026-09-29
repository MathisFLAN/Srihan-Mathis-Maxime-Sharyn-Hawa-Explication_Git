# 3. Résoudre un conflit sur sa branche

Dans cet exemple, nous allons intégrer les dernières modifications de `main` dans :

```text
feature/page-accueil
```

Nous utilisons `git merge`, ce qui permet de mettre à jour la branche sans réécrire son historique.

## 3.1 Vérifier sa branche

```bash
git switch feature/page-accueil
```

Puis vérifier que le travail local est enregistré :

```bash
git status
```

Avant de commencer, il est préférable d'avoir un working tree propre.

Si des modifications locales ne sont pas encore prêtes à être commitées, il faut soit les committer, soit utiliser une autre stratégie adaptée au contexte.

## 3.2 Récupérer les dernières informations du dépôt distant

```bash
git fetch origin
```

`git fetch` récupère les nouvelles informations depuis le dépôt distant sans modifier directement les fichiers de travail.

On dispose ensuite notamment de :

```text
origin/main
```

qui représente l'état connu de `main` sur le dépôt distant.

## 3.3 Fusionner `main` dans sa branche

```bash
git merge origin/main
```

Deux situations sont possibles.

### Aucun conflit

Git effectue automatiquement la fusion.

On peut ensuite vérifier :

```bash
git status
```

Puis lancer les tests.

### Un conflit apparaît

Git indique les fichiers concernés.

Par exemple :

```text
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

## 3.4 Identifier les fichiers en conflit

```bash
git status
```

Git peut afficher quelque chose comme :

```text
Unmerged paths:
  both modified:   index.html
```

Les fichiers concernés doivent être examinés.

## 3.5 Ouvrir les fichiers concernés

Dans `index.html` :

```html
<<<<<<< HEAD
<h1>Bienvenue sur notre site</h1>
=======
<h1>Bienvenue sur le projet Git</h1>
>>>>>>> origin/main
```

Il faut décider du résultat final.

Par exemple :

```html
<h1>Bienvenue sur notre projet Git</h1>
```

Puis enregistrer le fichier.

## 3.6 Indiquer à Git que le conflit est résolu

Une fois le fichier corrigé :

```bash
git add index.html
```

Vérifier ensuite :

```bash
git status
```

Git doit maintenant considérer le fichier comme résolu.

## 3.7 Finaliser le merge

Pour un merge classique, la commande :

```bash
git merge --continue
```

n'est généralement pas nécessaire.

Après avoir résolu les conflits et exécuté `git add`, on finalise habituellement avec :

```bash
git commit
```

Git propose alors généralement un message de commit de merge.

On peut également fournir son propre message :

```bash
git commit -m "merge: integrate latest main changes"
```

> `git merge --continue` est surtout utile dans certains workflows de fusion, mais pour un merge classique interrompu par un conflit, `git commit` est la commande habituelle pour finaliser la fusion.

## 3.8 Pousser la résolution

Une fois le merge terminé :

```bash
git push
```

La branche distante est mise à jour.

La Pull Request sur GitHub est alors mise à jour avec la résolution du conflit.

## 3.9 Tester

Après une résolution de conflit, il faut impérativement tester le projet.

Au minimum :

```bash
git diff HEAD^
```

Puis exécuter les tests adaptés au projet.

Exemples :

```bash
npm test
```

ou :

```bash
pytest
```

ou les commandes définies par le projet.

Une résolution peut être syntaxiquement correcte tout en supprimant involontairement un comportement.
