+++
title = "With NodeRED"
description = "How to integrate Nunux Keeper with NodeRED and therefore the rest of the world"
weight = 2
+++

![](images/node-red-logo.png?classes=border,shadow)

NodeRED is an extremely powerful tool with an impressive number of connectors:

- [Twitter][twitter]
- [Mastodon][mastodon]
- [Telegram][telegram]
- [Pushbullet][pushbullet]
- [Slack][slack]
- [Dropbox][dropbox]
- [Facebook][facebook]
- et [plus](https://flows.nodered.org/)

This makes NodeRDE the best possible meditation tool.

Here are some possible usage with Nunux Keeper:

- Automatically tweet new documents
- Archive in Nunux Keeper tweets from a timeline or a search
- Send a notification to your mobile phone when a document is created
  (for example with [Pushbullet](https://www.pushbullet.com/) or
  [Pushover](https://pushover.net/))
- Send links from your devices via a push system and archive them in Nunux Keeper
- Etc.

### Use the API from NodeRED

Using the API from NodeRED requires the usage of the
[node-red-contrib-openid](https://github.com/ncarlier/node-red-contrib-openid)
module.
This module will support the authentication and refreshing of API access tokens.

First, you must declare a new API client in Nunux Keeper.
Please refer to the [section of this documentation](../../create-doc/api#with-openid-connect).

Once the customer ID and secret obtained, you can return to NodeRED, open an
OIDC node and enter the following information:

- The OIDC discovery URL: https://login.nunux.org/auth/realms/nunux-keeper/.well-known/openid-configuration
- The client ID and secret

![](images/node-red-oidc-config.png?classes=border,shadow)

Then simply connect a standard HTTP node to make
[API](https://api.nunux.org/keeper/api-docs/) call.

**Example:**

![](images/node-red-flow-sample.png?classes=border,shadow)

```json
[{"id":"51c3a06f.0cad88","type":"inject","z":"c9fcbc16.4ac74","name":"Post fake","topic":"documents","payload":"{\"origin\":\"https://tuhrig.de/generating-pdfs-with-java-flying-saucer-and-thymeleaf/\"}","payloadType":"json","repeat":"","crontab":"","once":false,"x":160,"y":260,"wires":[["45864a8.d01f2b4"]]},{"id":"45864a8.d01f2b4","type":"function","z":"c9fcbc16.4ac74","name":"POST","func":"msg.method = 'POST';\nreturn msg;","outputs":1,"noerr":0,"x":290,"y":260,"wires":[["85076194.6abfd"]]},{"id":"85076194.6abfd","type":"openid","z":"c9fcbc16.4ac74","name":"","openid":"","x":420,"y":260,"wires":[["35455354.1972ec"]]},{"id":"35455354.1972ec","type":"http request","z":"c9fcbc16.4ac74","name":"","method":"use","ret":"obj","url":"https://api.nunux.org/keeper/v2/{{{topic}}}","tls":"","x":570,"y":260,"wires":[["ebc7f4a1.c6843"]]},{"id":"ebc7f4a1.c6843","type":"debug","z":"c9fcbc16.4ac74","name":"","active":true,"console":"false","complete":"false","x":730,"y":260,"wires":[]}]
```

### Push notifications to NodeRED

You can also use [Webhooks](../webhook) to push documents to NodeRED.


[twitter]: https://flows.nodered.org/node/node-red-contrib-twitter
[mastodon]: https://flows.nodered.org/node/node-red-contrib-mastodon
[telegram]: https://flows.nodered.org/node/node-red-contrib-telegrambot
[slack]: https://flows.nodered.org/node/node-red-contrib-slack
[dropbox]: https://flows.nodered.org/node/node-red-node-dropbox
[facebook]: https://flows.nodered.org/node/node-red-contrib-facebook
[pushbullet]: https://flows.nodered.org/node/node-red-node-pushbullet

