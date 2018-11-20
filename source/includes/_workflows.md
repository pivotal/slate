# Workflows

## Give plan access to an org
`cf enable-service-access p-identity -p PLAN_NAME -o ORG_NAME`

## Give plan access to all orgs
`cf enable-service-access p-identity -p PLAN_NAME`

## Remove plan access from an org
`cf disable-service-access p-identity -p PLAN_NAME -o ORG_NAME`

## Remove plan access from all orgs
`cf disable-service-access p-identity -p PLAN_NAME`
