---
layout: post
title: Installer un serveur GIT avec LinuxDeploy Debian
tags: [blog, android, serveur, git]
---

Après avoir installer LinuxDeploy sur son téléphone android comme vu dans le precedent [billet]({{ site.url }}/2015-04-05-Transformer-son-telephone-android-en-miniserver/),
nous allons installer git et le configurer pour héberger nos développement. Dans cette exemple deux utilisateurs seront créer git et gitadmin.
Git est l'utilisateur standard, pour utiliser les dépôts. Gitadmin permet d'administrer les dépôts.

## Installation

    sudo aptitude install git

### Ajout des utilisateurs et groupe

    sudo groupadd gitusers
    sudo useradd -g gitusers -s /usr/bin/git-shell git
    sudo useradd -g gitusers -s /usr/bin/git-shell gitadmin
    sudo mkdir /opt/git/
    sudo chown gitadmin:gitusers /opt/git/

### git-shell-command

Pour sécuriser le shell les utilisateurs git et gitadmin utilise git-shell.
Ce shell permet de limiter les actions à celle définis dans le répertoire git-shell-commands.
Dans cette exemple les commande disponible permettent d'ajouter des clef ssh, de créer un repository de lister les repository existant.

    sudo git clone https://gist.github.com/fad3b78b359153bd36c9.git /opt/git/git-shell-commands
    sudo chown -R gitadmin:gitusers /opt/git/git-shell-commands/
    sudo chmod -R +x /opt/git/git-shell-commands
    sudo ln -s /opt/git/git-shell-commands /home/git/git-shell-commands
    sudo ln -s /opt/git/git-shell-commands /home/gitadmin/git-shell-commands

## Fichiers git-shell

{% gist fad3b78b359153bd36c9 %}
