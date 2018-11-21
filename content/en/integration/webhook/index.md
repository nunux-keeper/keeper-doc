+++
title = "Via Webhooks"
description = "How to push document events to other systems"
weight = 3
+++

Nunux Keeper has a Webhook feature.
It is possible to notify an HTTP endpoint on events of a document.

An event may concern:

- A creation
- A deletion
- Or a document modification

### Event format

The configured HTTP endpoint will receive the following JSON object in POST:

- `action`: type of event
- `issue`: the issuer and the issue date
- `document`: The document
  - `id`: its ID
  - `title`: its title
  - `labels`: the list of labels
  - `origin`: its original URL
  - `date`: its creation/modification date

**Example:**


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

### Create a Webhook

Go to the `Webhook` tab of the settings page to create a Webhook:

![](images/create-webhook.png?classes=border,shadow)

On this page, you must specify:

- The URL of the Webhook (in POST)
- A secret (optional).
  This secret will be used to sign the request and thus validate its origin.
- The events concerned (Creation, modification and/or deletion)

You can then edit or delete this webhook.


![](images/manage-webhooks.png?classes=border,shadow)
