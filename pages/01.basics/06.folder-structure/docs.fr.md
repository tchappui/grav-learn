---
title: Structure Des Répertoires
taxonomy:
    category: docs
---

Grav étant un **CMS basé sur les fichiers**, ce qui signifie qu'aucune base de données n'est utilisée pour son fonctionnement, donne à la structure des dossiers de votre site une importance particulière. A la **racine** de votre installation Grav, la structure des répertoires ressemble à: 

```bash
/assets
/bin
/cache
/images
/logs
/system
/user
/vendor
```

Ainsi, approfondissons un peu chacun de ces dossiers à la racine du projet et expliquons à quoi ils servent:

### /assets

**(v0.9.0+)** Le dossier `assets` est utilisé par le nouveau système de gestion des assets de Grav pour stocker les fichiers `.css` et `.js` de Grav.

!! Ce dossier ne doit pas être utilisé pour stocker des données utilisateur, car il est vidé de manière régulière de toutes ses données. 

### /bin

Le dossier `bin` conteint [l'application en ligne de commande (CLI) de Grav](../../advanced/grav-cli) pouvant être utilisée pour effectuer des tâches pratiques à partir de la ligne de commande. Il s'agit d'une fonctionnalité relativement avancée destinée principalement aux développeurs. Nous allons donc réserver cette question pour une discussion ultérieure. 

### /cache

Le dossier `cache` est utilisé pour stocker les fichiers temporaires du cache qui sont générés automatiquement par Grav afin d'améliorer les performances. Par défaut, Grav gère automatiquement la mise en cache, en sélectionnant la meilleure option disponible pour votre environnement d'hébergement afin de vous assurer que votre site fonctionne aussi vite que possible. 

Si Grav décide que le **système de fichiers** est la meilleure méthode de mise en cache, les fichiers de cache qu'il génrérera seront stockés ici. Le moteur de templates Twig utilise également cet emplacement pour stocker ses fichiers de gabari précompilés. Encore une fois, cette phase de mise en cache est faite pour s'assurer que Grav s'exécute à sa vitesse optimale. 

!! Ce dossier ne doit pas être utilisé pour stocker des données utilisateur, car il est vidé de toutes ses données sur une base régulière. 

### /images

Grav est livré avec une [bibliothèque de manipulation d'images](../../content/media) puissante et facile à utiliser. Cela signifie que vous pouvez facilement redimensionner une image à la volée à partir de votre contenu ou même d'un plugin. Ces images sont stockées dans le dossier `images` pour pouvoir être réutilisées si une même image de même taille est demandée à nouveau. 

Ce dossier agit comme un cache d'image et est destiné aux fichiers générés automatiquement. Les media fournis par l'utilisateur doivent être stockés dans le répertoire `user/pages/`, `user/themes/` ou même dans un dossier `user/images/` personnalisé.

!! Ce dossier ne doit pas être utilisé pour stocker des données utilisateur, car il est vidé de toutes ses données sur une base régulière. 

### /logs

Lorsque Grav détecte une erreur, ou si vous avez activé une journalisation ou un profilage supplémentaire, il stocke les fichiers de journalisation pertinents dans le dossier `logs`.

### /system

Le dossier `system` est l'endroit où les fichiers qui font tourner Grav fonctionnent réellement. Vous ne devez rien modifier dans ce dossier, car une mise à jour de Grav pourrait écraser vos modifications. Si vous devez modifier quelque chose lié au fonctionnement de Grav, vous pouvez utiliser des plugins comme indiqué dans les chapitres suivants. 

### /vendor

Le dossier `vendor` contient des bibliothèques importantes sur lesquelles s'appuie Grav. Ce dossier est similaire au dossier `system` dans le sens que son contenu ne doit pas etre modifié, sauf si vous êtes absolument certain de ce que vous faites. 

**(v0.9.2+)**  Si vous avez [installé](../installation) Grav depuis GitHub, le dossier `vendor` n'aura pas été installé. Pour créer et remplir le dossier vendor, vous devez exécuter `bin/grav install` ou `composer install` depuis la racine de votre instance de Grav. Plus de détails peuvent être trouvés dans la section [installation](../installation).

### /user

C'est le dossier le plus important pour la majorité des utilisateurs de Grav. Ce dossier est l'endroit où vous passerez votre temps à créer du contenu, à utiliser des plugins et à éditer vos thèmes. Laissez-nous creuser un peu plus loin dans ce dossier:

```bash
/user/accounts
/user/config
/user/data
/user/pages
/user/plugins
/user/themes
```

### /user/accounts

Le répertoire `accounts` est l'endroit où vous définissez les comptes utilisateur si des restrictions d'accès sont requises pour certaines parties de votre site. 

### /user/config

Les [fichiers dans le répertoire config](../grav-configuration) sont utilisés pour configurer le site web et ont été discutés dans le chapitre précédent. 

### /user/data

Le dossier `data` peut être utilisé par les plugins pour stocker des données que vous pourrez référencer plus tard. Un bon exemple de plugin qui utilise ce dossier est le plugin **Forms** qui peut prendre un formulaire web et stocker les données soumises dans un fichier texte de ce dossier. Vous pouvez également stocker d'autres éléments tels que des téléversements d'utilisateurs ou tout ce que vous souhaitez.

!! Ce répertoire n'est pas accessible depuis le navigateur web par défaut. 

### /user/pages

C'est le coeur de Grav. Le dossier `pages` est l'endroit où vous créez et éditez votre contenu. Nous irons bbeaucoup plus en profondeur dans la [section suivante](../../content).

### /user/plugins

Un plugin peut étendre le noyau de Grav avec des fonctionnalités particulières dont vous pourriez avoir besoin pour votre site web. Les plugins peuvent être téléchargés à partir de [GetGrav.org/downloads/plugins](https://getgrav.org/downloads/plugins), ou vous pouvez [développer le votre](../../plugins/plugin-tutorial).

### /user/themes

Un thème transforme votre contenu en un véritable site web. Il convertit le contenu que vous avez construit en code HTML qu'un navigateur pourra comprendre et afficher à votre public. Il existe un thème de base fourni avec Grav, mais vous pouvez également en télécharger d’autres à partir de [GetGrav.org/downloads/themes](https://getgrav.org/downloads/themes) ou même créer le vôtre. La section [Thèmes](../../themes) expliquera cela avec plus de détails.
