# Workflows

## Managing CloudFoundry Organizations for SSO Plans

```example
$ cf api api.cf.example.com
Setting api endpoint to api.cf.example.com...

$ cf auth sso-api-client sso-api-client-secret --client-credentials
API endpoint: https://api.cf.example.com
Authenticating...
OK
Use 'cf target' to view or set your target org and space.

$ cf service-access -e p-identity
Getting service access for service p-identity as ...
broker: identity-service-broker
   service      plan                 access    orgs
   p-identity   uaa                  none
   p-identity   example-all     all
   p-identity   example                 limited   org1,org2

$ cf enable-service-access p-identity -p example -o system
Enabling access to plan asdf of service p-identity for org system as ...
OK

$ cf enable-service-access p-identity -p example-all
Enabling access of plan some-auth-domain for service p-identity as ...
OK

$ cf disable-service-access p-identity -p example
Disabling access of plan example for service p-identity as ...
OK

$ cf disable-service-access p-identity -p example-all
Disabling access of plan example-all for service p-identity as ...
OK
```

In order to manage CloudFoundry Organizations for SSO Plans, we will be using
the CF cli: [https://github.com/cloudfoundry/cli](https://github.com/cloudfoundry/cli).

Please target and authenticate using the CF cli prior to running the following commands. You may authenticate using [cf login](http://cli.cloudfoundry.org/en-US/cf/login.html) or [cf auth](http://cli.cloudfoundry.org/en-US/cf/auth.html). `cf auth` is useful when authenticating as a service account.  These commands require a user with the `cloud_controller.admin` scope.

Plan names are derived from the SSO Plan's auth domain. This can be retrieved in the response for [Creating a Plan](#create-a-plan) or [Getting a Plan by ID](#get-a-plan-by-id).

### Viewing current plan access to orgs
`cf service-access -e p-identity`

### Give plan access to a specific org
`cf enable-service-access p-identity -p PLAN_AUTH_DOMAIN -o ORG_NAME`

### Give plan access to all orgs
`cf enable-service-access p-identity -p PLAN_AUTH_DOMAIN`

### Remove plan access from a specific org
`cf disable-service-access p-identity -p PLAN_AUTH_DOMAIN -o ORG_NAME`

### Remove plan access from all orgs
`cf disable-service-access p-identity -p PLAN_AUTH_DOMAIN`

## Managing Plan Administrators for SSO Plans

```example
$ uaac target login.cf.example.com

Target: https://login.cf.example.com
Context: admin, from client admin

$ uaac token client get sso-api-client -s sso-api-client-secret

Successfully fetched token via client credentials grant.
Target: https://login.cf.example.com
Context: sso-api-client, from client sso-api-client

$ uaac group get zones.7891c78f-0cbd-46ab-9205-ef6f945c8071.admin
  id: a89ff489-f910-42e9-a8fc-a40486bb5b7f
  meta
    version: 4
    created: 2018-10-30T23:09:58.000Z
    lastmodified: 2018-11-26T22:38:37.000Z
  description:
  members:
  -
    origin: uaa
    type: USER
    value: 5d09d594-546d-49fd-b8c1-986875d2b45c
  -
    origin: uaa
    type: USER
    value: 9ceb2a21-e7ca-428d-ad51-3cb5df9919fe
  schemas: urn:scim:schemas:core:1.0
  displayname: zones.7891c78f-0cbd-46ab-9205-ef6f945c8071.admin
  zoneid: uaa

$ uaac curl /Users?filter=id+eq+%225d09d594-546d-49fd-b8c1-986875d2b45c%22
{
  "resources": [
    {
      "id": "5d09d594-546d-49fd-b8c1-986875d2b45c",
      "userName": "plan-admin",
      ...
    }
  ]
}

$ uaac member add zones.7891c78f-0cbd-46ab-9205-ef6f945c8071.admin my-plan-administrator
success

$ uaac member delete zones.7891c78f-0cbd-46ab-9205-ef6f945c8071.admin my-plan-administrator
success
```

In order to manage Plan Administrators for SSO Plans, we will be using
the UAA cli: [https://github.com/cloudfoundry/cf-uaac](https://github.com/cloudfoundry/cf-uaac).

Please target and authenticate the system UAA zone using the UAA cli prior to running the following commands.
The UAA cli has many ways of fetching a token, please see `uaac token --help` for options.

For these commands, you will need to know the Plan ID.
This can be retrieved in the response for [Creating a Plan](#create-a-plan) or [Listing Plans](#list-all-plans).

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `uaa.admin`
**Zones UAA Admin**  | `zones.uaa.admin`
**Base scopes**      | `scim.read` <br> `scim.write`

### Create UAA group

The `zones.PLAN_ID.admin` group may not exist in UAA. You can run the following:

`uaac group add zones.PLAN_ID.admin`

This command may error if the group already exists, you can safely ignore the error if so.

### Viewing current plan administrators for a plan

`uaac group get zones.PLAN_ID.admin`

The response will list plan administrators by the user ID.
To view more information about the users in the response, you
may use the [UAA List Users API](https://docs.cloudfoundry.org/api/uaa).

### Grant a plan administrator access to a plan

`uaac member add zones.PLAN_ID.admin [usernames...]`


### Revoke a plan administrator access to a plan

`uaac member delete zones.PLAN_ID.admin [usernames...]`