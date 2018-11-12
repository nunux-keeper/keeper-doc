+++
title = "Partager"
description = "Comment partager vos documents avec d'autres utilisateurs ou de façon publique"
weight = 3
+++

Dans Nunux Keeper la notion de partage concerne un label.
Autrement dit tous les documents ayant un label partagé sont partagés.

### Partager un label

Pour partager un label, vous pouvez:

- Cliquer sur le menu contextuel de la page d'un label et cliquer sur le lien
  `Share label`
- Ou accéder à l'URL [/label/ID/share](https://app.nunux.org/keeper/labels/ID/share)

La page d'édition d'un partage va s'ouvrir:

![](/share/create-sharing.png?classes=border,shadow)

Vous pouvez ici:

- Définir la durée du partage avec éventuellement un intervalle de temps
- Préciser le type de partage (publique ou non)

Un partage peut être borné ou non dans le temps.
Sa date de début peut également être positionnée dans le futur.

Un partage publique sera accessible sans besoin de s'authentifier.
Il s'agit d'une page dédiée qui permet de consulter librement les documents.

{{% notice note %}}
Cette page expose également un flux RSS à l'adresse suivante:
https://api.nunux.org/keeper/v2/public/[PAGE_ID]?output=rss
{{% /notice %}}

Un partage non publique est une page consultable uniquement par un utilisateur
connecté.

Dans les 2 cas, vous devez communiquer l'URL pour donner accès à un tiers.

### Gérer les partages

Pour gérer les partages, vous pouvez:

- Cliquer sur le lien `Sharing` du menu latéral gauche
- Ou accéder à l'URL [/sharing](https://app.nunux.org/keeper/lables/create)

La page de gestion des partages va s'ouvrir:

![](/share/manage-sharing.png?classes=border,shadow)

Sur cette page, vous pouvez:

- Modifier un partage existant
- Le supprimer

