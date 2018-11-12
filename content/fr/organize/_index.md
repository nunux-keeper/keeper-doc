+++
title = "Classer et Organiser"
description = ""
weight = 2
+++

Pour organiser vos documents, vous pouvez leur affecter des labels.

### Les labels

Un label est l'équivalent d'un tag avec un code couleur.

Pour créer un nouveau label, vous pouvez :

- Cliquer sur le lien `Create new Label` dans le menu latéral gauche
- Ou accéder à l'URL [labels/create](https://app.nunux.org/keeper/lables/create)

La page d'édition de label va s'ouvrir:

![](/organize/create-label.png?classes=border,shadow)

Sur cette page vous pouvez:

- Donner un nom à votre label
- Affecter une couleur

Appuyer sur le bouton `Submit` pour créer le label.

Une fois créé, vous pouvez affecter ce label à vos documents.
Pour cela il suffit de cliquer sur la liste déroulante des labels de vos
documents.
Les documents seront alors regroupés par label et vous pourrez naviguer entre
les labels en cliquant dessus.

![](/organize/doc-with-tags.png?classes=border,shadow)

### Le moteur de recherche

Une autre façon de retrouver vos documents est le moteur de recherche.
Ce dernier est un moteur de recherche "full text" très puissant: ElasticSearch

Vous pouvez taper simplement vos mots clés ou avoir recours aux mots clés pour
affiner votre recherche.

![](/organize/searchbar.png?classes=border,shadow)

Exemples de recherche:

- Rechercher les documents contenant `amazon` OU `alexa`:
  `amazon alexa` ou `amazon OR alexa`
- Rechercher les documents contenant `amazon` ET `alexa`:
  `amazon +alexa` ou `amazon AND alexa`
- Rechercher les documents contenant `amazon` sans `alexa`:
  `amazon -alexa` ou `amazon AND NOT alexa`
- Rechercher les documents dont le titre contient `alexa`:
  `title: alexa`
- Rechercher les documents sans label:
  `NOT _exists_: labels`
- ...

Vous pouvez trouver la documentation complète de cette syntaxe [ici][query-dsl].


[query-dsl]: https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html
