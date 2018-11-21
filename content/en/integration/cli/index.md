+++
title = "With the CLI"
description = "How to use the CLI to interact with the shell"
weight = 4
+++

Nunux Keeper has a native CLI.

![](images/cli.png?classes=border,shadow)

This CLI can be downloaded [here][keeper-cli-releases].

You can refer to the [project page][keeper-cli] for more details.

First, you must connect to get the access token:

```bash
$ keeper-cli login foo@gmail.com
Password of foo@gmail.com:
User foo@gmail.com logged.
```

You can now interact with the API:

```bash
$ # Get your profile
$ keeper-cli profile
Profile:
 UID:   foo@gmail.com
 Name:  John Doe
 Date:  2017-08-30T20:12:03.459Z
 Admin: true
$ # Get the last document (using JSON as output format):
$ keeper-cli document ls --json --size=1 | jq .
$ # Create a new document
$ echo "Hello World!" | keeper-cli document create --title="test"
Document:
 Id:          5bf046167d21e908224bfde3
 Title:       Test
 ContentType: text/html
 Content:     hello world

 Origin:
 Date:        2018-11-17T16:47:18.584Z
$ # And more...
$ keeper-cli --help
```

[keeper-cli-releases]: https://github.com/nunux-keeper/keeper-cli/releases
[keeper-cli]: https://github.com/nunux-keeper/keeper-cli

