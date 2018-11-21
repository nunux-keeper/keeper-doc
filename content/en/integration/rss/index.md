+++
title = "With RSS aggregators"
description = "How to integrate Nunux Keeper with RSS aggregators"
weight = 1
+++

Nunux Keeper natively supports the following RSS aggregators:

- [Nunux Reader](https://reader.nunux.org/welcome)
- [Miniflux](https://miniflux.app/)

With very few configurations, it is also possible to integrate:

- [Feedpushr](https://github.com/ncarlier/feedpushr)

### Nunux Reader

For Nunux Reader, simply activate the archiving service on the profile screen:

![](images/nunux-reader.png?classes=border,shadow)

{{% notice note %}}
For a self-hosted instance of Nunux Reader, it will be necessary to configure
the API client ID and secret.
{{% /notice %}}

### Miniflux

The Miniflux [official documentation](https://docs.miniflux.app/en/latest/integration.html#nunux-keeper)
explains how to perform the integration.

![](images/miniflux.png?classes=border,shadow)

### Feedpushr

![](images/feedpushr.png?classes=border,shadow)

To send Feedpushr articles to Nunux Keeper, you must obtain an API key and then
use Feedpusr's STDOUT output as follows:

```bash
$ feedpushr \
  | jq -c "select(.title) | {title:.title, content:.description, origin: .link}" \
  | while read next; do echo "$next" | http https://api:KEY@api.nunux.org/keeper/v2/documents; done
```

{{% notice tip %}}
BTW, we remind you that the pages of public labels provides an RSS feed.
It is therefore possible via Feedpushr to subscribe to this feed and
automatically send public documents to many outputs such as: Twitter, Mastodon,
etc.
{{% /notice %}}

