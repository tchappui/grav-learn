---
title: Installation
taxonomy:
    category: docs
---

L'installation de Grav est un processus trivial. En fait, il n'y a pas réellement d'installation. Vous avez **trois** otpions pour installer Grav. La première, et la plus simple, consiste à télécharger l'archive **zip** et à l'extraire. La deuxième méthode consiste à l'installer à l'aide de **Composer**. La troisième méthode consiste à cloner le projet directement à partir de **Github**, puis à exécuter une commande de script incluse pour installer les dépendances nécessaires:

## Vérifiez la Version de PHP

Grav est incroyablement facile à configurer et à utiliser. Assurez-vous d'avoir au moins la version 5.5.9 de PHP en exécutant la commande suivante depuis un terminal:

```bash
$ php -v
```

Cela devrait afficher la version et les informations de compilation. Par exemple:

```bash
PHP 5.5.20 (cli) (built: Jan 19 2014 21:32:15)
Copyright (c) 1997-2013 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2013 Zend Technologies
```

## Option 1: Installation à Partir d'une Archive Zip

Le moyen le plus simple d'installer Grav est de télécharger l'archive ZIP et de l'extraire:

1. Téléchargez la dernière et meilleure version de **[Grav](https://getgrav.org/download/core/grav/latest)** ou de **[Grav + Admin](https://getgrav.org/download/core/grav-admin/latest)**.
2. Extraire le fichier ZIP dans le répertoire [racine](https://www.wordnik.com/words/webroot) de votre serveur web, p.ex. `~/webroot/grav`

!!! Il existe des [exemples de structure (skeleton)](https://getgrav.org/downloads/skeletons) disponibles, qui incluent le système Grav principal, des exemples de pages, des plug-ins et une configuration. Ils sont un excellent moyen de commencer. Tout ce que vous avez à faire est de [télécharger l'archive de l'exemple de structure](https://getgrav.org/downloads/skeletons) que vous préférez et de suivre les étapes ci-dessus.

!!!! Si vous avez téléchargé le fichier ZIP, puis que vous envisagez de le déplacer à la racine de votre serveur web, déplacez le REPERTOIRE ENTIER, car il contient plusieurs fichiers cachés (tels que .htaccess) qui ne seront pas sélectionnées par défaut. L'omission de ces fichiers cachés peut entrainer des problèmes lors de l'exécution de Grav.


## Option 2: Installation à l'aide de Composer

La méthode alternative est d'installer Grav à l'aide de [composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx):

```
$ composer create-project getgrav/grav ~/webroot/grav
```

Si vous souhaitez consulter la version dernier cri de Grav, ajouter `1.x-dev` en tant que paramètre supplémentaire:

```
$ composer create-project getgrav/grav ~/webroot/grav 1.x-dev
```

## Option 3: Installer à partir de Github

Une autre méthode consiste à cloner Grav du dépôt Github, puis à exécuter un script d'installation de dépendances simple:

1. Cloner the déplôt Grav à partir de [GitHub](https://github.com/getgrav/grav) vers un répertoire à la racine web de votre serveur, p.ex. `~/webroot/grav`. Démarrer un **terminal** ou une console **console** et naviguer jusqu'au répertoire webroot:
   ```
   $ cd ~/webroot
   $ git clone -b master https://github.com/getgrav/grav.git
   ```

2. Installer les **dépendances externes** à l'aide de [composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx):
   ```
   $ cd ~/webroot/grav
   $ composer install --no-dev -o
   ```

3. Installer les **dépendances des plugins** et des **thèmes** en utilisant [l'application Grav en ligne de commande](../../advanced/grav-cli) `bin/grav`:
   ```
   $ cd ~/webroot/grav
   $ bin/grav install
   ```

   Cela **clonera** automatiquement les dpéendances requises directement depuis Github vers cette installation Grav. 

## Serveur web

#### Apache/IIS/Nginx

Utiliser Grav avec un serveur Web tel qu'Apèache, IIS ou Nginx est aussi simple que d'extraire Grav dans un dossier situé à la [racine web](https://www.wordnik.com/words/webroot). Tout ce dont il a besoin pour fonctionner est PHP 5.5.9 ou plus récent. Vous devez donc vous assurer que votre hébergement répond à cette exigence. Pour plus d'informations sur les conditions requises pour le fonctionnement de Grav, consultez le chapitre [exigences techniques](../requirements) de ce guide.

Si votre racine web est, par exemple, `~/public_html`, vous pouvez l'extraire dans ce dossier et l'atteindre via `http://localhost`. Si vous l'avez extrait dans `~/public_html/grav` vous pourrez l'atteindre via `http://localhost/grav`.

!!! Chapque serveur web doit être configuré. Grav est livré avecun .htaccess par défaut pour Apache, et vient avec quelques [fichiers de configuration par défaut](https://github.com/getgrav/grav/tree/master/webserver-configs), pour `nginx`, `caddy server`, `iis`, et `lighttpd`. Utilisez-les en fonction de vos besoins.

#### Lancer Grav avec le serveur web intégré à PHP avec `router.php`

Vous pouvez exécuter Grav à l'aide d'une simple commande depuis le terminal / l'invite de commande, à l'aide du serveur web intégré à PHP et disponible sur tout système doté de PHP 5.5+. Tout ce dont vous avez besoin est de naviguer jusqu'à la racine de votre installation Grav à l'aide du terminal, puis d'entrer `php -S localhost:8000 system/router.php`. Vous pouvez remplacer le numéro du port (dans notre exemple, il s'agit du port `8000`) par le port de votre choix.

En exécutant cette commande, vous obbtiendrez un résultats similaire à celui-ci:

```bash
$ php -S localhost:8000 system/router.php
PHP 7.0.14 Development Server started at Thu Jan 26 17:19:50 2017
Listening on http://localhost:8000
Document root is /Users/example/sites/grav/
Press Ctrl-C to quit.
```

Votre terminal vous informera en temps réel de toute mise à jour ou activité sur ce serveur. Vous pouvez copier l'URL fournie dans le ligne `Listening on` et la coller dans le navigateur web de votre choix pour accéder à votre site, y compris pour accéder à l'interface d'administration. 

!!!! Ce serveur de développement est un outils utile pour les développement rapides, et il **ne** devrait pas être utilisé à la place d'une serveur web dédié à la production, tel que Apache. 

## Installation réussie

Lors du premier chargement, Grav pré-compile certains fichiers. Si vous actualisez maintenant votre navigateur, vous obtiendrez une version plus rapide et mise en cache. 

![Grav Installed](install.png?cropResize=600,600)  {.border}

!! Dans les exemples précédent, **$** représente l'invite de commander. Ca peut être différent sur différentes plates-formes. 

Par défaut, Grav est livré avec des pages exemple pour vous donner des informations utiles. Votre site est déjà entièrement fonctionnel et vous pouvez le configurer, ajouter du contenu, le développer ou le personnaliser autant que vous le souhaitez. 

## Problèmes D'Installation Et De Configuration

Si des problèmes sont découverts lors du chargement initial de la page (ou après une vidange du cache), une page d'erreur peut s'afficher: 

![Grav with Problems](problems.png?cropResize=600,600)  {.border}

Veuillez consulter la section [Dépannage](../../troubleshooting) pour obtenir de l'aide sur des prolèmes spécifiques.

! Si vous rencontrez des problèmes avec les autorisations de fichiers, veuillez consulter la documentation relative au [dépannage des permissions de fichiers](/troubleshooting/permissions). Vous pouvez également consulter la documentation sur [l'hébergement](/webservers-hosting) qui contient des instructions spécifiques pour différents environnements d'hébergement.

## Mises à jour de Grav

### Mises à jour automatiques

La méthode recommandée pour mettre à jour Grav (à partir de la v0.9.3) consiste à utiliser **le gestionnaire de paquets de Grav (GPM)**. Tout ce que vous avez à faire est de naviguer à la racine de votre site Grav et de taper: 

```
bin/gpm selfupgrade -f
```

Vous trouverez des informations complètes dans Full information can be found in the [documentation de GPM](../../advanced/grav-gpm). GPM est également intégré à notre plugin [de tableau d'administration](../../admin-panel) qui vérifie, signale et installe automatiquement les mises à jour.
