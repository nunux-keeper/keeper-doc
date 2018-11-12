+++
title = "Via la CLI"
description = "Comment utiliser la CLI pour interagir avec le shell"
weight = 4
+++

Nunux Keeper dispose d'une CLI sous forme d'un binaire natif.

![](/integration/cli.png?classes=border,shadow)

Cette CLI peut être téléchargée [ici][keeper-cli-releases].

Vous pouvez vous référer à la [page du projet][keeper-cli] pour de plus amples détails.

Vous devez, dans un premier temps, vous connecter afin d'obtenir le jeton
d'accès:

```bash
$ keeper-cli login foo@gmail.com
Password of foo@gmail.com:
User foo@gmail.com logged.
```

Vous pouvez maintenant interagir avec l'API:

```bash
$ # Lire son profil
$ keeper-cli profile
Profile:
 UID:   foo@gmail.com
 Name:  John Doe
 Date:  2017-08-30T20:12:03.459Z
 Admin: true
$ # Récupérer le dernier document (en JSON):
$ keeper-cli document ls --json --size=1 | jq .
$ # Créer un document
$ echo "Hello World!" | keeper-cli document create --title="test"
Document:
 Id:          5bf046167d21e908224bfde3
 Title:       Test
 ContentType: text/html
 Content:     hello world

 Origin:
 Date:        2018-11-17T16:47:18.584Z
$ # Et plus...
$ keeper-cli --help
```

[keeper-cli-releases]: https://github.com/nunux-keeper/keeper-cli/releases
[keeper-cli]: https://github.com/nunux-keeper/keeper-cli

