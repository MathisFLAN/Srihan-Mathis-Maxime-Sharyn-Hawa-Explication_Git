# Initialiser Git sur un projet

Ce guide explique comment commencer à suivre un projet avec Git, puis comment publier son historique sur un dépôt distant comme GitHub.

## 1. Vérifier l'installation de Git

Ouvrez un terminal dans le dossier du projet et vérifiez que Git est disponible :

```bash
git --version
```

Si une version s'affiche, Git est installé. Sinon, installez Git depuis [git-scm.com](https://git-scm.com/downloads), puis rouvrez le terminal.

## 2. Ouvrir le dossier du projet

Dans le terminal, placez-vous à la racine du projet, c'est-à-dire dans le dossier qui contient ses fichiers :

```bash
cd chemin/vers/mon-projet
```

Sous Windows, vous pouvez aussi ouvrir le dossier dans l'Explorateur de fichiers, cliquer dans la barre d'adresse, saisir `cmd` ou `powershell`, puis appuyer sur Entrée.

## 3. Configurer son identité

Git inscrit un nom et une adresse e-mail dans chaque commit. Configurez-les une seule fois pour votre compte utilisateur :

```bash
git config --global user.name "Votre nom"
git config --global user.email "vous@example.com"
```

Pour vérifier la configuration :

```bash
git config --global --list
```

## 4. Initialiser le dépôt

À la racine du projet, lancez :

```bash
git init
```

Cette commande crée un dossier caché `.git` contenant l'historique et la configuration du dépôt. Les fichiers du projet ne sont pas déplacés ni modifiés.

Vérifiez l'état du dépôt avec :

```bash
git status
```

### Comprendre le résultat de `git status`

Cette commande ne modifie rien : elle indique sur quelle branche vous vous trouvez et compare les fichiers du dossier avec le dernier commit. Elle distingue notamment :

- **Modifications à valider** (`Changes to be committed`) : les fichiers ont été préparés avec `git add` et seront inclus dans le prochain commit.
- **Modifications non préparées** (`Changes not staged for commit`) : les fichiers suivis ont changé, mais il faut encore les ajouter avec `git add` pour inclure ces changements au prochain commit.
- **Fichiers non suivis** (`Untracked files`) : Git a détecté de nouveaux fichiers, mais ils ne sont pas encore suivis. Utilisez `git add nom-du-fichier` pour les inclure, ou ajoutez-les à `.gitignore` s'ils ne doivent pas être versionnés.
- **Dépôt propre** (`nothing to commit, working tree clean`) : aucun changement local n'attend d'être ajouté ou commité.

Après un `git add`, relancez `git status` pour vérifier que les fichiers sont bien dans la liste des modifications à valider. Après un `git commit`, vérifiez à nouveau que le dépôt est propre.

Pour une vue abrégée, utilisez `git status --short`. Les indicateurs courants sont `??` pour un fichier non suivi, ` M` pour une modification non préparée et `M ` pour une modification préparée. Dans cette sortie, la première position correspond à l'index (préparation) et la seconde aux changements dans les fichiers.

## 5. Ignorer les fichiers inutiles

Avant le premier commit, créez un fichier `.gitignore` à la racine. Il indique à Git quels fichiers ne doivent pas être suivis, par exemple les fichiers temporaires, les dépendances générées ou les secrets.

Exemple générique à adapter au projet :

```gitignore
# Fichiers temporaires et journaux
*.log
*.tmp

# Secrets locaux
.env

# Fichiers système
.DS_Store
Thumbs.db
```

Ne placez jamais de mot de passe, clé privée ou jeton d'accès dans un dépôt. Si un secret a déjà été commité, l'ajouter ensuite à `.gitignore` ne le retire pas de l'historique.

## 6. Créer le premier commit

Ajoutez les fichiers que vous souhaitez suivre. Pour tout ajouter sauf les fichiers ignorés :

```bash
git add . 
```


```bash
git status
git diff --cached
```

Créez ensuite le premier commit avec un message descriptif :

```bash
git commit -m "Initialisation du projet"
```

Un commit est un point de sauvegarde nommé dans l'historique Git. Après le commit, `git status` doit indiquer que l'arbre de travail est propre si aucun autre changement n'a été fait.

## 7. Définir la branche principale

Pour utiliser `main` comme nom de branche principale :

```bash
git branch -M main
```

Cette commande renomme la branche actuelle en `main`.

## 8. Relier le projet à un dépôt distant (facultatif)

Créez d'abord un dépôt vide sur la plateforme de votre choix. Si le projet existe déjà localement, évitez de demander à la plateforme de créer un README, une licence ou un `.gitignore` : ces fichiers pourraient entrer en conflit avec ceux du projet local.

Copiez l'URL du dépôt distant, puis enregistrez-la sous le nom `origin` :

```bash
git remote add origin https://github.com/nom-utilisateur/nom-du-projet.git
```

Vérifiez l'adresse configurée :

```bash
git remote -v
```

Envoyez la branche `main` sur le dépôt distant :

```bash
git push -u origin main
```

L'option `-u` associe la branche locale à la branche distante. Pour les envois suivants, `git push` suffit généralement.

## Cas d'un dépôt distant déjà existant

Si le projet existe déjà sur GitHub ou une autre plateforme et que vous voulez en récupérer une copie, utilisez plutôt `git clone` :

```bash
git clone https://github.com/nom-utilisateur/nom-du-projet.git
cd nom-du-projet
```

Le clonage télécharge les fichiers et l'historique, et configure automatiquement le dépôt distant `origin`. Il n'est alors pas nécessaire de lancer `git init`.

## Commandes courantes

```bash
git status                  # Voir les changements
git add fichier             # Préparer un fichier pour le prochain commit
git add .                   # Préparer tous les changements non ignorés
git commit -m "Message"     # Enregistrer les changements
git pull                    # Récupérer les changements distants
git push                    # Envoyer les commits vers le dépôt distant
```

## En cas de problème

- **`git` n'est pas reconnu** : vérifiez l'installation, puis fermez et rouvrez le terminal.
- **Git demande une identité** : configurez `user.name` et `user.email` avec les commandes de la section 3.
- **`git push` est refusé** : vérifiez l'URL avec `git remote -v`, votre accès au dépôt et la présence éventuelle de commits distants à récupérer avec `git pull`.
- **Un fichier ignoré apparaît encore dans Git** : `.gitignore` n'arrête pas le suivi d'un fichier déjà ajouté ou commité. Il faut retirer ce fichier de l'index sans supprimer sa copie locale, par exemple avec `git rm --cached nom-du-fichier`, puis créer un commit.
