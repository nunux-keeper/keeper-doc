+++
title = "Avec NodeRED"
description = "Comment intégrer Nunux Keeper avec NodeRED et donc le reste du monde"
weight = 2
+++

![](/integration/node-red-logo.png?classes=border,shadow)

NodeRED est un outil extrêmement puissant qui dispose d'un nombre impressionnant
de connecteurs:

- [Twitter][twitter]
- [Mastodon][mastodon]
- [Telegram][telegram]
- [Pushbullet][pushbullet]
- [Slack][slack]
- [Dropbox][dropbox]
- [Facebook][facebook]
- et [plus](https://flows.nodered.org/)

Cela en fait l'outil de méditation par excellence.

Voici quelques exemples d'usage avec Nunux Keeper:

- Twitter automatiquement les nouveaux documents
- Archiver dans Nunux Keeper les tweets d'une timeline ou d'une recherche
- Envoyer une notification à votre mobile lorsqu'un document est créé (par
  exemple avec [Pushbullet](https://www.pushbullet.com/) ou
  [Pushover](https://pushover.net/))
- Envoyer des liens depuis vos devices via un système de push et archiver les
  dans Nunux Keeper
- Etc.

### Utiliser l'API depuis NodeRED

Utiliser l'API depuis NodeRED nécessite l'usage du module
[node-red-contrib-openid](https://github.com/ncarlier/node-red-contrib-openid).
Ce module va prendre en charge l'authentification et l'entretient des jetons
d'accès à l'API.

Vous devez, dans un premier temps, déclarer dans Nunux Keeper un nouveau client
d'API.
Veuillez vous référer à [la section de cette documentation](../../create-doc/api#via-openid-connect).

Une fois l'ID client et le secret obtenu, vous pouvez retourner sur NodeRED,
ouvrir un nœud OIDC et saisir les informations suivantes:

- L'URL de discovery d'OIDC: https://login.nunux.org/auth/realms/nunux-keeper/.well-known/openid-configuration
- L'identifiant client et son secret


![](/integration/node-red-oidc-config.png?classes=border,shadow)

Il suffit ensuite de connecter un nœud HTTP classique pour effectuer l'appel
d'[API](https://api.nunux.org/keeper/api-docs/).

**Exemple:**

![](/integration/node-red-flow-sample.png?classes=border,shadow)

```json
[{"id":"51c3a06f.0cad88","type":"inject","z":"c9fcbc16.4ac74","name":"Post fake","topic":"documents","payload":"{\"origin\":\"https://tuhrig.de/generating-pdfs-with-java-flying-saucer-and-thymeleaf/\"}","payloadType":"json","repeat":"","crontab":"","once":false,"x":160,"y":260,"wires":[["45864a8.d01f2b4"]]},{"id":"45864a8.d01f2b4","type":"function","z":"c9fcbc16.4ac74","name":"POST","func":"msg.method = 'POST';\nreturn msg;","outputs":1,"noerr":0,"x":290,"y":260,"wires":[["85076194.6abfd"]]},{"id":"85076194.6abfd","type":"openid","z":"c9fcbc16.4ac74","name":"","openid":"","x":420,"y":260,"wires":[["35455354.1972ec"]]},{"id":"35455354.1972ec","type":"http request","z":"c9fcbc16.4ac74","name":"","method":"use","ret":"obj","url":"https://api.nunux.org/keeper/v2/{{{topic}}}","tls":"","x":570,"y":260,"wires":[["ebc7f4a1.c6843"]]},{"id":"ebc7f4a1.c6843","type":"debug","z":"c9fcbc16.4ac74","name":"","active":true,"console":"false","complete":"false","x":730,"y":260,"wires":[]}]
```

### Pousser des notifications vers NodeRED

Vous pouvez également utiliser les [Webhooks](../webhook) pour pousser les documents vers
NodeRED.


[twitter]: https://flows.nodered.org/node/node-red-contrib-twitter
[mastodon]: https://flows.nodered.org/node/node-red-contrib-mastodon
[telegram]: https://flows.nodered.org/node/node-red-contrib-telegrambot
[slack]: https://flows.nodered.org/node/node-red-contrib-slack
[dropbox]: https://flows.nodered.org/node/node-red-node-dropbox
[facebook]: https://flows.nodered.org/node/node-red-contrib-facebook
[pushbullet]: https://flows.nodered.org/node/node-red-node-pushbullet

