+++
title = "Via des Webhooks"
description = "Comment pousser des événements vers d'autres systèmes"
weight = 3
+++

Nunux Keeper a une fonctionnalité de Webhook.
Il est possible de notifier un endpoint HTTP sur l'évènement d'un document.

Un événement peut concerner:

- Une création
- Une suppression
- Ou une modification de document

### Format de l'évènement

L'endpoint HTTP configuré recevra en POST l'objet JSON suivant:

- `action`: le type d'évènement
- `issue`: l'émetteur et la date d'émission
- `document`: Le document
  - `id`: son identifiant
  - `title`: son titre
  - `labels`: la liste des labels
  - `origin`: son URL d'origine
  - `date`: sa date de création/modification

**Exemple:**


```json
{
  "action": "create_document",
  "issue": {
    "url": "https://api.nunux.org/keeper",
    "date": "Sat Nov 17 2018 12:22:37 GMT+0100"
  },
  "document": {
    "id": "5b190798cc6ab70020bae60a",
    "title": "Alchemist Laboratory - Artwork",
    "labels": ["58186d8bf85a70004195725a"],
    "origin": "https://blenderartists.org/t/alchemist-laboratory/1133337",
    "date": "2018-11-11T22:02:05.820Z",
  }
}
```



### Créer un Webhook

Rendez-vous sur l'onglet `Webhook` de la page des settings pour créer un Webhook.

![](images/create-webhook.png?classes=border,shadow)

Sur cette page, vous devez préciser:

- L'URL du Webhook (en POST)
- Un secret (en option). Ce secret sera utilisé pour signer la requête et ainsi
  permettre de valider son origine.
- Les événements concernés (Création, mise à jour et/ou suppression)

Vous pouvez par la suite éditer ce webhook ou le supprimer.

![](images/manage-webhooks.png?classes=border,shadow)
