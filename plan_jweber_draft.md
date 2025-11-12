# atelier git



## Introduction

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
- Optimisation de la mémoire (avec un système qui enregistre les différences entre fichiers plutôt que le fichier à chaque état du projet)
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




### Historique (d'où vient git) : 

Les différentes générations de système de control de version:

|Generation|Networking|Operations|Concurrency|Examples|
|----------|----------|----------|-----------|--------|
|1ère|Aucun|Un fichier à la fois|Locks|SCCS, RCS|
|2ème|Centralisé|Plusieurs fichiers|Merge avant de commit|CVS, SourceSafe, Subversion|
|3ème|Décentralisé|Changeset|Commit avant de Merge|Bazaar, git, Mercurial, BitKeeper|

source : https://ericsink.com/vcbe/html/history_of_version_control.html

#### 1ere generation de système de control de version : 

- en 1972 SCCS (Source Code Control System) : le premier système de controle de version, il apporte les notions de :
    - système de lock pour pouvoir modifier un fichier
    - enregistrement de changements incremental
    - gérer plusieurs versions

- en 1982 RCS (Revison Control System), un SCCS amélioré:
    - des branches 
    - possibilité de unlock un fichier

#### 2eme génération de système de control de version :

- en 1985 CVS (concurrent version system) : à la base un script qui sert de front-end à RCS
    - architecture client-server : le serveur contient le repo, et le client parle à ce serveur pour avoir accès au code, modifier le code, et pleins d'autres opérations.

- en 2001 SVN (Apache subversion) : une refonte de CVS pour palier à ses défaults et ajouts de fonctionnalités manquantes à CVS

#### 3eme generation de systeme de control de version : 

- en 1998, le projet Linux commence à être vraiment gros, et jusque là, le système de control de version, c'est juste Linus Torvald. Qui par la même occasion déteste CVS et prefére ne rien utiliser que d'utiliser CVS. 

- Toujours en 1998, un mec (Larry McVoy) propose son idée d'outil de controle de version décentralisé à Linus. Il lui dit c'est cool j'aime l'idée.

- en 2000 : Ce même mec (Larry McVoy) sort alors BitKeeper en 2000.

- en 2002 : BitKeeper est adopté pour le gestion de contrôle du noyau linux. Mais c'est un logiciel propriétaire certains termes de la license sont très restrictif :
    - Interdit de reverse-engineer quoi que ce soit lié à BitKeeper
    - Interdiction de participer au développement d'un outil concurrent à BitKeeper.

L'adoption de BitKeeper fait beaucoup débat dans la communauté linux.

- en 2005 : ça fini par exploser et Larry McVoy retire la license pour utiliser BitKeeper pour gérer le noyau linux pour différentes raisons.
    
Il faut rapidement une alternative a BitKeeper pour permettre la suite du développement du noyau, les alternatives existantes à l'époque sont essentiellement:
- monotone
- DARCS

Mais les alternatives sont trop inéfficientes.

- en (avril) 2005 : Linus décide d'écrire son propre logiciel de gestion de version et il sort git. Le 16 juin 2005, la version 2.6.12 du noyau est gérer avec git.

Note : c'est apparement pas du tout le linux qu'on connais aujourd'hui et c'était vraiment dur à prendre en main et c'était développer vraiment pour les besoins de Linus et l'intégration du développement du noyau.

- en 2007 : après pas mal de modification, git est prêt à être utilisé pour gérer d'autre logiciel que le noyau linux.

[ICI] insérer graph de l'evolution 'git' versus 'svn' pour la gestion de projet

![test](images/git_vs_svn.png)

### Alternatives :

- Donc aujourd'hui : pour le version control, la majorité utilise git, avec leur répertoire sur github, mais il existe des alternative :

#### Alternative a git :

le plus populaire et je dirais le seul viable et maintenu à ce jour ? :
- Mercurial 

[ICI] mettre le graph de git survey pour savoir ce que les gens utilisaient à l'époque

ça virer ?(dessous)

d'autres moins populaire (je ne sais pas si c'est encore utilisé aujourd'hui, renseignez vous si ça vous chante):
- GNU arch
- Monotone
- Darcs
- Pijul
- Apache Subversion

#### Alternative à GitHub :

- SourceForge
- Bitbucket
- GitLab
- Gitea


### sources :

- https://en.wikipedia.org/wiki/Git
- https://en.wikipedia.org/wiki/Version_control
- https://en.wikipedia.org/wiki/Distributed_version_control
- https://graphite.com/blog/bitkeeper-linux-story-of-git-creation
- https://www.youtube.com/watch?v=W3hr-F8ie94
- https://ericsink.com/vcbe/html/history_of_version_control.html
- https://archive.kernel.org/oldwiki/git.wiki.kernel.org/index.php/GitSurvey2007.html (graphic sur qui utilise quel VCS)

### a voir submodule et autres (jweber)
