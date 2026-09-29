# 4. Vérifier et finaliser la résolution

Résoudre un conflit ne signifie pas simplement supprimer les marqueurs Git.

Il faut vérifier que le résultat est réellement correct.

## 4.1 Vérifier l'état Git

```bash
git status
```

Il ne doit plus rester de fichiers indiqués comme non fusionnés.

## 4.2 Vérifier le diff

Après le merge :

```bash
git diff HEAD^
```

Pour examiner plus largement l'état de la branche :

```bash
git diff origin/main...HEAD
```

L'objectif est de vérifier que :

- les modifications de sa branche sont toujours présentes ;
- les modifications de `main` sont présentes ;
- aucune partie de code n'a été supprimée accidentellement ;
- le résultat correspond au comportement attendu.

## 4.3 Rechercher les marqueurs de conflit

On peut également rechercher les marqueurs dans le projet :

```bash
git grep -n -e '<<<<<<<' -e '=======' -e '>>>>>>>'
```

S'il reste des marqueurs, ils doivent être examinés avant de poursuivre.

## 4.4 Lancer les tests

Exécuter les tests adaptés au projet.

Exemples :

```bash
npm test
npm run lint
```

ou :

```bash
pytest
```

ou la commande de test officielle du projet.

## 4.5 Vérifier manuellement si nécessaire

Pour une interface, on peut par exemple :

- lancer l'application ;
- ouvrir la page modifiée ;
- vérifier le comportement ;
- vérifier les erreurs dans la console.

Pour une API :

- lancer les tests ;
- appeler les endpoints concernés ;
- vérifier les réponses.

## 4.6 Push et mise à jour de la PR

Lorsque tout est correct :

```bash
git push
```

La PR reflète alors la nouvelle version de la branche.

Les checks CI sont généralement relancés automatiquement.

## 4.7 Abandonner un merge en cours

Si la résolution est devenue trop complexe ou si l'on s'est trompé, il est possible d'annuler un merge en cours :

```bash
git merge --abort
```

Cette commande tente de revenir à l'état précédent le début du merge.

Elle est particulièrement utile lorsque l'on veut repartir proprement.

> `git merge --abort` doit être utilisé **pendant qu'un merge est en cours**. Une fois le merge terminé par un commit, cette commande ne permet plus d'annuler ce commit.

## 4.8 Annuler un merge déjà terminé

Si le merge a déjà été commité, la situation est différente.

Avant toute action, vérifier l'historique :

```bash
git log --oneline --graph --decorate -n 10
```

Selon le contexte, on peut utiliser `git revert` pour annuler les effets d'un merge déjà intégré, notamment lorsqu'il a déjà été partagé avec l'équipe.

L'annulation d'un merge déjà publié doit être traitée avec prudence et suivre les règles du projet.
