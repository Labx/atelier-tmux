# Atelier CLI, utilisation de `Tmux`

### Table des matières

- [Préambule](#préambule)
- [Objectifs](#objectifs)
    - [Scénario](#scénario)
- [Installation](#installation)
- [Configuration](#configuration)
    - [Création du serveur `Tmux`](#création-du-serveur-tmux)
    - [Se connecter au serveur en `SSH`](#se-connecter-au-serveur-en-ssh)
    - [Lister les sessions](#lister-les-sessions)
    - [S'attacher à une session existante](#sattacher-à-une-session-existante)
    - [Lister les utilisateurs connectés](#lister-les-utilisateurs-connectés)
- [Todo](#todo)

## Préambule

> Ce document s'adresse aux participants des [ateliers CLI organisés au LabX](https://www.labx.fr/) (_hackerspace_ de Bordeaux) à un publique **débutant**.
> 
> Il est évident que certains concepts sont simplifiés pour s'adapter au public. 

Si toutefois vous trouvez des erreurs, merci de les signaler à l'auteur via : 

* Mail : [dev+clilabx@edouard-lopez.com](dev+clilabx@edouard-lopez.com) ;
* Twitter : [@edouard_lopez](https://twitter.com/edouard_lopez) ;
* IRC : #giroll ou #labx ;
* en venant discuter à [Giroll](http://giroll.org/), au [LabX](www.labx.fr/), au [Node](http://bxno.de/) ou autres.

## Objectifs

L'objectif de l'atelier et d'être capable d'utiliser `tmux` lors des prochains ateliers pour partager un _shell_ commun lors des démos.

### Scénario

Pour le moment tous les participants se connecte à la machine hôte en SSH, avec les même identifiants, et s'attachent à une session `tmux` existante. 

Cela soulève des questions de **sécurité** que nous avons résolue par la **création d'un utilisateur dédié** aux ateliers.

## Installation

Chercher dans votre gestionnaire de paquets `tmux`. 

Vous aurez également besoin d'installer un client `ssh`.

## Configuration

Un membre du groupe commence par créer un nouveau compte utilisateur, p. ex. `labx` sur sa machine. Par la suite, tout le monde se connectera sur ce compte via `ssh`.

### Création du serveur `Tmux`

Pour créer le serveur `tmux`, la personne dont la machine servira d’hôtes devra saisir la commande suivante [^](http://explainshell.com/explain?cmd=tmux new-session -s labx) :

        tmux new-session -s labx 

### Se connecter au serveur en `SSH`

Les autres membres vont se connecter avec la commande suivante :

        ssh labx@192.168.0.4 

### Lister les sessions 

Une fois connecté à la machine hôte, il est possible de lister les sessions _tmux_ active avec la commande [^](http://explainshell.com/explain?cmd=tmux list-sessions) :

        tmux list-sessions
        # ou
        tmux ls

Les sessions d'un utilisateur peuvent être lister avec la commande `tmux ls` uniquement depuis cet utilisateur. Il est par contre possible de voir les processus correspondant à chaque sessions avec la commande [^](http://explainshell.com/explain?cmd=ps aux | grep tmux) :

        ps aux | grep tmux

Mais il n'est pas possible de se connecter aux sessions d'un autres utilisateurs.

### S'attacher à une session existante

Aprés avoir trouver la session à laquelle on souhaite se rattacher (ici _labx_), on se connecte avec la commande suivante [^](http://explainshell.com/explain?cmd=tmux attach-session -t labx) :

        tmux attach-session -t labx
        # ou 
        tmux attach -t labx

Il est possible de créer une connexion restreindre en lecture seule avec l'option `-r` (i.e. _read-only_) : 

        tmux attach -r -t labx

Ce qui est dommage c'est que c'est le client lui même qui spécifie cette configuration.

### Lister les utilisateurs connectés

Il est possible de les clients connectés à un serveur avec la commande [^](http://explainshell.com/explain?cmd=tmux list-clients): 

        tmux list-clients
        # ou
        tmux lsc

La commande peut prendre une option `-t ma-session` pour restreindre la liste des clients à une sessions particulière [^](http://explainshell.com/explain?cmd=tmux list-clients -t labx):

        tmux lsc -t labx

## Todo

* tmux et ssh
* restriction des droits client (cf. `readonly`)
* `tmux show-environment -g`
* tmux multi-utilisateurs ?