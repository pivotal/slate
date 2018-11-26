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