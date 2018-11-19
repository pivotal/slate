# Plans

## Create a Plan

```shell
curl -X POST "http://example.com/v1/plans" \
  -H "Authorization: Bearer some-token" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "some-plan-name",
    "description": "some-description",
    "auth_domain": "some-auth-domain.com",
    "instance_name": "some-instance-name"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "id": "1",
  "name": "some-plan-name",
  "description": "some-description",
  "auth_domain": "some-auth-domain.com",
  "instance_name": "some-instance-name"
}
```

This endpoint creates a plan.

### HTTP Request

`POST /v1/plans`

### Request Fields

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name of the plan
description | String | Appears as a plan feature in the Services Marketplace
auth_domain | String | URL where users authenticate to access applications covered by the service plan
instance_name | String | Appears on the login page and in other user-facing content, such as email communications
