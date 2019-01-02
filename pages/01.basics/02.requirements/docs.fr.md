---
title: Exigences Techniques
taxonomy:
    category: docs
---

Grav est conçu intentionnellement avec un nombre d'exigences technique limité. Vous pouvez facilement exécuter Grav sur votre ordinateur local, ainsi que chez 99% des fournisseurs d’hébergement web. Si vous avez un stylo à portée de main, notez les exigences suivantes pour la plateforme Grav:

1. Server HTTP (Apache, Nginx, LiteSpeed, Lightly, IIS, etc.)
2. PHP 5.6.3 ou plus récent
3. hmm... c'est vraiment tout, (mais regarder également les exigences techniques de php pour une expérience d'installation plus en douceur)!

Grav est construit en utilisant des fichiers textes brut pour votre contenu. Aucune base de données n'est nécessaire.

!! Un cache PHP tel que APC, APCu, XCache, Memcached, ou Redis est vivement recommandé pour des performances optimales. Ne vous inquiétez pas cependant, ils font généralement déjà partie de votre forfait d'hébergement.

## Serveurs HTTP

Grav est si simple et polyvalent que vous n’avez même pas besoin d’un serveur web pour l’exécuter. Vous pouvez l'exécuter directement à partir du serveur de développement intégré à PHP et du fichier system/router.php, tant que vous utilisez PHP 5.6.3 ou une version ultérieure.

C'est un moyen facile de vérifier une installation Grav et d'effectuer de bref développements, mais ce n'est **pas** recommandé pour un site en production ou même pour des tâches de développement avancées. Nous avons expliqué comment exécuter Grav avec le serveur de développement PHP dans notre [Guide d'installation](../installation#running-grav-with-the-built-in-php-webserver-using-routerphp).

Même si techniquement, vous n'avez pas besoin d'un serveur web autonome, il est préférable d'en utiliser un, même pour le développement local. Il y a beaucoup de bonnes options disponibles:

### Mac

* OS X 10.13 High Sierra est déjà livré avec le serveur web Apache et PHP 7.2. Le travail est donc terminé!
* [MAMP/MAMP Pro](http://mamp.info) est fourni avec Apache, MySQL et bien sûr PHP. C'est un excellent moyen d'obtenir plus de contrôle sur la version de PHP que vous utilisez, la configuration des hôtes virtuels, ainsi que d'autres fonctionnalités utiles telles que la gestion automatique du DNS dynamique.
* [AMPPS](http://www.ampps.com/downloads) est une pile logicielle de Softaculous permettant l'installation de Apache, PHP, Perl, Python, ... Cela inclut tout ce dont vous avez besoin (et plus encore) pour le développement Grav.

### Windows

* [XAMPP](https://www.apachefriends.org/index.html) fournit Apache, PHP et MySQL dans un package simple.
* [EasyPHP](http://www.easyphp.org/) fournit un package d'hébergement web personnel ainsi qu'une version plus puissante pour les développeurs.
* [MAMP pour Windows](http://mamp.info) est favori de longue date sur Mac, mais il est maintenant disponible pour Windows.
* [IIS avec PHP](http://php.iis.net/) est un moyen rapide d'exécuter PHP sur Windows.
* [AMPPS] (http://www.ampps.com/downloads) est une pile logicielle de Softaculous permettant l'installation de Apache, PHP, Perl, Python, ... Cela inclut tout ce dont vous avez besoin (et plus encore) pour le développement Grav.

### Linux

* De nombreuses distributions de Linux sont déjà livrées avec Apache et PHP intégrés. S'ils ne le sont pas, la distribution fournit généralement un gestionnaire de paquets grâce auquel vous pouvez les installer sans souci. Des configurations plus avancées pourront être étudiées avec l'aide d'un bon moteur de recherche.

### Exigences Apache

Même si la plupart des distributions d’Apache contiennent tout ce dont vous avez besoin, voici une liste des modules Apache requis:

* `mod_rewrite`
* `mod_ssl` (si vous désirez utiliser Grav avec SSL)

Vous devez également vous assurer que les options `AllowOverride All` sont définies dans les blocs `<Directory>` et/ou `<VirtualHost>`afin que les fichiers `.htaccess` soient traitées correctement et que les règles de réécriture soient appliquées.

### Exigences IIS

Bien que IIS soit considéré comme un serveur web prêt à fonctionner sans configuration particulière, certaines modifications doivent être apportées.

Pour que **Grav** fonctionne sur un serveur IIS, vous devez installer **URL Rewrite**. Cela peut être accompli à l'aide de **Microsoft Web Platform Installer** à partir de IIS. Vous pouvez également installer URL Rewrite en allant sur [iis.net](https://www.iis.net/downloads/microsoft/url-rewrite).

### Exigences PHP

La plupart des hébergeurs et même des configurations LAMP locales possèdent PHP pré-configuré avec tout ce dont vous avez besoin pour que Grav puisse fonctionner "tout de suite". Cependant, certaines configurations Windows, et même des distributions Linux locales ou sur VPS (je pense particulièrement à toi, Debian!), sont livrées avec une distribution PHP très minimaliste. Par conséquent, vous devrez peut-être installer ou activer les modules PHP suivants:

* `curl` (client utilisé par GPM pour la gestion des URLs)
* `ctype` (utilisé par Symfony/Yaml/Inline)
* `dom` (utilisé par les newsfeeds de grav/admin)
* `gd` (une bibliothèque graphique utilisée pour manipuler des images)
* `json` (utilisé par Symfony/Composer/GPM)
* `mbstring` (support des chaines de caractères mutli-bytes)
* `openssl` (bibliothèque de sockets sécurisées utilisée par GPM)
* `session` (utilisé par toolbox)
* `simplexml` (utilisé par le newsfeed de grav/admin)
* `xml` (support de XML)
* `zip` extension support (utilisé par GPM)

Pour activer le support `openssl` et de (un)pa)zip, vous devez trouver dans le fichier `php.ini`de votre distribution Linux des lignes telles que:

  - `;extension=openssl.so`.
  - `;extension=zip.so`.

et éliminer les point-virgules en début de ligne.

##### Modules Optionnels

* `apcu` pour des performances accrues du cache
* `opcache` pour des performances accrues de PHP
* `xcache` alternative à *apcu*, pas aussi rapide, mais de relativement bonne qualité. 
* `yaml` PECL Yaml fournit un traitement natif de yaml et peut considérablement améliorer les performances.
* `xdebug` utile pour le débogage dans un environnement de développement.

### Permissions

Pour que Grav fonctionne correctement, votre serveur web doit disposer des **autorisations de fichier** appropriées pour écrire des écrire des logs, caches, etc. Lors de l'utilisation de l'interface [CLI](/advanced/grav-cli) (Command Line Interface) ou de [GPM](/advanced/grav-gpm) (Grav Package Manager), l'utilisateur qui exécute PHP à partir de la ligne de commande doit également disposer des autorisations appropriées pour modifier les fichiers.

Par défaut, Grav installera les fichiers et répertoires avec des permissions de `644` et `755`, respectivement. La plupart des fournisseurs d'hébergement ont des configurations garantissant qu'un serveur we exécutant PHP vous permettra de créer et de modifier des fichiers dans votre espace personnel. Cela signifie que Grav fonctionne **sans configuration particulière** chez la grande majorité des fournisseurs d'hébergement.

Toutefois, si vous utilisez un serveur dédié ou même votre environnement local, vous devrez peut-être ajuster les autorisations pour vous assurer que votre **utilisateur** et votre **serveur web** peuvent modifier les fichiers en fonction des besoins. Vous pouvez utiliser plusieurs approches.

1. Dans un **environnement de développement local**, vous pouvez généralement configurer votre serveur web pour s'exécuter sous votre nom d'utilisateur. De cette façon, le serveur web vous permettra toujours de créer et de modifier des fichiers.

2. Modifiez les **autorisations de groupe** sur tous les fichiers et répertoires afin que le groupe du serveur web dispose d'un accès en écriture aux fichiers et dossiers tout en conservant les autorisations standards. Cela demande quelques commandes pour que cela fonctionne.

Commmencez par rechercher l'utilisateur avec lequel Apache s'exécute en exécutant la commande suivante:
```
ps aux | grep -v root | grep apache | cut -d\  -f1 | sort | uniq 
```
Recherchez maintenant le groupe auquel cet utilisateur appartient en exécutant cette commande (remarque: ajustez le USERNAME avec le nom d'utilisateur Apache que vous avez trouvé en exécutant la commande précédente).
```
groups USERNAME
```
(remarque: ajustez `GROUP` pour qu'il soit le groupe sous lequel tourne votre Apache, ce qui a été déterminé à l'aide de la commande précédente. [`www-data`, `apache`, `nobody`, etc.])

```
chgrp -R GROUP .
find . -type f | xargs chmod 664
find ./bin -type f | xargs chmod 775
find . -type d | xargs chmod 775
find . -type d | xargs chmod +s
umask 0002
```

Si vous devez invoquer des autorisations de superutilisateur, exécutez `find … | sudo xargs chmod …` à la place.

## Outils recommandés

### Editeurs de Texte

Bien que vous puissiez vous en sortir avec Notepad, Textedit, Vi ou l'éditeur de texte par défaut fourni avec votre plate-forme, nous vous recommandons d'utiliser un bon éditeur de texte avec mise en évidence de la syntaxe pour faciliter les choses. Voici quelques options recommandées.

1. [SublimeText](http://www.sublimetext.com/) - OS X/Windows/Linux - Un éditeur commercial dédié aux développeurs, mais le prix en vaut la peine. Très puissant en particulier combiné à des plug-ins tels que [Markdown Extended](https://sublime.wbond.net/packages/Markdown%20Extended), [Pretty YAML](https://sublime.wbond.net/packages/Pretty%20YAML), and [PHP-Twig](https://sublime.wbond.net/packages/PHP-Twig).
2. [Atom](http://atom.io) - OS X/Windows/Linux - Un nouvel éditeur développé par Github. Il est gratuit et open source. Il est similaire à Sublime, mais ne possède pas encore autant de plug-ins.
3. [Notepad++](http://notepad-plus-plus.org/) - Windows - Un éditeur pour développeurs gratuit et très populaire sous Windows.
4. [Bluefish](http://bluefish.openoffice.nl/index.html) - OS X/Windows/Linux - Un éditeur de texte open source grauit destiné aux programmeurs et aux développeurs web.
5. [Visual Studio Code](https://code.visualstudio.com/) - Un éditeur de code source léger mais puissant qui s'exécute sur votre desktop. Il est disponible sous Windows, MacOS ou Linux.

### Editeurs de Markdown

Une autre option si vous travaillez principalement sur la création de contenu consiste à utiliser un **éditeur de Markdown**. Ce type d'éditeurs sont souvent très centrés sur le contenu et fournissent généralement un **aperçu en direct** de votre contenu rendu au format HTML. Il y en a littéralement des centaines, mais voici quelques bonnes options:

1. [MacDown](http://macdown.uranusjr.com/) - OS X - Un éditeur de Markdown gratuit, simple, léger et open source.
2. [LightPaper](http://lightpaper.42squares.in/) - OS X - $9.99, propre, puissant. Notre éditeur de Markdown de choix sur MacOS. **Obtenez 25% de réduction avec le code: GET_GRAV_25**
3. [MarkDrop](http://culturezoo.com/markdrop/) - OS X - $5, mais super propre et prise en charge intégrée de Droplr.
4. [MarkdownPad](http://markdownpad.com/) - Windows - Versions gratuite et Pro. Possède même le support pour l'édition des sections d'introduction YAML. Une excellente solution pour les utilisateurs de Windows.
5. [Mark Text](https://marktext.github.io/website/) - Editeur de Markdown gratuit et open source pour Windows / Linux / OS X. 

### Clients FTP

Bien qu'il existe de nombreuses façons de déployer **Grav**, le plus simple consiste à copier votre site local vers votre hébergement. Le moyen le plus simple d'y parvenir est d'utiliser un [client FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol). Il en existe beaucoup, voici ceux que nous recommandons:

1. [Transmit](http://panic.com/transmit/) - OS X - Le client FTP/SFTP de factor pour OS X. Facile à utiliser, rapide, synchronisation de dossiers et à peu prêt tout ce que vous pourriez attendre d'un tel client.
2. [FileZilla](https://filezilla-project.org/) - OS X/Windows/Linux - Probablement la meilleure option pour les utilisateurs de Windows et de Linux. Gratuit et très puissant (mais très moche sur Mac!).
3. [Cyberduck](http://cyberduck.io/) - OS X/Windows - Une option gratuite et décente pour utilisateurs de MacOS et de Windows. Pas aussi complet que les autres.
4. [ForkLift](http://www.binarynights.com/forklift/) - OS X - Une alternative solide à Transmit, et légèrement moins lourde à démarrer.


