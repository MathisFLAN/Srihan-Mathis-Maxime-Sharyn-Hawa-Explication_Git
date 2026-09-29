# Les commandes essentielles de Git

Git est un outil de gestion de versions. Il permet de suivre les changements d’un projet, de revenir à une version précédente et de travailler à plusieurs.

## Comprendre les trois zones

Avant d’utiliser les commandes, il est utile de distinguer :

- **Le répertoire de travail** : les fichiers sur lesquels vous travaillez.
- **La zone de préparation** (*staging area*) : les changements choisis pour le prochain enregistrement.
- **Le dépôt** : l’historique des versions enregistrées sous forme de commits.

Le cycle habituel est : modifier des fichiers, les préparer avec `git add`, puis enregistrer les changements avec `git commit`.

## Démarrer un dépôt

Créer un dépôt Git dans le dossier courant :

```bash
git init
```

Récupérer une copie d’un dépôt distant :

```bash
git clone https://github.com/utilisateur/projet.git
```

Remplacez l’adresse d’exemple par celle du dépôt à récupérer.

## Vérifier et enregistrer les changements

Afficher l’état du dépôt :

```bash
git status
```

Ajouter un fichier à la zone de préparation :

```bash
git add README.md
```

Ajouter tous les changements du dossier courant :

```bash
git add .
```

Enregistrer les changements préparés dans l’historique :

```bash
git commit -m "Décrire le changement"
```

Un bon message de commit est court et indique clairement ce qui a été fait, par exemple : `Ajoute la page de présentation`.

## Consulter l’historique et les différences

Afficher les commits récents :

```bash
git log --oneline
```

Voir les changements qui ne sont pas encore préparés :

```bash
git diff
```

Voir les changements déjà préparés pour le prochain commit :

```bash
git diff --staged
```

## Travailler avec des branches

Une branche permet de développer une fonctionnalité sans modifier directement la branche principale.

Afficher les branches locales :

```bash
git branch
```

Créer une branche et basculer dessus :

```bash
git switch -c nom-de-branche
```

Basculer vers une branche existante :

```bash
git switch nom-de-branche
```

Fusionner une branche dans la branche actuelle :

```bash
git merge nom-de-branche
```

En cas de conflit, Git indique les fichiers concernés. Il faut corriger ces fichiers, puis les ajouter avec `git add` et terminer la fusion avec `git commit` si Git le demande.

## Échanger avec un dépôt distant

Récupérer les changements distants et les intégrer à la branche actuelle :

```bash
git pull
```

Envoyer les commits locaux vers le dépôt distant :

```bash
git push
```

Pour publier une nouvelle branche distante lors de son premier envoi :

```bash
git push -u origin nom-de-branche
```

`origin` est le nom distant utilisé le plus souvent par défaut. La commande `git remote -v` permet de vérifier les dépôts distants configurés.

## Annuler ou retirer un changement

Retirer un fichier de la zone de préparation tout en conservant ses modifications :

```bash
git restore --staged nom-du-fichier
```

Annuler les modifications locales d’un fichier non préparé :

```bash
git restore nom-du-fichier
```

**Attention :** cette dernière commande supprime les modifications non enregistrées de ce fichier. Vérifiez toujours `git status` et `git diff` avant de l’utiliser.

## Exemple de cycle complet

```bash
git status
git add README.md
git commit -m "Met à jour le README"
git pull
git push
```

En pratique, vérifiez l’état avec `git status` avant et après vos opérations. Cela aide à savoir quels changements sont prêts à être enregistrés ou envoyés.
