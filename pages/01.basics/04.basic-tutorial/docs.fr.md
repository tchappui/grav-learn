---
title: Tutoriel de Base
taxonomy:
    category: docs
---

En supposant que vous ayez réussi à installer [Grav](../installation) en suivant les instructions du chapitre précédent, nous pouvons continuer et jouer un peu avec Grav pour vous mettre plus à l'aise. 

Grav ne nécessitant pas de base de données, il est très facile de travailler avec lui, sans avoir à s'inquiéter de problèmes pouvant survenir entre votre installation de Grav et toute source de données externe d'importance. Si quelque chose ne va pas, vous pouvez généralement récupérer la situation très facilement. 

## Fondamentaux Sur La Gestion Du Contenu

Tout d'abord, familiarisons-nous avec l'endroit dans lequel Grav stocke le contenu. Nous approfondirons dans un [chapitre à venir](../folder-structure), mais pur le moment, vous devez savoir que tout notre contenu utilisateur est stocké dans le dossier `user/pages/` de votre installation de Grav.

Actuellement, il y a deux dossiers dans le dossier des pages, le premier s'appelle `01.home` et le second `02.Typography`.  La partie `01.` du dossier est facultative mais fournit quelques éléments qui peuvent être utiles.

Premièrement, il vous permet de définir expressément l'ordre de vos pages. Par exemple, `01` viendra avant `02`, mais `00` sera avant `01`.

L'autre chose que la partie numérique du nom du dossier fait est d'informer Grav explicitement que cette page doit être visible dans le menu. Il est important de noter que la partie numérique, y compris le `.`, sera supprimée des URL. 

## Configuration De La Page D'Accueil

Il existe une option dans le fichier `user/config/system.yaml` qui définit l'emplacement de la __page d'accueil__, en d'autres termes, où Grav pointe lorsque vous référencez la racine de votre site: `http://yoursite.com`.

Si vous examinez ce fichier de configuration lors de l'installation, vous verrez qu'il pointe déjà sur l'alias de `/home`.  Nous pouvons le laisser comme ça dans cet exemple.

## Edition De Pages

Les pages dans **Grav** sont composées à l'aide de la syntaxe **Markdown**.  Markdown est une syntaxe de mise en forme écrite en texte brut, puis convertie automatiquement en HTML. Elle utilise des symboles de texte élémentaires pour indiquer les balises HTML associées, ce qui permet d'écrire facilement sans avoir à connaître la complexité du HTML. L'utilisation de Markdown présente de nombreux autres avantages, parmi lesquels, moins d'erreurs, un balisage valide. Il est par ailleurs très lisible, simple à apprendre, transférable, etc.

Vous pouvez lire une [description détaillée de la syntaxe de Markdown](../../content/markdown) avec des exemples dans la documentation. Mais pour le moment, continuez de lire ci-dessous.

Ouvrez la page d'accueil dans votre éditeur de texte. Le fichier qui contrôle la page d'accueil se trouve dans le dossier `user/pages/01.home/` et s'appelle `default.md`. Tout le contenu que vous créez sera créé dans le dossier `user/pages/` de votre installation Grav.

Lorsque vous modifiez la page dans un éditeur de texte, le contenu ressemblera à ceci (en anglais): 

    ---
    title: Home
    ---

    # Grav is Running!
    ## You have installed **Grav** successfully

    Congratulations! You have installed the **Base Grav Package** that provides a **simple page** and the default **antimatter** theme to get you started.

    ! If you want a more **full-featured** base install, you should check out [**Skeleton** packages available in the downloads](http://getgrav.org/downloads).

    ### Find out all about Grav

    * Learn about **Grav** by checking out our dedicated [Learn Grav](http://learn.getgrav.org) site.
    * Download **plugins**, **themes**, as well as other Grav **skeleton** packages from the [Grav Downloads](http://getgrav.org/downloads) page.
    * Check out our [Grav Development Blog](http://getgrav.org/blog) to find out the latest goings on in the Grav-verse.

Laissez-nous décomposer un peu afin que vous puissiez voir comme il est facile d'écrire dans un fichier Markdown. Les éléments entre les séparateurs `---` sont les [en-têtes de la page](../../content/headers), et ils sont écrits dans un format simple appelé [YAML](../../advanced/yaml). Ce bloc de configuration contenu dans le fichier `.md` est communément appelé **l'en-tête YAML**.

```ruby
title: Home
```

Ce bloc définit la balise de titre HTML pour la page (le texte que vous voyez dans l'onglet du navigateur web). Vous pouvez également y accéder depuis vos thèmes via l'attribut `page.title`. Il existe quelques [en-têtes standard](../../content/headers) qui vous permettent de configurer diverses options pour cette page. Un autre exemple est `menu: QuelqueChose` qui vous permet de remplacer dans le menu le texte utilisé pour afficher le nom de la page. Par défaut, Grav utilisera le titre comme entrée dans le menu. 

```markdown
# Grav is Running!
## You have installed **Grav** successfully
```

La syntaxe `#` ou `dièses` ou `hashes` dans un fichier Markdown indique un titre. Un simple `#` avec un espace puis du texte est converti en un une balise `<h1>` en HTML.  syntax in markdown indicates a title. Le `##` ou double dièse serait converti en une balise `<h2>`.  ien sûr, cela va jusqu'à la balise de titre HTML de niveau `<h6>` qui est bien sûr composée de six dièses `###### Mon Titre De Niveau H6`.

```markdown
Congratulations! You have installed the **Base Grav Package** that provides a **simple page** and the default **antimatter** theme to get you started.
```

C'est un simple paragraphe qui aurait été encapsulé dans des balises `<p>` lors de la conversion en HTML.  Les marqueurs `**` transforment le texte en gras ou `<b>` en HTML. Le texte en italic est indiqué en plaçant ce dernier entre des marqueurs `_`.

```markdown
* Learn about **Grav** by checking out our dedicated [Learn Grav](http://learn.getgrav.org) site.
* Download **plugins**, **themes**, as well as other Grav **skeleton** packages from the [Grav Downloads](http://getgrav.org/downloads) page.
* Check out our [Grav Development Blog](http://getgrav.org/blog) to find out the latest goings on in the Grav-verse.
```

La création de listes non ordonnées est très simple en Markdown. Utilisez simplement un `*`, un `-` ou un `+` suivit d'un espace pour indiquer que le texte fait partie d'une liste. Pour une liste ordonnée, utilisez simplement un nombre et un point avant le texte. 

Cet aperçu devrait vous fournir quelques indications clés pour l'écriture de texte en Markdown, mais vous devriez consulter notre [explication plus détaillée](../../content/markdown) pour mieux comprendre.

!! Veillez à enregistrer vos fichiers `.md` sous forme de fichiers `UTF8`. Cela garantira qu'ils fonctionnent avec des caractères spéciaux spécifiques à la langue utilisée. 

## Ajouter Une Nouvelle Page

Créer une nouvelle page est une affaire de quelques minutes dans **Grav**. Il suffit de suivre ces étapes simples: 

1. Rendez-vous dans le dossier des pages: `user/pages/` et créez un nouveau dossier. Dans cet exemple, nous allons utiliser [le tri explicite par défaut](http://learn.getgrav.org/content/content-pages) et appeler le dossier `02.mapage`.
2. Lancez votre éditeur de texte, créez un nouveau fichier et collez le code d'exemple suivant: 

    ```markdown
    ---
    title: Une Nouvelle Page
    ---
    # Ma Toute Nouvelle Page!

    Voici le contenu de **ma toute nouvelle page** et je peux facilement utiliser la syntaxe _Markdown_ ici.
    ```

3. Enregistrez ce fichier dans le dossier `user/pages/02.mapage/` sous le nom `default.md`. Cela indiquera à **Grav** de rendre la page en utilisant le gabari **par défaut**. 

La page s'affichera automatiquement dans le menu après la page d'**Accueil**. Si vous souhaitez odifier le nom qui apparaît dans le menu, ajoutez: `menu: Ma Super Page` dans l'en-tête de la page.

**Félicitations**, vous venez de créer une nouvelle page avec succès dans Grav. Grav vous permet de faire beaucoup plus, alors continuez à lire pour en savoir plus sur les fonctionnalité plus avancées et plus en profondeur.

!! Si vous rencontrez des problèmes pour accéder à cette nouvelle page, il vous manque un fichier `.htaccess` (uniquement pour le serveur web Apache) ou vous devez peut-être modifier la commande `RewriteBase` dans le fichier `.htaccess`. Veuillez consulter la section [Dépannage](../../troubleshooting) pour plus d'informations.
