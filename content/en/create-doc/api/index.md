+++
title = "Use the API"
description = ""
weight = 4
+++

All Nunux Keeper features are available thru the API.

You can fin the API documentation [here](https://api.nunux.org/keeper/api-docs/).

You can access the document creation API in 2 ways:

- Using an API key
- By declaring an API client and using tokens with a short lifespan
  (OpenID Connect protocol)

## Using an API key

This first method is not very secure and only allows limited access to the API.
However, this method is the simplest and still allows you to create a document.

You can get your API key on the settings page:

![](images/api-key.png)

{{% notice warning %}}
The API key is only displayed once (when created).
If you lose this key, you will have no choice but to generate another one.
{{% /notice %}}

The API key is used as a password for basic HTTP authentication:

```bash
$ http https://api:KEY@api.nunux.org/keeper/v2/documents
origin="http://example.org/foo.html" title="My title"
```

## Using OpenID Connect

This method allows access to the entire API.
However, it requires you to declare an API client and then obtain a temporary
access token from the OpenID Connect authentication provider
(Keycloak in our case).

There can be several types of API clients.
The GUI only allows you to configure a Web-based API client.
If you want another type of client, please use your own OpenID Connect
authentication provider.

Go to the settings page to declare a Web API client:

![](images/create-api-client.png)

You must provide:

- A name
- One or more valid redirection URLs (used after authentication)
- One or more original URLs (original URLs allowed for CORS access)

Once the information has been set and validated, you will obtain setting needed
to configure your OIDC client:

- Discovery URL
- Clinet ID
- And client secret

![](images/edit-api-client.png)

