+++
title = "Avec des aggrégateurs RSS"
description = "Comment intégrer Nunux Keeper avec des agrégateurs RSS"
weight = 1
+++

Nunux Keeper supporte nativement les agrégateurs RSS suivants:

- [Nunux Reader](https://reader.nunux.org/welcome)
- [Miniflux](https://miniflux.app/)

Avec très peu de configuration, il est également possible d'intégrer:

- [Feedpushr](https://github.com/ncarlier/feedpushr)

### Nunux Reader

Pour Nunux Reader, il suffit d'activer le le service d'archivage dans l'écran de
profil:

![](/integration/nunux-reader.png?classes=border,shadow)

{{% notice note %}}
Pour une instance auto hébergée de Nunux Reader, il faudra configurer l'ID
et secret du client d'API.
{{% /notice %}}

### Miniflux

La [documentation officielle](https://docs.miniflux.app/en/latest/integration.html#nunux-keeper)
de Miniflux explique comment effectuer l'intégration.

![](/integration/miniflux.png?classes=border,shadow)

### Feedpushr

![](/integration/feedpushr.png?classes=border,shadow)

Pour envoyer les articles de Feedpushr vers Nunux Keeper, vous devez obtenir
une clé d'API puis utiliser la sortie `STDOUT` de Feedpusr comme suit:

```bash
$ feedpushr \
  | jq -c "select(.title) | {title:.title, content:.description, origin: .link}" \
  | while read next; do echo "$next" | http https://api:KEY@api.nunux.org/keeper/v2/documents; done
```

{{% notice tip %}}
En parlant de Feedpushr, on rappel que les pages des labels publiques exposent
un flux RSS.
Il est donc possible via Feedpushr de souscrire à ce flux et d'envoyer
automatiquement les documents publiques vers de nombreuses sorties tel que:
Twitter, Mastodon, etc.
{{% /notice %}}

