---
title: Configuration
taxonomy:
    category: docs
---

Tous les fichiers de configuration de Grav sont écrits en [syntaxe YAML](../../advanced/yaml) avec une extension de fichier `.yaml`.  YAML est très intuitif, ce qui facilite la lecture et l'écriture, mais vous pouvez consulter la page sur [YAML dans le chapitre Avancé](../../advanced/yaml) pour obtenir une compréhension complète de la sytaxe proposée. 

## Configuration Du Système

Grav s'efforce de rendre les choses aussi simples que possible pour l'utilisateur, de même que pour la configuration. Grav propose quelques options par défaut judicieuses, qui sont définies dans le fichier `system/config/system.yaml`.

Cependant, **vous ne devriez jamais changer ce fichier**, toutes les modifications de configuration que vous devez apporter devraient être stockées dans un fichier nommé `user/config/system.yaml`. Tout paramètre défini dans ce fichier ayant la même structure et le même nom remplace le paramètre fourni dans le fichier de configuration système par défaut. 

!!!! De manière générale, vous ne devriez **JAMAIS** changer quoi que ce soit dans le dossier `system/`.  Tout ce que fait l'utilisateur (création de contenu, installation de plugins, modification de la configuration, etc.) doit être effectué dans le dossier `user/`.  De cette manière, la mise à niveau est simplifiée et vos modifications sont conservées dans un seul emplacement pour la sauvegarde, la synchronisation, etc. 

Voici les variables présentes dans le fichier `system/config/system.yaml`:

### Options De Base

```yaml
absolute_urls: false
timezone: ''
default_locale:
param_sep: ':'
wrapped_site: false
reverse_proxy_setup: false
force_ssl: false
force_lowercase_urls: true
custom_base_url: ''
username_regex: '^[a-z0-9_-]{3,16}$'
pwd_regex: '(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}'
intl_enabled: true
```

Ces options de configuration n'apparaissent pas dans leurs propres sections. Ce sont des options générales qui affectent le fonctionnement du site, son fuseau horaire et son URL de base. 

* **absolute_urls**: URL absolues ou relatives pour `base_url`.
* **timezone**: Des valeurs valides peuvent être trouvées [ici](http://php.net/manual/en/timezones.php).
* **default_locale**: Paramètres régionaux par défaut (par défaut, utilise les paramètres système)
* **param_sep**: Utilisé pour les paramètres Grav dans l'URL. Ne changez pas cela à moins de savoir ce que vous faites. Grav > `1.1.16` définit automatiquement ce paramètre sur `;` pour les utilisateurs exécutant le servceur web Apache sous Windows.
* **wrapped_site**: Pour que les thèmes/plugins sachent si Grav est intégré dans une autre plate-forme. Peut prendre les valeurs `true` ou `false`.
* **reverse_proxy_setup**: Exécution dans un scénario de proxy inversé avec des ports de serveur web différents de ceux du proxy. Peut prendre les valeurs `true` ou `false`.
* **force_ssl**: Si activé, Grav force l'accès au site via HTTPS (REMARQUE: ce n'est pas une solution idéale). Peut être `true` ou `false`.
* **force_lowercase_urls**: Si vous souhaitez prendre en charge des URL à casse mixte, définissez cette option sur false.
* **custom_base_url**: Définissez manuellement `base_url` ici
* **username_regex**: Seulement les caractères miniscules, chiffres, tirets, caractères de soulignement. 3-16 caractères
* **pwd_regex**: Au moins un chiffre, une lettre majuscule et minuscule et au moins 8 caractères
* **intl_enabled**: Logique spéciale pour l'extension internationale de PHP (mod_intl)


### langues

```yaml
languages:
  supported: []
  include_default_lang: true
  translations: true
  translations_fallback: true
  session_store_active: false
  http_accept_language: false
  override_locale: false
```

La zone **Languages** du fichier féinit les paramètres de langue du site. Cela inclut la ou les langues prises en charge, la désignation de la langue par défaut dans les URL et les traductions. Voici le détail de la section **Languages** du fichier de configuration système:

* **supported**: Liste des langues supportées, p.ex. `[en, fr, de]`
* **include_default_lang**: Inclure le préfixe de la langue par défaut dans toutes les URL. Peut être `true` ou `false`.
* **translations**: Activer les traductions par défaut. Peut être `true` ou `false`.
* **translations_fallback**: Configuration de repli sur les traductions prises en charge si aucune langue active n'existe. Peut être `true` ou `false`.
* **session_store_active**: Stocker la langue active en session. Peut être `true` ou `false`.
* **http_accept_language**: Essayer de définirt la langue en fonction de l'en-tête http_accept_language dans le navigateur web. Peut être `true` ou `false`.
* **override_locale**: Remplacer les paramètres régionaux par défaut ou système avec des paramètres régionaux spécifiques. Peut être `true` ou `false`.

### Accueil

```yaml
home:
  alias: '/home'
  hide_in_urls: false
```

La section de la **page d'accueil (Home)** est l'endroit où vous déterminez le chemin par défaut pour la homepage du site. Vous pouvez également choisir de chacher la route de l'accueil dans les URL. 

* **alias**: Chemin par défaut pour home, c'est-à-dire `/home` ou `/`.
* **hide_in_urls**: Masquer la route de home dans les URL. Peut être `true` or `false`.

### Pages

```yaml
pages:
  theme: quark
  order:
    by: default
    dir: asc
  list:
    count: 20
  dateformat:
    default:
    short: 'jS M Y'
    long: 'F jS \a\t g:ia'
  publish_dates: true
  process:
    markdown: true
    twig: false
  twig_first: false
  never_cache_twig: false
  events:
    page: true
    twig: true
  markdown:
    extra: false
    auto_line_breaks: false
    auto_url_links: false
    escape_markup: false
    special_chars:
      '>': 'gt'
      '<': 'lt'
  types: [txt,xml,html,htm,json,rss,atom]
  append_url_extension: ''
  expires: 604800
  cache_control:
  last_modified: false
  etag: false
  vary_accept_encoding: false
  redirect_default_route: false
  redirect_default_code: 302
  redirect_trailing_slash: true
  ignore_files: [.DS_Store]
  ignore_folders: [.git, .idea]
  ignore_hidden: true
  url_taxonomy_filters: true
  frontmatter:
    process_twig: false
    ignore_fields: ['form','forms']
```

La section **Pages** du fichier `system/config/system.yaml` est l'endroit où vous déinissez une grande partie des principaux paramètres liés au thème. Par exemple, c'est à cet endroit que vous définissez le thème utilisé pour réaliser le produire le rendu du site, pour trier les pages, pour définir les traitements par défaut de twig et Markdown, et plus encore. C'est ici que sont prises la plupart des décisions qui ont une incidence sur le rendu de vos pages. 

* **theme**: C'est ici que vous définissez le thème par défaut. La valeur par défaut est `quark`.
* **order**:
    - **by**: Trie les pages selon une stratégie prédéfinie. Les valeurs acceptées sont `default`, `alpha` or `date`.
    - **dir**: Direction par défaut du tri, `asc` ou `desc`.
* **list**:
    - **count**: Nombre d'éléments par défaut pour cha  que page. 
* **dateformat**:
    - **default**: Le format de date par défaut que Grav attend dans le champ `date: `.
    - **short**: Format de date raccourci. Exemple: `'jS M Y'`
    - **long**: Format de date long. Exemple: `'F jS \a\t g:ia'`
* **publish_dates**: Publier/dépublier automatiquement sur la base des dates. Peut être `true` ou `false`.
* **process**:
    - **markdown**: Activer ou désactiver le traitement du Markdown sur le front-end. Peut être défini à `true` ou `false`.
    - **twig**: Activer ou désactiver le traitement du twig sur le front-end. Peut être défini à `true` ou `false`.
* **twig_first**: Traitez twig avec le Markdown lorsque les deux doivent être traîté sur une même page. Peut être `true` ou `false`.
* **never_cache_twig**: Activer cette option vous permettra d'ajouter une logique de traitement pouvant changer dynamiquement à chaque chargement de page, plutôt que de mettre en cache les résultats et de les stocker pour chaque chargement. Peut être activé à l'échelle du site dans **system.yaml** ou sur une page spécifique. Peut être défini à true` or `false`.
* **events**:
    - **page**: Activer les événements au niveau de la page. Peut être `true` ou `false`.
    - **twig**: Activer les événements au niveau de Twig. Peut être `true` ou `false`.
* **markdown**:
    - **extra**: Activer le support de Markdown Extra (version Github par défaut (GFM: Gihub-flavored Markdown)) Peut être `true` ou `false`.
    - **auto_line_breaks**: Activer les sauts de ligne automatique. Peut être `true` ou `false`.
    - **auto_url_links**: Activer les liens HTML automatique. Peut être `true` ou `false`.
    - **escape_markup**: Echapper les balises de markup sous forme d'entité. Escape markup tags into entities. Peut être `true` ou `false`.
    - **special_chars**: Liste des caractères spéciaux à convertir automatiquement en entités. Chaque caractère utilise une ligne en dessous de cette option. Exemple: `'>': 'gt'`.
* **types**: Liste des types de page valides. Par exemple: `[txt,xml,html,htm,json,rss,atom]`
* **append_url_extension**: Ajouter l'extension de la page dans les URL de la page. (p.ex. `.html` conduit à **/path/page.html**).
* **expires**: Temps d'expiration de la page en secondes  (604800 secondes = 7 jours) (`no cache` est également possible).
* **cache_control**: Peut être vide pour exprimer aucun paramètre, ou une valeur [valide](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control): `cache-control`
* **last_modified**: Définir en-tête pour la date de dernière modification sur la base de l'horodatage de modification du fichier. Peut être `true` ou `false`.
* **etag**: Définir la balise d'en-tête etag. Peut être `true` ou `false`.
* **vary_accept_encoding**: Ajouter l'en-tête `Vary: Accept-Encoding`. Peut-être `true` ou `false`.
* **redirect_default_route**: Rediriger automatiquement sur la route d'une page par défaut. Peut être `true` ou `false`.
* **redirect_default_code**: Code à utiliser par défaut pour les redirections. Par exemple: `302`.
* **redirect_trailing_slash**: Traiter automatiquement un / à la fin de l'URL ou effectuer une redirection 302.
* **ignore_files**: Fichiers à ignorer en dans les pages. Exemple: `[.DS_Store] `.
* **ignore_folders**: Répertoires à ignorer dans les pages. Exemple: `[.git, .idea]`
* **ignore_hidden**: Ignorer tous les fichiers et répertores cachés. Peut être `true` ou `false`.
* **url_taxonomy_filters**: Activer les filtres de taxonomie basés sur les URL auto-magiques pour la collecte des pages. Peut être`true` ou `false`.
* **frontmatter**:
    - **process_twig**: L'en-tête de page doit-il être traité pour remplacer les variables Twig? Peut être `true` ou `false`.
    - **ignore_fields**: Champs pouvant contenir des variables Twig et qui doivent pas être traités. Exemple: `['form','forms']`

### cache

```yaml
cache:
  enabled: true
  check:
    method: file
  driver: auto
  prefix: 'g'
  clear_images_by_default: true
  cli_compatibility: false
  lifetime: 604800
  gzip: false
  allow_webserver_gzip: false
  redis:
    socket: false
```

La section **Cache** vous permet de configurer les paramètres de mise en cache du site. Vous pouvez activer, désactiver, choisir la méthode, etc. 

* **enabled**: Définir à vrai (`true`) pour activer la mise en cache. Peut être `true` ou `false`.
* **check**:
    - **method**: Méthode à utiliser pour vérifier la mise à jour des pages. Options: `file`, `folder`, `hash` et `none`. [plus](../../advanced/performance-and-caching#grav-core-caching)
* **driver**: Sélectionner un driver pour le cache. Les options sont: `auto`, `file`, `apc`, `xcache`, `redis`, `memcache`, et `wincache`.
* **prefix**: Chaîne de caractère à utiliser comme préfixe pour le cache (évite les conflits dans la mise en cache). Exemple: `g`.
* **clear_images_by_default**: Par défaut, Grav inclut les images traitées lorsque la mémoire cache est vidée. Pour désactiver, définir cette option à `false`
* **cli_compatibility**: S'assurer que seuls les drivers non volatiles sont utilisés (file, redis, memcache, etc.)
* **lifetime**: Durée de vie données mises en cache en secondes (`0` = infini). `604800` correspond à 7 jours.
* **gzip**: GZip compresse la sortie de la page. Peut être `true` ou `false`.
* **allow_webserver_gzip**: Cette option changera l'en-tête en `Content-Encoding: identity`, ce qui permettra à gzip d'être défini de manière plus fiable par le serveur web, bien que cela pose généralement des problèmes avec la fonctionnalité `onShutDown()`.  L'événement sera toujours exécuté, mais il ne sera pas hos processus et pourra bloquer la page jusqu'à ce que l'événement soit terminé. 

### twig

```yaml
twig:
  cache: true
  debug: true
  auto_reload: true
  autoescape: false
  undefined_functions: true
  undefined_filters: true
  umask_fix: false
```

La section **Twig** vous donne un ensembble rapide d'outils permettant de configurer Twig sur votre site pour le débogage, la mise en cache et l'optimisation. 

* **cache**: Définir à vrai (`true`) pour activer la mise en cache pour Twig. Peut être `true` ou `false`.
* **debug**: Active le debug de Twig. Peut être `true` ou `false`.
* **auto_reload**: Actualiser le cache lors des modifications. Peut être `true` ou `false`.
* **autoescape**: Echaper automatiquement les variables Twig. Peut être`true` ou `false`.
* **undefined_functions**: Autoriser les fonctions non définies. Peut être `true` ou `false`.
* **undefined_filters**: Permettre les filtres non définis. Peut être `true` ou `false`.
* **umask_fix**: Par défaut, Twig créé les fichiers en cache avec les permissions 755. Peut être `true` ou `false`.

### assets

```yaml
assets:
  css_pipeline: false
  css_pipeline_include_externals: true
  css_pipeline_before_excludes: true
  css_minify: true
  css_minify_windows: false
  css_rewrite: true
  js_pipeline: false
  js_pipeline_include_externals: true
  js_pipeline_before_excludes: true
  js_minify: true
  enable_asset_timestamp: false
  collections:
    jquery: system://assets/jquery/jquery-2.x.min.js
```

La section **Assets** vous permet de configurer les options relatives à l'Asset Manager (JS, CSS).

* **css_pipeline**: Le pipeline CSS est l'unification de plusieurs ressources CXSS dans un seul fichier. Peut être `true` or `false`.
* **css_pipeline_include_externals**: Inclure des URL externes dans le pipeline par défaut. Peut être `true` or `false`.
* **css_pipeline_before_excludes**: Produire le rendu du pipeline avant tout fichier exclu. Peut être `true` or `false`.
* **css_minify**: Minifier le CSS durant le traitement. Peut être `true` or `false`.
* **css_minify_windows**: Ecraser l'option minifier pour les plate-formes Windows. `false` par défaut à cause de ThreadStackSize. Peut être `true` or `false`.
* **css_rewrite**: Réécrire les URL relatives dans le CSS durant le traitement. Peut être `true` or `false`.
* **js_pipeline**: Le pipline JS est le processus permettant l'unification de plusieurs ressources JS en une seul fichier. Peut être `true` or `false`.
* **js_pipeline_include_externals**: Inclure par défaut des URL externes dans le pipline de traitements du JS. Peut être `true` or `false`.
* **js_pipeline_before_excludes**: Produire le rendu du pipline avant tout fichier excut. Peut être `true` or `false`.
* **js_minify**: Minifier le JS durant le pipline de traitements. Peut être `true` or `false`.
* **enable_asset_timestamp**: Activé l'horodatage des assets. Peut être `true` or `false`.
* **collections**: Contient des collections, désignées comme sous-éléments. Par exemple: `jquery: system://assets/jquery/jquery-2.x.min.js`

### erreurs

```yaml
errors:
  display: 0
  log: true
```

La section **Errors** détermine comment Grav gère l'affichage et la consignation des erreurs. 

* **display**: Détermine comment les erreurs sont affichées. Entrez soit `1` pour la trace complète, `0` pour une erreur simple ou `-1` pour une erreur système
* **log**: Log errors to `/logs` folder. Can be set to `true` or `false`.

### debogueur

```yaml
debugger:
  enabled: false
  shutdown:
    close_connection: true
```

Cette section vous permet d'activer le débogage de Grav. Un outil utile lors du développement. 

* **enabled**: Activer le débogueur de Grav et les options qui s'y rapportent. Peut être `true` or `false`.
* **shutdown**:
    - **close_connection**: Fermer la connexion avant d'appeler `onShutdown()`. `false` pour le débogage.

### images

```yaml
images:
  default_image_quality: 85
  cache_all: false
  cache_perms: '0755'
  debug: false
  auto_fix_orientation: false
```

Cette section vous permet de définir la qualité d'image par défaut utilisée pour le rééchantillonnage des images, ainsi que de contrôler les fonctionnalités de mise en cache et de débogage des images. 

* **default_image_quality**: Qualité par défaut des images à utiliser lors du rééchantillonnage. Par exemple: `85` = 85%.
* **cache_all**: Mettre en cache toutes les images par défaut. Peut être `true` or `false`.
* **cache_perms**: DOIT ETRE ENTRE GUILLEMETS.!! Permissions par défaut pour le répertoire de cache. Générallement `'0755'` ou `'0775'`
* **debug**: Afficher un filligrane sur les images indiquant la profondeur en pixels de l'image lorsque vous travaillez avec Retina. Peut être `true` or `false`.

### media

```yaml
media:
  enable_media_timestamp: false
  unsupported_inline_types: []
  allowed_fallback_types: []
  auto_metadata_exif: false
```

La section **Media** traite des options de configuration pour les paramètres liés à la gestion des fichiers multimédias. Cela inclut l'affichage de l'horodatage, la taille de téléchargement, etc. 

* **enable_media_timestamp**: Activer l'horodatage des médias. 
* **unsupported_inline_types**: Tableau de types de media pris en charge pour un essai d'affiche inline. Ces types de fichiers sont placés entre crochets `[]`. 
* **allowed_fallback_types**: Tableau des types de fichiers media autorisés si accédés via la route d'une page. Ces types de fichiers sont placés entre crochets `[]`. 
* **auto_metadata_exif**: Créer automatiquement des fichiers de méta-données à partir de données Exif lorsque c'est possible 

### session

```yaml
session:
  enabled: true
  timeout: 1800
  name: grav-site
  secure: false
  httponly: true
  split: true
  path:
```

Ces options déterminent les propriétés de session pour votre site.

* **enabled**: Activer le support des sessions. Peut être `true` or `false`.
* **timeout**: Délai d'attente en secondes. Par exemple: `1800`.
* **name**: Préfixe de nom pour le cookie de session. Utiliser des caractères alphanumériques, des tirets ou des caractères de soulignement uniquement. Ne pas utiliser de points dans le nom de la session. Par exemple: `site-grav`.
* **secure**: Active l'option session secure. Si l'option vaut `true`, cela indique que la communcation de ce cookie doit utiliser une transmission chiffrée. Activer cette fonctionnalité seulement sur les sites qui tournent exclusivement sur HTTPS. Peut être `true` or `false`.
* **httponly**: Active l'option HTTP only. Si la valeur de cette option est `true`, cela indique que ce cookie ne devrait être utilisé que par l'intermédiaire de HTTP, et que les modification Javascript ne sont pas autorisées. Peut être `true` or `false`.
* **path**:

### gpm

```yaml
gpm:
  releases: stable
  proxy_url:
  method: 'auto'
  verify_peer: true
  official_gpm_only: true
```

La section **GPM** offre aux utilisateurs des options permettant de contrôler comment le gestionnaire de paquets de Grav obtient et prépare les mises à jour pour votre site. Vous pouvez choisir entre les versions stable et de test, ainsi que définir l'URL d'un proxy. 

* **releases**: Régler sur `stable` ou `testing` pour déterminer si vous souhaitez mettre à jour la dernière version stable ou la version de test. 
* **proxy_url**: Configurer manuellement une URL de proxy pour GPM. Par exemple: `127.0.0.1:3128`.
* **method**: Soit 'curl', 'fopen' ou 'auto'. 'auto' va essayer fopen en premier et, si non disponible, cURL
* **verify_peer**: Sur certains système (essentiellement Windows), GPM n'arrive pas à se connecter, car le certificat SSL ne peut être vérifié. Désactiver cette option peut aider. 
* **official_gpm_only**: Par défaut, l'installation directe via GPM n'autorisera que les URL qui passent via le proxy officiel de GPM pour des questions de sécurité, désactivez cette option pour autoriser d'autres sources. 

!! Vous n'avez pas besoin de copier **l'ensemble** du fichier de configuration pour modifier certaines options. Vous pouvez modifier aussi peu ou autant que vous le désirez. Assurez-vous juste que vous conservez **une structure d'option rigoureusement identifique** pour les options spécifiques que vous désirez personnaliser. 

## Configuration du site

En plus du fichier `system.yaml`, Grav fournit également un fichier de configuration par défaut appelé `site.yaml` qui est utilisé pour définir une configuration par défaut spécifique au front-end telle que le nom de l'auteur, l'adresse email de l'auteur, ainsi que certans paramètres de taxonomie importants. Vous pouvez les remplacer de la même manière que vous le feriez avec system.yaml en fournissant votre propre fichier de configuration dans `user/config/site.yaml`. Vous pouvez également utiliser ce fichier pour définir des options de configuration arbitraires que vous pourrez ensuite référencer à partir de votre contenu ou de vos gabaris.

Le fichier par défaut, `system/config/site.yaml`, qui est envoyé avec Grav, ressemble à quelque chose comme ça: 

```ruby
title: Grav                                 # Nom du site

author:
  name: John Appleseed                      # Nom de l'auteur par défaut
  email: 'john@email.com'                   # Email de l'auteur par défaut

taxonomies: [category,tag]                  # Liste de types taxonomiques arbitraires

metadata:
  description: 'My Grav Site'               # Description du site

summary:
  enabled: true                             # activer ou désactiver le résumer de la page
  format: short                             # long = résumé, le délimiteur sera ignoré; short = utiliser la première occurrence du délimiteur ou une indication de taille
  size: 300                                 # Longueur maximale du résumé (en caractères)
  delimiter: ===                            # Délimiteur pour le résumé

redirects:
#  '/redirect-test': '/'                         # Test de redirection qui pointe vers la page d'accueil
#  '/old/(.*)': '/new/$1'                        # Redirigerait /old/my-page vers /new/my-page

routes:
#  '/something/else': '/blog/sample-3'         # Alias pour /blog/sample-3
#  '/new/(.*)': '/blog/$1'                     # Regex toute /new/my-page URL vers /blog/my-page Route

blog:
  route: '/blog'                            # Valeur personnalisée ajoutée (accessible via system.blog.route)

#menu:                                      # Echantillon exemple de Menu
#    - text: Source
#      icon: github
#      url: https://github.com/getgrav/grav
#    - icon: twitter
#      url: http://twitter.com/getgrav
```

Décomposons les éléments de ce fichier exemple:

| Champ                | Description                                                                                                                                                                                                                                                                                                                                                              |
| :-----               | :-----                                                                                                                                                                                                                                                                                                                                                                   |
| **title:**           | Le titre est une simple variable chaîne de caractère pouvant être référencée chaque fois que vous souhaitez afficher le nom de ce site.                                                                                                                                                                                                                               |
| **author: name:**    |  Le nom de l'auteur du site, qui peut être référencé lorsque vous en avez besoin.                                                                                                                                                                                                                                                                                     |
| **author: email:**   | Un email par défaut à utiliser pour votre site.                                                                                                                                                                                                                                         |
| **taxonomies:**      | Une liste arbitraire de types de haut niveau que vous pouvez utiliser pour organiser votre contenu. Vous pouvez affecter du contenu à des types de taxonomie spécifiques, par exemple des catégories ou des étiquettes (tags). N'hésitez pas à modifier ou à ajouter les vôtres.                                                                                                                                                                      |
| **metadata:**        | Définit les métadonnées par défaut pour toutes vos pages, voir la section [en-têtes de pages](../../content/headers) pour plus de détails.                                                                                                                                                                                                                                  |
| **summary: size:**   | Variable permettant de remplacer le nombre de caractères par défaut pouvant être utilisé pour définir la taille du résumé lors de l'affichage d'une partie du contenu.                                                                                                                                                                                           |
| **routes:**          | Il s'agit d'un mapping basique qui peut fourir des alias d'URL simples dans Grav.  Si vous naviguez vers `/something/else` vous serez effectivement redirigés vers `/blog/sample-3`. N'hésitez pas à modifier ou à ajouter vos propres alias au besoin. **Les remplacements sous forme d'expressions rationnelles** (`(.*) - $1`) sont maintenant pris en charge à la fin des alias des routes. Vous devriez mettre ces définition au bas de la liste pour des performances optimales.                                                                                                                                                                                                        |
| **(custom options)** | Vous pouvez créer n'importe quelle option dans ce fichier. Un bon exemple est l'option `blog: route: '/blog'` qui est accessible dans vos gabaris Twig via `system.blog.route`                                                                                                                                                                                  |

!! Pour la plupart des gens, l'élément le plus important de ce fichier est la liste `Taxonomy`.  Les taxonomies de cette liste **doivent** être définies ici si vous souhaitez les utiliser dans votre contenu. 

## Autres paramètres et fichiers de configuration

La configuration de l'ûtilisateur est complètement facultative. Vous pouvez remplacer autant de paramètres par défaut que vous le souhaitez. Ceci s'applique à la fois au système, au site et à toutes les configuration de plugin de votre site. 

De plus, vous n'êtes pas limité aux fichiers `user/config/system.yaml` ou `user/config/site.yaml` comme décrit ci-dessus. Vous pouvez créer n'importe quel fichier de configuration de votre choix avec l'extension `.yaml` dans le répertoire `user/config` et il sera automatiquement chargé par Grav.

Par exemple, si le nouveau fichier de configuration s'appelle  `user/config/data.yaml` et qu'il contient une variable yaml appelée count:

```
count: 39
```

La variable serait accessible dans notre gabari Twig en utilisant la syntaxe suivante: 

```
{{ config.data.count }}
```

Il serait également accessible via PHP depuis n'importe quel plugin avec le code suivant:

```
$count_var = Grav::instance()['config']->get('data.count');
```

! Vous pouvez également fournir un fichier blueprint personnalisé pour permettre la modification de votre fichier personnalisé depuis le plugin d'admin. Découvrez [la marche à suivre dans la section Admin du Cookbook](/cookbook/admin-recipes#add-a-custom-yaml-file).

## Espace de nommage des variables de configuration

Les chemins d'accès aux fichiers de configuration seront utilisés comme **espaces de noms** pour vos options de configuration. 

Vous pouvez également placer toutes les options dans un fichier et utiliser les structures YAML pour spécifier la hiérarchie de vos options de configuration. Ce mécanisme d'espace de nommage est construit sur une combinaison entre **chemin + nom de fichier + nom de l'option**.

Par exemple: une option telle que `author: Frank Smith` dans le fichier `plugins/myplugin.yaml` pourrait être accessible via: `plugins.myplugin.author`. Cependant, vous pouvez également avoir un fichier `plugins.yaml` et avoir dans ce fichier une option appelée `myplugin: author: Frank Smith` et l'option serait toujours accessible par le même espace de noms `plugins.myplugin.author`.

Quelques fichiers de configuration exemples ont pu être structurés:

| Nom de fichier                         | Description                                       |
| :-----                                 | :-----                                            |
| **user/config/system.yaml**            | Fichier de configuration système global           |
| **user/config/site.yaml**              | Fichier de configuration spécifique au site     |
| **user/config/plugins/monplugin.yaml** | Fichier de configuration individuel pour le plugin monplugin |
| **user/config/themes/montheme.yaml**   | Fichier de configuration individuel pour le thème montheme   |

!! Avoir un fichier de configuration dans son espace de nom écrasera ou masquera toutes les options ayant le même chemin dans fichiers de configuration par défaut. 

### Configuration des plugins

La plupart des **plugins viendront leur propre fichier de configuration YAML. Nous recommendons de copier ce fichier dans le répertoire **user/config/plugins/** plutôt que d'éditer directement les options de configuration du fichier situé dans le répertoire du plugin. Cette mesure assurera qu'une mise à jour du plugin n'écrasera pas vos personnalisations, et permettra de conserver toutes vos options configurables dans un endroit pratique.

Si vous avez un plugin `user/plugins/myplugin` qui possède un fichier de configuration appelé `user/plugins/myplugin/myplugin.yaml`, alors vous pouvez copier ce fichier vers `user/config/plugins/myplugin.yaml` et l'éditer dans ce répertoire.

Le fichier YAML qui existe dans le répertoire principal du plugin servira de configuration par défaut. Chaque option listée dans dans ce fichier et pas dans celui de la copie du répertoire utilisateur sera collectée et utilisée par Grav. 

### Configuration du thème

Les mêmes règles que pour les plugins sont appliquées pour les thèmes. Ainsi, si vous avez un thème appelé `user/themes/montheme` qui possède un fichier de configuration appelé `user/themes/montheme/montheme.yaml`, alors vous pourrez copier ce fichier vers `user/config/themes/montheme.yaml` et l'éditer dans ce répertoire.
