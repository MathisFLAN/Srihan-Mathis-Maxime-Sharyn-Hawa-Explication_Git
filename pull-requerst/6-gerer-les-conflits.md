# 6. Gérer les conflits dans une Pull Request

## 6.1 Pourquoi un conflit apparaît ?

Un conflit apparaît lorsque Git ne peut pas déterminer automatiquement quelle version conserver.

Exemple :

```text
main :
const timeout = 5000;

feature :
const timeout = 10000;
```

Si les deux modifications concernent la même zone, Git peut demander une résolution manuelle.

## 6.2 Identifier les conflits

```bash
git fetch origin
git status
```

Après un merge :

```bash
git merge origin/main
```

Git peut indiquer les fichiers en conflit.

## 6.3 Résoudre un conflit

Dans le fichier, Git peut afficher :

```text
<<<<<<< HEAD
const timeout = 5000;
=======
const timeout = 10000;
>>>>>>> origin/main
```

Il faut décider quelle version correspond au comportement attendu, puis supprimer les marqueurs.

Ensuite :

```bash
git add fichier.js
git commit
```

Pour un rebase :

```bash
git add fichier.js
git rebase --continue
```

## 6.4 Ne pas résoudre un conflit « au hasard »

Un conflit n'est pas seulement un problème syntaxique.

Il faut comprendre les deux changements.

Questions utiles :

- Pourquoi la branche `main` a-t-elle changé cette ligne ?
- Pourquoi ma branche la modifie-t-elle ?
- Les deux comportements sont-ils nécessaires ?
- Faut-il combiner les changements ?
- Les tests couvrent-ils le comportement résultant ?

## 6.5 Demander de l'aide

Pour un conflit complexe, demander au propriétaire du changement concerné peut être plus sûr que de choisir seul.

Exemple :

> J'ai un conflit entre la nouvelle gestion des permissions et ma modification de l'API. Peux-tu confirmer le comportement attendu avant que je résolve le conflit ?

## 6.6 Après résolution

Toujours :

1. relire le diff ;
2. lancer les tests pertinents ;
3. vérifier qu'aucune fonctionnalité n'a disparu ;
4. vérifier que les fichiers de configuration sont corrects ;
5. pousser les changements.

Une résolution de conflit peut compiler tout en introduisant un bug fonctionnel.
