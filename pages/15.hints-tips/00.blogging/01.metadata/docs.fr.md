---
title: Metadonnées
menu: Blogging
visible: true
twig_first: true
process:
    twig: true
taxonomy:
    category: docs
---

Lorsque vous utilisez Grav en tant que plate-forme de blog, vous souhaiterez inclure des métadonnées permettant de renseigner les descriptions et les images lorsque des personnes partagent votre publication sur des médias sociaux tels que Facebook, Twitter, etc. 

Vous ajouterez ces informations dans la section [d'en-tête](/content/headers) de votre page Grav. 

La documentation contient des références aux métadonnées que vous devez ajouter dans la section d'en-tête, sous [Meta Page Headers](/content/headers#meta-page-headers). Toutefois, si vous avez migré depuis une plate-forme telle que WordPress où vous utilisez un plugin pour cela, vous ne réaliserez peut-être pas l'importance de ces métadonnées.

Au déut de chacun de vos articles de log, vous souhaiterez avoir les éléments suivants:

```---
title: Titre de l'article
publish_date: Date à laquelle le blog va être publié
date: Date à laquelle le blog a été écrit
metadata:
    'og:title': Titre de l'article
    'og:type': article
    'og:description': Description de ce que votre article de blog couvre. Cela sera visible lorsque les lecteurs partageront votre message sur les médias sociaux.
    'og:url': L'URL de l'article
    'og:site_name': Le nom du site auquel appartient l'article de blog. 
    'og:locale': Le langage dans lequel est écrit votre blog
    'og:image': L'image que vous référencez ici sera visible lors du partage sur les médias sociaux.
    'twitter:card' : Le type de carte Twitter qui doit être utilisé.
    'twitter:site' : Votre identifiant Twitter
    'twitter:title' : Titre de l'article
    'twitter:description' : Description de ce que votre article de blog couvre. Cela sera visible lorsque les lecteurs partageront votre message sur les médias sociaux.
    'twitter:image' : 'image que vous référencez ici sera visible lors du partage sur les médias sociaux.
    'twitter:creator': Le nom twitter du l'auteur de l'article. 
taxonomy:
    category: [Catégorie de l'article]
    tag: [Tag 1, Tag 2, Tag 3, Tag 4]
    author: Nom de l'auteur
---
```

En savoir plus sur [les cartes Twitter](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started.html)

En savoir plus sur [le protocole Open Graph](http://ogp.me/)