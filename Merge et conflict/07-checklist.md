# 7. Checklist

## Avant de créer une branche

- [ ] `main` est à jour
- [ ] Le nom de branche respecte la convention
- [ ] La tâche est suffisamment claire

```bash
git switch main
git pull --ff-only
git switch -c feature/ma-tache
```

## Avant la Pull Request

- [ ] Les modifications sont commitées
- [ ] Le code a été testé
- [ ] Le diff a été relu
- [ ] La branche a été poussée
- [ ] La PR cible la bonne branche

```bash
git status
git diff
git push
```

## Avant de résoudre un conflit

- [ ] Je suis sur la bonne branche
- [ ] Mes changements sont enregistrés
- [ ] J'ai récupéré les dernières informations du dépôt

```bash
git switch feature/ma-tache
git status
git fetch origin
```

## Résolution

- [ ] J'ai identifié tous les fichiers en conflit
- [ ] J'ai compris les deux versions
- [ ] J'ai choisi le comportement attendu
- [ ] J'ai supprimé les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`
- [ ] J'ai ajouté les fichiers résolus

```bash
git status
git add fichier
```

## Après résolution

- [ ] Le merge est finalisé
- [ ] Le diff a été vérifié
- [ ] Aucun marqueur de conflit ne reste
- [ ] Les tests passent
- [ ] La branche a été poussée
- [ ] La PR est à jour

Commandes utiles :

```bash
git status
git diff HEAD^
git grep -n -e '<<<<<<<' -e '=======' -e '>>>>>>>'
git push
```

## En cas de problème

Si le merge est toujours en cours :

```bash
git merge --abort
```

Puis prendre le temps de comprendre le conflit avant de recommencer.

---

# Résumé du workflow

```text
1. Créer une branche
       ↓
2. Développer
       ↓
3. Commit
       ↓
4. Push
       ↓
5. Pull Request
       ↓
6. Review + CI
       ↓
7. Si nécessaire : mettre à jour avec main
       ↓
8. Résoudre les conflits
       ↓
9. Tester
       ↓
10. Push
       ↓
11. Merge de la PR
```

> **Principe essentiel :** un conflit n'est pas une erreur de Git. C'est une situation dans laquelle Git demande à l'équipe de décider quel doit être le résultat final.

# Par Srihan