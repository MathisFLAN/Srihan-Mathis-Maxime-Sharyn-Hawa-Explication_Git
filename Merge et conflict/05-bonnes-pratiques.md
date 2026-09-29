# 5. Bonnes pratiques d'équipe

## 5.1 Partir d'une branche à jour

Avant de créer une nouvelle branche :

```bash
git switch main
git pull --ff-only
git switch -c feature/ma-tache
```

Cela réduit les divergences inutiles.

## 5.2 Faire des branches courtes

Plus une branche reste longtemps séparée de `main`, plus le risque de conflit augmente.

Préférer :

```text
petite tâche
→ branche
→ développement
→ PR
→ review
→ merge
```

plutôt qu'une branche qui reste ouverte pendant plusieurs semaines.

## 5.3 Mettre régulièrement sa branche à jour

Si `main` évolue beaucoup, il peut être utile de l'intégrer régulièrement dans sa branche.

Avec merge :

```bash
git fetch origin
git merge origin/main
```

Ou avec rebase si c'est la convention du projet :

```bash
git fetch origin
git rebase origin/main
```

## 5.4 Ne pas résoudre un conflit sans comprendre

Ne pas simplement choisir :

```text
Current
```

ou :

```text
Incoming
```

dans son éditeur sans comprendre ce que ces versions représentent.

Lire les deux modifications et déterminer le comportement attendu.

## 5.5 Communiquer en cas de conflit complexe

Si deux développeurs ont travaillé sur la même fonctionnalité, ils peuvent avoir des informations importantes sur l'intention des changements.

Un conflit complexe est parfois plus rapide à résoudre à deux qu'en essayant de deviner.

## 5.6 Tester après chaque résolution importante

Une résolution de conflit peut :

- supprimer une validation ;
- réintroduire un bug ;
- supprimer un import ;
- modifier un comportement ;
- rendre deux parties du code incompatibles.

Les tests sont donc indispensables.

## 5.7 Éviter les gros changements sans rapport

Un conflit est beaucoup plus difficile à résoudre lorsque la PR contient :

- une fonctionnalité ;
- un refactoring massif ;
- un changement de formatting ;
- des renommages de fichiers ;
- une mise à jour de dépendances.

Limiter le périmètre des PR réduit les conflits et facilite la review.

## 5.8 Protéger `main`

Dans un dépôt d'équipe, `main` peut être protégée avec des règles telles que :

- PR obligatoire ;
- review obligatoire ;
- CI obligatoire ;
- interdiction du push direct ;
- interdiction du force push ;
- branche à jour avant merge.

Les règles exactes dépendent de l'outil et du niveau de risque du projet.

## 5.9 Une résolution de conflit doit être reviewable

Si la résolution est importante, le reviewer doit pouvoir comprendre le résultat.

L'auteur peut signaler dans la PR :

> La branche a été mise à jour avec `main`. Le conflit concernait `index.html` et a été résolu en conservant le nouveau titre tout en gardant la structure ajoutée dans `main`.

Cela donne du contexte au reviewer.
