
# atelier git

- [`Introduction`](#Introduction)
    - [`Glossaire`](#Glossaire)
    - [`git en bref résumé`](#git-en-bref-r%C3%A9sum%C3%A9-)
    - [`Historique (d'où vient git)`](#historique-do%C3%B9-vient-git-)
        - [`1ere generation de VCS`](#1ere-g%C3%A9n%C3%A9ration-de-syst%C3%A8me-de-control-de-version)
        - [`2eme generation de VCS`](#2eme-g%C3%A9n%C3%A9ration-de-syst%C3%A8me-de-control-de-version)
        - [`3eme generation de VCS`](#3eme-g%C3%A9n%C3%A9ration-de-syst%C3%A8me-de-control-de-version)
    - [`Alternatives`](#Alternatives-)
- [Vue d'ensembe d'un repo](#vue-densembe-dun-repo)
    - [`git add`](#git-add)
    - [`git status`](#git-status)
    - [`git commit`](#git-commit)
    - [`git push`](#git-push)
    - [`git pull`](#git-pull)
    - [`git remote`](#git-remote)
    - [`git diff`](#git-diff)
    - [`git log`](#git-log)

    

## `Introduction`

### Glossaire 

Différents termes pour dire for "version control system":
- VCS : Version Control Software / Version Control System
- SCM : Source Control Management / Software Configuration Management
- Revision Control


Abréviations de VCS:
- SCCS : Source Code Control System
- RCS : Revision Control System
- CVS : Concurrent Version System
- SVN : Apache Subversion

### git en bref résumé : 

**git** : un logiciel de control de version décentralisé.

Créer en 2005 par Linus Torvalds pour pouvoir gérer les versions du noyau linux.

#### un logiciel de control de version :

- Pouvoir gérer différentes versions d'un logiciel.
- Optimisation de la mémoire (avec un système qui enregistre les différences d'un fichiers entre deux patches plutôt que le fichier entier à chaque état du projet)
- Savoir qui à changer quoi et quand.
- Savoir quel version du logiciel le client a sur son pc.

<small> <small> Pratique pour avoir un historique de l'évolution d'un code source, sans avoir à créer des dossiers libft_V1, libft_V2, libft_Vfinale, libft_Vfinale_2, libft_Vfinal_final.

Permet de travailler facilement en groupe, ou chacun à accès au code et peu le modifier de son côté. 
</small></small>  

#### Centralisé (centralized) versus Décentralisé (distributed) :

    
**centralisé** : 

Pas de copie sur l'ordinateur local, il faut se connecter à un serveur pour pouvoir travailler sur un projet.

**Décentralisé** :

Le répertoire entier, incluant le code source et l'historique, est copié localement sur l'ordinateur de chaque developper travaillant sur le projet.

Donc pas de version centrale du code source, chaque developpeur à sa copie local du répertoire avec ses potentiels changements.


NOTE : il existe quand même un serveur général où tout le monde va partager ses modifications et récupérer les modifications des autres (ex: Mercurial, GitLab, SourceForge, Bitbucket, Github, ...)

souvent utilisé pour gérer le code source d'un programme.

**avantages / inconvénients** :

Exemple d'avantages d'un système décentralisé :
- possibilité de travailler hors-ligne
- les copies local du répertoires sont aussi des backups : il n'y a pas un seul endroit ou se situe le code source.

Exemples de désavantages d'un système décentralisé :
- Peu prendre beaucoup de place, vu que chaque personne fait une copie entière du répertoire. (-> à vérifier, mais : un studio de jeu AAA n'utilisera jamais git car pas adapté pour gérer tous les assets, mais plus quelque chose comme Perforce)
- Un code plus facilement exposé, vu qu'il est présent sur plein de machine.



### `Historique (d'où vient git)` : 

Les différentes générations de système de control de version:

|Generation|Networking|Operations|Concurrency|Examples|
|----------|----------|----------|-----------|--------|
|1ère|Aucun|Un fichier à la fois|Locks|SCCS, RCS|
|2ème|Centralisé|Plusieurs fichiers|Merge avant de commit|CVS, SourceSafe, Subversion|
|3ème|Décentralisé|Changeset|Commit avant de Merge|Bazaar, git, Mercurial, BitKeeper|

source : https://ericsink.com/vcbe/html/history_of_version_control.html

#### 1ere génération de système de control de version

- en 1972 SCCS (Source Code Control System) : le premier système de controle de version, il apporte les notions de :
    - système de lock pour pouvoir modifier un fichier
    - enregistrement de changements incremental
    - gérer plusieurs versions

- en 1982 RCS (Revison Control System), un SCCS amélioré:
    - des branches 
    - possibilité de unlock un fichier

#### 2eme génération de système de control de version

- en 1985 CVS (concurrent version system) : à la base un script qui sert de front-end à RCS
    - architecture client-server : le serveur contient le repo, et le client parle à ce serveur pour avoir accès au code, modifier le code, et pleins d'autres opérations.

- en 2001 SVN (Apache subversion) : une refonte de CVS pour palier à ses défaults et ajouts de fonctionnalités manquantes à CVS

#### 3eme génération de système de control de version

##### en 1998:

le projet Linux commence à être vraiment gros, et jusque là, le système de control de version, c'est juste Linus Torvald. Qui par la même occasion déteste CVS et prefére ne rien utiliser que d'utiliser CVS. 

##### Toujours en 1998:

un mec (Larry McVoy) propose son idée d'outil de controle de version décentralisé à Linus qui lui réponds que c'est cool, qu'il aime l'idée.

##### en 2000 :

Ce même mec (Larry McVoy) sort alors BitKeeper en 2000, historiquement le premier des système de controle de version **décentralisé**.

##### en 2002 :

BitKeeper est adopté pour le gestion de contrôle du noyau linux. Mais c'est un logiciel propriétaire certains termes de la license sont très restrictif :
- Interdit de reverse-engineer quoi que ce soit lié à BitKeeper.
- Interdiction de participer au développement d'un outil concurrent à BitKeeper.

L'adoption de BitKeeper fait beaucoup débat dans la communauté linux.

##### en 2005 :

ça fini par exploser et Larry McVoy retire la license pour utiliser BitKeeper pour gérer le noyau linux pour différentes raisons (non respect de la license entre autres.
    
Il faut rapidement une alternative a BitKeeper pour permettre la suite du développement du noyau, les alternatives existantes à l'époque sont essentiellement:
- monotone
- DARCS

Mais les alternatives sont trop inéfficientes.

En avril 2005 : Linus décide d'écrire son propre logiciel de gestion de version et il sort git. 

Le 16 juin 2005, la version 2.6.12 du noyau est gérer avec git.

Note : c'est apparement pas du tout le linux qu'on connais aujourd'hui et c'était vraiment dur à prendre en main et c'était développer vraiment pour les besoins de Linus et l'intégration du développement du noyau.

- en 2007 : après pas mal de modification, git est prêt à être utilisé pour gérer d'autre logiciel que le noyau linux.

### Alternatives :

- Donc aujourd'hui : pour le version control, la majorité utilise git, avec leur répertoire sur github, mais il existe des alternative :

#### Alternative a git :

le plus populaire et je dirais le seul viable et maintenu à ce jour ? :
- Mercurial 

sinon d'après 'git survey' en 2007, voici ce que les gens utilisaient pour gérer le versionning de leur projet (pour 654 répondants (plusieurs réponses possibles)) pour donner une idée :

|Réponses|nombre|Réponses|nombres|Réponses|nombres|
|--------|------|--------|-------|--------|-------|
AccuRev |	3| Mercurial |	92|Subversion |	524|
Aegis |	1|Monotone |31|Sun NSE 	|2|
Bazaar |	19|Omniworks |	1|Sun TeamWare |	4|
Bazaar-NG 	|50|OpenCM |	1|VCS 	|1|
BitKeeper |	27|PRCS |	1|VMS 	|1|
CCC |	1|PVCS 	|12|VSS 	|26|
CMS (Digital) |	1|Perforce 	|50|'cp -a' 	|1|
CMS (VAX) |	1|Quilt |	2|akpm patch scripts| 	1|
CMS (VMS) |	1|RCS 	|61|custom in-house tools 	|1|
CVCS | 	1|SCCS |	18|diff patch |	2|
CVS |	454|SCM 	|1|notes-on-paper-made-by-hand |	1|
ClearCase |	43|SCSS |	1|really horrible stuff |	1|
CodeMgr |1|SVK |	19|scripts for 'shadow trees' |	1|
Continuus 	|1|Sourcerer's Apprentice 	|1|tarballs 	|1|
Darcs 	|78|SourceForge |	1|tlib 	|1|none 	|9|
DesignSync |	1|Serena Version Manager |	1|undisclosed 	|1 |
GNU Arch 	|57|StarTeam 	|4|

source :  https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitSurvey2007.html#10._What_other_SCMs_did.2Fdo_you_use.3F


#### Alternative à GitHub :

- SourceForge
- Bitbucket
- GitLab
- Gitea

### NOTES:

- De grosses entreprise comme Facebook et Google n'utilise pas / plus git. Car trop peu efficient pour gérer les énormes historiques de projet.

- Les studios de jeu AAA vont préférer un système centralisé, car trop long / pas pratique de télécharger tous le répo qui peut peser plusieurs Tera octets de données.

ci-dessous un graphique de l'évolution de l'adoption de git versus svn pour la gestion de version d'après un songae eclispe :

![grpahique de l'évolution de l'adoption de git versus svn](images/git_vs_svn.png)


source : https://softwareengineering.stackexchange.com/a/150791


### sources :

- https://en.wikipedia.org/wiki/Git
- https://en.wikipedia.org/wiki/Version_control
- https://en.wikipedia.org/wiki/Distributed_version_control
- https://graphite.com/blog/bitkeeper-linux-story-of-git-creation
- https://www.youtube.com/watch?v=W3hr-F8ie94
- https://ericsink.com/vcbe/html/history_of_version_control.html
- https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitSurvey2006.html

### a voir submodule et autres (jweber)


### config son git 

Git fonctionne avec une configuration pour etablir des logs precis et des strategie par défaut.

`git config --global user.name` permet de set le nom de l'utilisateur git (qui sera affiché dans les logs)
`git config --global user.email` permet de set l'email de l'utilisateur git (qui sera affiché dans les logs)
`git config --global init.defaultBranch` permet d'etablir la branch par defaut lors d'un git init
`git config --global core.editor` permet de choisir quel editeur ouvrir quand il y a un besoin de message (ex: git commit)


# Utilisations basique et commandes principales :

## Vue d'ensembe d'un repo

Un repo est globalement divisé en 4 parties :

### 1. **Copie de travail** (**working tree**)

C'est le contenu présent sur le disque, ce que tu peux éditer en créant, supprimant ou modifiant un fichier.

### 2. **Index** (**staging area**)

La zone intermédiaire avant le commit. Elle permet de sélectionner ce que tu veux mettre dans un commit avec [`git add`](#git-add) avant de le commit

### 3. **Dépôt local** (**local repository**)

Tout ce qui a été ajouté "définitivement" au repo git est présent ici.  
On retrouve dans le dossier `.git` à la racine du repo, tous les commits, toutes les branches, les tags, etc.  
Les modifications y sont ajoutées avec la commande [`git commit`](#git-commit) depuis l'index.

### 4. **Dépôt distant** (**remote repository**)

C'est la copie externe du repo présent localement sur ta machine.  
Désigné par la `remote` (voir [`git remote`](#git-remote)) le dépôt distant permet de centraliser toutes les modifications depuis le début du projet. Ca permet simplement d'avoir un seul endroit commun où partager ses modifications.  
Il existe beaucoup de services de gestion de dépôt distant, bien le plus connnu soit GitHub un grand nombre d'alternatives existent. GitLab, Bitbucket, SourceForge, ... Si tu possèdes un serveur il est même possible d'héberger facilement le tien avec la commande git uniquement.

![repo overview](./images/repo-overview.png)

> ###### sources : [Introduction à GIT](https://perso.liris.cnrs.fr/pierre-antoine.champin/enseignement/intro-git/#vue-d-ensemble)

## `git add`

`git add` permet d'ajouter les fichiers et dossiers spécifiés à l'index.  
Cette commande agit récursivement ce qui permet d'ajouter tous les fichiers et dossier présent dans un dossier sécifié.

Example :

```sh
git add . # Ajoute le dossier actuel et tous ses fichiers/sous-dossiers récursivement

git add file1 file2 dir1/file3 # Ajoute les fichiers sélectionner
```

> [!NOTE]  
> #### ``.gitignore``
> Le ``.gitignore`` permet de spécifier des fichiers/dossiers à ne pas ajouter automatiquement à l'index avec [`git add`](#git-add).  
> Il peut y en avoir plusieurs dans différents dossiers d'un repo et ils agiront tous sur leur dossier et tous ses sous-dossiers.


## commande/utilisation poussée (branching)

### branching, plusieurs strategie de fusion, resolution de conflits, checkout un fichier, upstream (kporceil)


#### C’est quoi une branche ?

Une **branche** Git, c’est une **ligne de développement parallèle**.  
Chaque branche représente une version différente du projet, avec son propre historique de commits.

> 💬 En gros : une branche = une série de modifications indépendantes.

---

#### À quoi ça sert ?

- **Tester** : Pratique pour essayer une nouvelle fonctionnalité sans impacter la version principale.  
- **Travailler à plusieurs** : chaque contributeur peut avancer sur sa branche, puis fusionner le résultat.  
- **Organiser ton code** : par exemple :
  - `main` ou `master` → version stable  
  - `dev` → développement en cours  
  - `feature/xxx` → une fonctionnalité
  - `fix/xxx` → une correction de bug

---

####  Les commandes de base

```bash
# Voir les branches existantes
git branch

# Créer une nouvelle branche
git branch nom-de-branche

# Changer de branche
git switch nom-de-branche

# Créer et passer directement sur une nouvelle branche
git switch -c nom-de-branche

# Fusionner une branche dans la branche actuelle
git merge nom-de-branche

# Supprimer une branche devenue inutile
git branch -d nom-de-branche
```

####  Fusionner des branches

#####  Le but du merge

Quand une branche est finis (plus rien a faire dessus) (ex : `feature/xx`), il faut **intégrer la nouvelle branche** dans la branche principale.
Pour ça, il existe deux approches principales : **merge** et **rebase**.

---

###### `git merge` — la fusion classique

`merge` combine l’historique de deux branches **sans le réécrire**.  
C’est la méthode la plus sûre et la plus utilisée.

```bash
git switch main
git merge feature/ajout-login
```

Git crée alors un **commit de merge** qui relie les deux branches.  
l’historique exact des commits est conservé.

###### ✅ Avantages
- Historique fidèle : rien n’est modifié.  
- Facile à comprendre, surtout en équipe.  
- Sécurisé : aucun commit n’est réécrit.

###### ⚠️ Inconvénients
- L’historique peut devenir “brouillon” (avec des branches et commits entrecroisés).

---

##### `git rebase` — la réécriture

`rebase` réapplique les commits d’une branche **au-dessus** d’une autre, comme si le travail avait commencé plus tard.

```bash
git switch feature/ajout-login
git rebase main
```

Cela **réécrit l’historique** pour donner une ligne de commits plus propre et linéaire.

###### ✅ Avantages
- Historique propre et linéaire.  
- Idéal avant de fusionner une branche de fonctionnalité.

###### ⚠️ Inconvénients
- Réécrit l’historique → dangereux sur des branches partagées !
- Nécessite de comprendre ce qu’on fait.

> 💡 **Warning: **  
> Le `rebase` peux poser des problemes sur les branches deja partagée avec d'autres contributeurs 
> À moins d'être sur de ce que l'on fait, il vaut mieux utiliser `merge`

---

##### Les conflits

Quand deux branches modifient **les mêmes lignes d’un fichier**, Git ne peut pas deviner quelle version garder : c’est un **conflit**. et c'est tout a fait normal.

Git fais alors savoir qu'il y a un conflit

```bash
CONFLICT (content): Merge conflict in main.c
```

Le fichier concerné contient alors des marqueurs :

```diff
<<<<<<< HEAD
printf("Bonjour\n");
=======
printf("Hello\n");
>>>>>>> feature/anglais
```

les indicateurs sont les suivants: `<<` represente la partie de la difference qui represente la branche actuelle, tandis que `>>` represente les changements de la branche en train d'etre merge. Les deux sont separé par une ligne de `=`.
il faut alors modifier le fichier, en choisissant la partie du code qu'on veux garder (ou les deux si besoin), et supprimer les indicateurs de conflit.

il suffit maintenant de faire un commit de resolution de conflit.

```bash
# Une fois le fichier corrigé
git add main.c
git commit   # pour terminer le merge
```

> 🔧 les éditeurs modernes (VS Code, etc.) proposent une interface visuelle pour résoudre les conflits facilement, il est tout de meme primordiale de savoir les régler manuellement.

---

###### En résumé

| Stratégie | Résumé | Avantages | Inconvénients |
|--------|------------------|------------|----------------|
| **Merge** | Fusionne les branches avec un commit de merge | Simple, sûr, collaboratif | Historique plus complexe |
| **Rebase** | Réécrit les commits sur une autre base | Historique propre et linéaire | Risque si mal utilisé |

##### Annuler des changements:

###### Recuperer une ancienne version d'un fichier

il arrive que l'on veuille recuperer une version plus ancienne d'un fichier, la version que l'on cherche est dans un commit antérieur. Il suffit alors de localiser le commit, copier son hash. puis d'utiliser la commande suivante:

```bash
git checkout [hash] [path/to/file]
```

le fichier sera alors remplacé par son ancienne version.

###### Annuler des changements et retourner a un ancien commit.

il arrive des fois ou les derniers changements ne sont finalement pas bon, et nous voulons reprendre a partir d'un commit antérieur.

####### `git revert`

`git revert` **annule un commit en créant un nouveau commit inverse**.  
L’historique reste intact — pratique pour corriger sans casser.

```bash
git revert <hash_du_commit>
```

✅ Avantages :
- Sécurisé (aucune perte d’historique)
- Idéal pour les repo partagés

⚠️ Inconvénient :
- L’historique garde une trace du commit annulé

---

####### `git reset`

`git reset` **remonte le temps** en déplaçant le pointeur `HEAD` à un commit précédent.  

```bash
# Déplace HEAD, garde les fichiers
git reset --soft <id>

# Supprime aussi les changements du staging
git reset --mixed <id>

# Efface tout (⚠️ dangereux)
git reset --hard <id>
```

✅ Avantages :
- Permet de revenir en arrière proprement  
- Utile pour corriger des commits locaux

⚠️ Inconvénients :
- Peut **supprimer définitivement** des changements
- À éviter sur une branche partagée

---

💡 **En résumé :**
- `revert` → crée un nouveau commit correctif (sécurisé)  
- `reset` → efface ou remonte l’historique (puissant mais risqué)

---

ON MONTRE LEARN GIT BRANCHING

### a voir submodule et autres (jweber)

### Fonctionnement interne de git sur certains trucs (fonctionnement parent enfant des commits, HEAD, indexing, ...) (a voir)
