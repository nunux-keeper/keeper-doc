+++
title = "Utiliser l'API"
description = ""
weight = 4
+++


Toutes les fonctionnalités de Nunux Keeper sont accessibles via une API.

L'API est documentée [ici](https://api.nunux.org/keeper/api-docs/).

L'API de création d'un document est accessible de 2 façons:

- En utilisant une clé d'API
- En déclarant un client d'API et utilisant des jetons avec une durée de vie
  courte (protocole OpenID Connect).

## Via la clé d'API

Cette première méthode est peu sécurisée et ne permet qu'un accès restreint à
l'API. Cependant cette méthode est la plus simple et permet tout de même de
créer un document.

La clé d'API s'obtient en allant sur la page des settings.

![](images/api-key.png)

{{% notice warning %}}
La clé d'API est affichée uniquement à sa création.
Si vous perdez cette clé, vous n'aurez d'autre choix que d'en générer une autre.
{{% /notice %}}

La clé d'API s'utilise simplement comme mot de passe d'une authentification
HTTP basique:

```bash
$ http https://api:KEY@api.nunux.org/keeper/v2/documents
origin="http://example.org/foo.html" title="Mon titre"
```

## Via OpenID Connect

Cette méthode permet d'accéder à toute l'API.
Elle nécessite cependant de déclarer un client d'API, puis d'obtenir un jeton
temporaire d'accès auprès du fournisseur d'authentification OpenID Connect
(Keycloak dans notre cas).

Il peut y avoir plusieurs types de client d'API.
L'IHM vous permet uniquement de configurer un client d'API de type Web.
Si vous désirez un autre type de client veuillez utiliser votre propre
fournisseur d'authentification OpenID Connect.

Allez sur la page des `settings` pour déclarer un client d'API Web.

![](images/create-api-client.png)

Vous devez fournir:

- Un nom
- Une ou plusieurs URL valides de redirection (utilisées après une authentification)
- Une ou plusieurs URL d'origine (URL d'origine autorisée pour les accès CORS)

Une fois les informations saisies et validées, vous obtiendrez les données
nécessaires à votre client OIDC:

- L'URL de discovery
- L'ID client
- Et son secret

![](images/edit-api-client.png)

