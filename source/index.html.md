---
title: SSO API Reference

language_tabs:
  - shell

includes:
  - workflows
  - plans
  - status_codes

search: true
---

# Introduction

SSO Tile provides a Plan API for managing SSO Plans via `https://sso-api.YOUR-SYSTEM-DOMAIN`.
System operators can use the Plan API to automate plan creation, retrieval, update, and deletion.

# Authentication

SSO Plan API uses an OAuth2 access token to access the API. An access token capable of using all the Plans API, can be created with one of the following scope combinations:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Base scopes**      | `cloud_controller.admin` <br> `zones.write` <br> `scim.write` <br> `scim.read`

For all API calls, you must include `Authorization: Bearer YOUR_ACCESS_TOKEN` as a request header. For example, to get all plans,

`curl https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans" -H "Authorization: Bearer YOUR_ACCESS_TOKEN"`

## Creating an Automation Client

```
$ uaac client add example-sso-client --secret sso-client-secret --authorized_grant_type client_credentials --authorities "cloud_controller.admin,zones.write,scim.write,scim.read"
```

On the right, we show how to create a client using `uaac client add`. Please see the scopes required per endpoint to determine the appropriate authorities to give to your client.

To create clients you must do so with a user or client containing any of the following scope combinations:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `uaa.admin`
**Zones UAA Admin**  | `zones.uaa.admin`
**Base scopes**      | `clients.read` <br> `clients.write`


You may also create a client directly from UAA using their API. Please see: [Clients > Create](http://docs.cloudfoundry.org/api/uaa/)

## Acquiring an access token

```
# Using UAA CLI with UAA User
$ uaac target login.YOUR-SYSTEM-DOMAIN
$ uaac token owner get CLIENT_ID USERNAME -p PASSWORD -s CLIENT_SECRET
# Note: You must create your own client that allows the scopes required
$ uaac context
```

```
# Using CF CLI with UAA Client
$ cf api api.YOUR-SYSTEM-DOMAIN
$ cf auth CLIENT_ID CLIENT_SECRET --client-credentials
$ cf oauth-token
```

```
# Using UAA CLI with UAA Client
$ uaac target login.YOUR-SYSTEM-DOMAIN
$ uaac token client get CLIENT_ID -s CLIENT_SECRET
$ uaac context
```

Access tokens may be retrieved in many ways. On the right, we show common approaches to
authenticating against the appropriate UAA and retrieving an access token. For command line usage, it is helpful to extract the token into an environment variable, such as `$SSO_TOKEN`.

You may also fetch a token directly from UAA using their API. Please see the supported grant types: [Token](http://docs.cloudfoundry.org/api/uaa/)
