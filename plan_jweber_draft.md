
# atelier git

## Glossaire 

different termes pour dire for "version control system":
- VCS : Version Control Software / Version Control System
- SCM : Source Control Management / Software Configuration Management
- Revision Control
- CVS : Concurrent Version system

- SCCS : Source Code Control System

## introduction pourquoi git ? historique rapide. (jweber)

### qu'est ce que git en résumé : 

- un logiciel de control de version

A la base, l'objectif d'un système de control de version :
    - economiser de la place.
    - pouvoir gérer les versions.
    - avoir une trace de qui à changer quoi et quand.
    - savoir quel version du logiciel le client a sur son pc.

- c'est un logiciel libre et open-source (free and open-source software (FOSS), au contraire de propriétaire) de control/gestion de version decentralisé (distributed version control software)
    - décentralisé : le répertoire entier, incluant le code source et l'historique, est copié localement sur l'ordinateur de chaque developper travaillant sur le projet.
    NOTE : il existe quand même un serveur général où tout le monde va partager ses modifications et récupérer les modifications des autres (ex: Mercurial, GitLab, SourceForge, Bitbucket, Github)
    - centralisé : pas de copie sur l'ordinateur local, il faut se connecter à un serveur pour pouvoir travailler sur le projet.
- Donc pas de version centrale du code source, chaque developpeur à sa copie local du répertoire avec ses potentiels changements.
- souvent utilisé pour gérer le code source d'un programme.


Exemple d'avantages d'un système décentralisé :
    - possibilité de travailler hors-ligne
    - les copies local du répertoires sont aussi des backups : il n'y a pas un seul endroit ou se situe le code source.

Exemples de désavantages d'un système décentralisé :
    - Peu prendre beaucoup de place, vu que chaque personne fait une copie entière du répertoire. (-> à vérifier, mais : un studio de jeu AAA n'utilisera jamais git car pas adapté pour gérer tous les assets, mais plus quelque chose comme Perforce)
    - Un code plus facilement exposé, vu qu'il est présent sur plein de machine.

#### En gros :

- c'est pas mal pour avoir un historique de ce qui s'est passé dans notre code, sans avoir à créer un dossier libft_V1, libft_V2, libft_Vfinale, libft_Vfinale_2, libft_Vfinal_final,
- donc ça garde l'historique de modifications. C'est intelligent pour ne garder que les différences entre chaques versions (optimisation de la mémoire)
- ça permet de travailler facilement en groupe, ou chacun à accès au code et peu le modifier de son côté.

### Un peu d'histoire : 

premier systeme de control de version :
- SCCS : Source Code Control System

- Sur les 10 premières année du developpement du noyau linux (1990 à 1998), le système de control de version c'etait : Linux lui même.
- Critique de Linus sur les CVS (Concurrent Version Systems)
- Puis vers 1998 : BitKeeper est venu avec son idée d'une 'distributed source management system'.
- Vers 2002 : Changement de BitKeeper vers un outils interne.
- A la base, créé par Linus Torvald pour le version control du developpement du noyau linux. Le développement de git à commencé en 2005.
- Au début, le développement du noyau linux reposait sur BitKeeper pour son gestionnaire de version. Mais c'était un logiciel propriétaire, donc Linux à décidé de créer le sien, pour avoir un systeme de versionning libre.
- 

### Alternatives :

- Donc aujourd'hui : pour le version control, la majorité utilise git, avec leur répertoire sur github, mais il existe des alternative :

#### Alternative a git :

le plus populaire :
- Mercurial 

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

### LISEZ LES MESSAGES D'ERREUR GIT TOUT EST ECRIT (c'est pas parce que c'est rouge que ton pc va exploser si tu lis)

### config son git (kporceil)

## commande/utilisation basique

### add, status, commit, push, pull, remote, diff, log (jweber)

## commande/utilisation poussée (branching)

### branching, plusieurs strategie de fusion, resolution de conflits, checkout un fichier, upstream (kporceil)

ON MONTRE LEARN GIT BRANCHING

### a voir submodule et autres (jweber)

### Fonctionnement interne de git sur certains trucs (fonctionnement parent enfant des commits, HEAD, indexing, ...) (a voir)

# sources :

- https://en.wikipedia.org/wiki/Git
- https://en.wikipedia.org/wiki/Version_control
- https://en.wikipedia.org/wiki/Linux_kernel
- https://en.wikipedia.org/wiki/Distributed_version_control
- https://en.wikipedia.org/wiki/Perforce
- https://www.reddit.com/r/devops/comments/xwnpze/better_git_alternative/
- https://www.reddit.com/r/git/comments/q5qow9/best_github_opensource_alternative/
- https://www.reddit.com/r/opensource/comments/1gx5wri/suggestions_on_a_github_alternative/
- https://graphite.com/blog/bitkeeper-linux-story-of-git-creation
- https://www.youtube.com/watch?v=W3hr-F8ie94
