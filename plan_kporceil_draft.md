# atelier git

## introduction

### LISEZ LES MESSAGES D'ERREUR GIT TOUT EST ECRIT (c'est pas parce que c'est rouge que ton pc va exploser si tu lis)
### pourquoi git ? historique rapide. (jweber)
### config son git (kporceil)

Git fonctionne avec une configuration pour etablir des logs precis et des strategie par défaut.

`git config --global user.name` permet de set le nom de l'utilisateur git (qui sera affiché dans les logs)
`git config --global user.email` permet de set l'email de l'utilisateur git (qui sera affiché dans les logs)
`git config --global init.defaultBranch` permet d'etablir la branch par defaut lors d'un git init
`git config --global core.editor` permet de choisir quel editeur ouvrir quand il y a un besoin de message (ex: git commit)

## commande/utilisation basique

### add, status, commit, push, pull, remote, diff, log (jweber)

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

Quand une branche est fini (plus rien a faire dessus) (ex : `feature/xx`), il faut **intégrer la nouvelle branche** dans la branche principale.
Pour ça, il existe deux approches principales : **merge** et **rebase**.

---

###### `git merge` — la fusion classique

`merge` combine l’historique de deux branches **sans le réécrire**.  
C’est la méthode la plus sûre et la plus utilisée.

```bash
git switch main
git merge feature/add-login
```

Git crée alors un **commit de merge** qui relie les deux branches.  
L’historique exact des commits est conservé.

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
Il faut alors modifier le fichier, en choisissant la partie du code qu'on veux garder (ou les deux si besoin), et supprimer les indicateurs de conflit.

Il suffit maintenant de faire un commit de resolution de conflit.

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
git checkout [hash] -- [path/to/file]
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
