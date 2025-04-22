# 02: Les bases de Git et GitHub

Maintenant que tu es familiere avec les commandes de base du terminal Linux,
on va découvrir Git et comment l'utiliser avec GitHub pour gérer tes projets de programmation.

## Qu'est-ce que Git ?

Git est un système de contrôle de version distribué qui permet de suivre les modifications apportées à tes fichiers au fil du temps. Il te permet de :
- Enregistrer l'historique complet de tes projets
- Collaborer facilement avec d'autres personnes
- Travailler sur différentes versions (branches) d'un même projet
- Revenir à des versions antérieures si nécessaire

## Concepts fondamentaux de Git

### Les 3 états de Git

Dans Git, tes fichiers peuvent être dans trois états principaux :
1. **Modified** : Tu as modifié le fichier mais tu ne l'as pas encore enregistré dans Git
2. **Staged** : Tu as marqué un fichier modifié pour qu'il soit inclus dans le prochain commit
3. **Committed** : Les données sont stockées en sécurité dans ta base de données locale Git

### Le workflow de base

```
┌─────────────┐    git add     ┌─────────────┐    git commit    ┌─────────────┐
│  Working    │ ──────────────>│   Staging   │ ───────────────> │    Local    │
│  Directory  │                │     Area    │                  │ Repository  │
└─────────────┘                └─────────────┘                  └─────────────┘
```

## Commandes Git de base

### Configuration initiale

Configure ton identité Git :

```bash
git config --global user.name "Ton Nom" # ton pseudo github
git config --global user.email "ton.email@exemple.com" # ton adresse mail github
```

### Créer un nouveau dépôt

```bash
# Crée un nouveau directory pour ton projet
mkdir mon_projet
cd mon_projet

# Initialise un dépôt Git vide
git init
```

### Vérifier l'état de ton dépôt

```bash
git status
```

### Ajouter des fichiers au suivi

```bash
# Crée un fichier
echo "# Mon Projet" > README.md

# Ajoute le fichier à la zone de staging
git add README.md

# Pour ajouter tous les fichiers modifiés
# git add .
```

### Créer un commit

Un commit est comme une "sauvegarde" de ton projet à un moment donné.

```bash
git commit -m "Premier commit : ajout du README"
```

### Voir l'historique des commits

```bash
git log
```

Pour une version plus concise :
```bash
git log --oneline
```

## Cloner un dépôt existant

Pour récupérer une copie complète d'un dépôt distant (comme celui contenant ces leçons) :

```bash
git clone https://github.com/titembaatar/alyssa.git
cd alyssa
```

Cela va :
1. Télécharger l'intégralité du dépôt dans un nouveau directory
2. Créer une référence distante nommée "origin" pointant vers le dépôt d'origine
3. Créer une branche locale "main" qui suit la branche "main" distante

## Travailler avec GitHub

GitHub est une plateforme qui héberge des dépôts Git et facilite la collaboration.

### Créer un nouveau dépôt sur GitHub

1. Connecte-toi à ton compte GitHub
2. Clique sur le bouton "+" en haut à droite puis "New repository"
3. Donne un nom à ton dépôt et une description
4. Choisis s'il est public (tout le monde peut voir) ou privé
5. Clique sur "Create repository"

GitHub te donnera ensuite des instructions pour connecter ton dépôt local à GitHub.

### Connecter un dépôt local existant à GitHub

Si tu as déjà un dépôt local (avec `git init`), tu peux le connecter à GitHub :

```bash
# Ajoute GitHub comme "remote" (dépôt distant)
git remote add origin https://github.com/ton-pseudo/ton-depot.git

# Envoie tes commits vers GitHub
git push -u origin main
```

### Les opérations principales avec GitHub

#### Pull : récupérer les modifications distantes

```bash
git pull
```

Cela récupère les dernières modifications depuis GitHub et les fusionne avec ta copie locale.

#### Push : envoyer tes modifications vers GitHub

```bash
git push
```

Cela envoie tes commits locaux vers GitHub.

## Exemple pratique : Travailler avec le dépôt des leçons

### 1. Clone le dépôt des leçons

```bash
git clone https://github.com/username/linux-lessons.git
cd linux-lessons
```

### 2. Examine le contenu

```bash
ls -la
```

### 3. Crée un fichier de notes personnel

```bash
# Crée un directory pour tes notes personnelles
mkdir mes_notes
touch mes_notes/lecon1.md

# Ajoute du contenu à ton fichier
echo "# Mes notes sur la Leçon 1" > mes_notes/lecon1.md
echo "Commandes importantes :" >> mes_notes/lecon1.md
echo "- pwd : affiche le directory courant" >> mes_notes/lecon1.md
echo "- ls : liste les fichiers" >> mes_notes/lecon1.md
```

### 4. Vérifier l'état des modifications

```bash
git status
```

Tu verras que Git a détecté tes nouveaux fichiers mais qu'ils ne sont pas encore suivis.

### 5. Ajouter et committer tes modifications

```bash
git add mes_notes/
git commit -m "Ajout de mes notes personnelles sur la leçon 1"
```

### 6. Si tu as les droits, pousse tes modifications vers GitHub

```bash
git push
```

## Bonnes pratiques Git

1. **Commits fréquents et ciblés** : Fais des commits petits et cohérents plutôt que d'énormes changements
2. **Messages de commit clairs** : Écris des messages de commit informatifs
3. **Pull avant de Push** : Toujours récupérer les dernières modifications avant d'envoyer les tiennes
4. **Revue de code** : Vérifie tes modifications avant de les commit

## Commandes Git supplémentaires utiles

### Voir les différences

```bash
# Voir les modifications non stagées
git diff

# Voir les modifications stagées
git diff --staged
```

### Annuler des modifications

```bash
# Annuler les modifications d'un fichier non stagé
git checkout -- nom_du_fichier

# Désindexer un fichier (le retirer de la zone de staging)
git restore --staged nom_du_fichier

# Modifier le dernier commit
git commit --amend
```

### Branches

```bash
# Créer une nouvelle branche
git branch ma-fonctionnalite

# Changer de branche
git checkout ma-fonctionnalite

# Créer et changer de branche en une seule commande
git checkout -b ma-fonctionnalite
```

## Ressources supplémentaires

- [Documentation officielle Git](https://git-scm.com/doc)
- [GitHub Learning Lab](https://lab.github.com/)
- [Oh Shit, Git!?!](https://ohshitgit.com/) (guide pour corriger les erreurs Git courantes)

