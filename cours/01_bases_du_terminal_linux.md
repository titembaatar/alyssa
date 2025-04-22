# 01: Les bases du terminal Linux

## Qu'est-ce que le terminal?

Le terminal est une interface textuelle qui te permet de communiquer directement avec ton système d'exploitation.
Sous Linux, c'est un outil très puissant qui permet de faire presque tout ce que tu peux imaginer.

## Les commandes de base

### 1. `pwd` - Print Working Directory

Cette commande t'indique dans quel directory (dossier) tu te trouves actuellement.

```bash
pwd
```

Exemple de résultat: `/home/user`

### 2. `ls` - List

Affiche le contenu du directory courant.

```bash
ls
```

Options utiles:
- `ls -l` : Affiche les détails (permissions, taille, date de modification)
- `ls -a` : Affiche aussi les fichiers cachés (qui commencent par un point)
- `ls -la` : Combine les deux options précédentes

### 3. `cd` - Change Directory

Te permet de changer de directory.

```bash
cd Documents
```

Astuces de navigation:
- `cd ..` : Remonte d'un niveau (dossier parent)
- `cd ~` : Retourne à ton directory personnel
- `cd /` : Va à la racine du système
- `cd -` : Retourne au directory précédent

### 4. `mkdir` - Make Directory

Crée un nouveau directory.

```bash
mkdir projet_programmation
```

### 5. `touch`

Crée un fichier vide ou met à jour la date de modification d'un fichier existant.

```bash
touch mon_premier_script.sh
```

### 6. `cat` - Concatenate

Affiche le contenu d'un fichier.

```bash
cat mon_premier_script.sh
```

### 7. `echo`

Affiche du texte dans le terminal.

```bash
echo "Bonjour !"
```

Tu peux aussi rediriger la sortie vers un fichier:

```bash
echo "#!/bin/bash" > mon_premier_script.sh
echo "echo 'Bonjour depuis mon script!'" >> mon_premier_script.sh
```

Note: `>` écrase le contenu, `>>` ajoute à la fin du fichier.

### 8. `nano` - Éditeur de texte simple

Pour éditer des fichiers directement dans le terminal:

```bash
nano mon_premier_script.sh
```

Raccourcis dans nano:
- `Ctrl+O` puis Enter : Sauvegarder
- `Ctrl+X` : Quitter
- `Ctrl+K` : Couper une ligne
- `Ctrl+U` : Coller une ligne

### 9. `chmod` - Change Mode

Change les permissions d'un fichier.

```bash
chmod +x mon_premier_script.sh
```

Cela rend ton script exécutable. Tu peux maintenant l'exécuter avec:

```bash
./mon_premier_script.sh
```

### 10. `man` - Manuel

Affiche la documentation d'une commande.

```bash
man ls
```

Utilise `q` pour quitter.

## Comprendre les permissions

Quand tu fais `ls -l`, tu vois quelque chose comme:
```
-rwxr-xr-x 1 user user 42 Apr 20 10:00 mon_premier_script.sh
```

Les lettres au début indiquent les permissions:
- Premier caractère: Type (- pour fichier, d pour directory)
- Ensuite par groupes de trois (rwx):
  - Owner (propriétaire): rwx = Read, Write, Execute
  - Group (groupe): r-x = Read, pas Write, Execute
  - Others (autres): r-x = Read, pas Write, Execute

## Redirection et pipes

### Redirection
```bash
# Redirige la sortie vers un fichier
echo "Liste de mes fichiers" > liste.txt
ls -la >> liste.txt

# Redirige l'entrée depuis un fichier
cat < liste.txt
```

### Pipes (`|`)
Le pipe envoie la sortie d'une commande à l'entrée d'une autre.

```bash
# Cherche le mot "bash" dans la liste des processus
ps aux | grep bash

# Compte le nombre de fichiers dans le directory courant
ls -1 | wc -l
```

## Commandes d'aide

Si tu es perdue ou si tu as besoin d'aide:

```bash
# Affiche les options d'une commande
ls --help

# Consulte le manuel d'une commande
man ls

# Cherche une commande par mot-clé
apropos "create directory"
```

## Le gestionnaire de paquets (apt)

Ubuntu utilise `apt` pour installer, mettre à jour, et supprimer des logiciels.

Pour utiliser `apt`, tu as besoin des droits administrateur, donc on utilise `sudo` (SuperUser DO).

### Mettre à jour la liste des paquets disponibles
```bash
sudo apt update
```

### Mettre à jour tous les logiciels installés
```bash
sudo apt upgrade
```

### Installer un nouveau logiciel

Voici comment installer Git, un système de contrôle de version très utilisé en programmation:

```bash
sudo apt install git
```

### Vérifier que Git est installé
```bash
git --version
```

Tu devrais voir quelque chose comme: `git version 2.40.1`

