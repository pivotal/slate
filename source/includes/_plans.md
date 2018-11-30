# Plans

## The Plan Object

```json
{
  "id": "1",
  "name": "some-plan-name",
  "description": "some-description",
  "auth_domain": "some-auth-domain",
  "instance_name": "some-instance-name"
}
```

Field | Type | Description
--------- | ------- | -----------
id | String | ID of the plan
name | String | Name of the plan
description | String | Appears as a plan feature in the Services Marketplace
auth_domain | String | Subdomain of the URL where users authenticate to access applications covered by the service plan
instance_name | String | Appears on the login page and in other user-facing content, such as email communications


## Create a Plan

> Example Request:

```shell
curl -X POST "https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans" \
  -H "Authorization: Bearer some-token" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "some-plan-name",
    "description": "some-description",
    "auth_domain": "some-auth-domain",
    "instance_name": "some-instance-name"
  }'
```

> Example Response:

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": "1",
  "name": "some-plan-name",
  "description": "some-description",
  "auth_domain": "some-auth-domain",
  "instance_name": "some-instance-name"
}
```

This endpoint creates a plan.

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Base scopes**      | `cloud_controller.admin` <br> `zones.read` <br> `zones.write` <br> `scim.read` <br> `scim.write` 

### HTTP Request

`POST /v1/plans`

### Request Body Fields

Field | Type | Description
--------- | ------- | -----------
name | String | Name of the plan
description | String | Appears as a plan feature in the Services Marketplace
auth_domain | String | Subdomain of the URL where users authenticate to access applications covered by the service plan
instance_name | String | Appears on the login page and in other user-facing content, such as email communications

### Response Body

[Plan Object](#the-plan-object)

## Get a Plan by ID

> Example Request:

```shell
curl "https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans/1" \
  -H "Authorization: Bearer some-token"
```

> Example Response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": "1",
  "name": "some-plan-name",
  "description": "some-description",
  "auth_domain": "some-auth-domain",
  "instance_name": "some-instance-name"
}
```

This endpoint retrieves a plan by its ID.

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Base scopes**      | `cloud_controller.admin` <br> `zones.read` <br> `scim.read`

### HTTP Request

`GET /v1/plans/{id}`

### Request Parameters

Parameter | Type | Description
--------- | ------- | -----------
id | String | ID of the plan, which is included in the response of the [Create a Plan](#create-a-plan) endpoint.

### Response Body

[Plan Object](#the-plan-object)

## Update a Plan by ID

> Example Request:

```shell
curl -X PATCH "https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans/1" \
  -H "Authorization: Bearer some-token" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "new-plan-name",
    "description": "new-description",
    "instance_name": "new-instance-name"
  }'
```

> Example Response:

```http
HTTP/1.1 202 Accepted
Content-Type: application/json

{
  "id": "1",
  "name": "new-plan-name",
  "description": "new-description",
  "auth_domain": "old-auth-domain",
  "instance_name": "new-instance-name"
}
```

This endpoint updates a plan.

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Base scopes**      | `cloud_controller.admin` <br> `zones.read` <br> `zones.write` <br> `scim.read` <br> `scim.write` 

### HTTP Request

`PATCH /v1/plans/{id}`

### Request Parameters

Parameter | Type | Description
--------- | ------- | -----------
id | String | ID of the plan, which is included in the response of the [Create a Plan](#create-a-plan) endpoint.

### Request Body Fields
One or more of the following fields is required:

Field | Type | Description
--------- | ------- | -----------
name | String | Name of the plan
description | String | Appears as a plan feature in the Services Marketplace
instance_name | String | Appears on the login page and in other user-facing content, such as email communications

**Note**: A plan's auth domain is immutable. 

### Response Body

[Plan Object](#the-plan-object)

## Delete a Plan by ID

> Example Request:

```shell
curl -X DELETE "https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans/1" \
  -H "Authorization: Bearer some-token"
```

> Example Response:

```http
HTTP/1.1 202 Accepted
Content-Type: application/json
```

This endpoint deletes a plan by its ID.

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Base scopes**      | `cloud_controller.admin` <br> `zones.read` <br> `zones.write` <br> `scim.read` <br> `scim.write`

### HTTP Request

`DELETE /v1/plans/{id}`

### Request Parameters

Parameter | Type | Description
--------- | ------- | -----------
id | String | ID of the plan, which is included in the response of the [Create a Plan](#create-a-plan) endpoint.

## List all Plans

> Example Request:

```shell
curl -X GET "https://sso-api.YOUR-SYSTEM-DOMAIN/v1/plans" \
  -H "Authorization: Bearer some-token"
```

> Example Response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "plans": [
    {
      "id": "1",
      "name": "some-plan-name",
      "description": "some-description",
      "auth_domain": "some-auth-domain",
      "instance_name": "some-instance-name"
    },
    {
      "id": "2",
      "name": "some-other-plan-name",
      "description": "some-other-description",
      "auth_domain": "some-other-auth-domain",
      "instance_name": "some-other-instance-name"
    }
  ]
}
```

This endpoint lists all plans.

### Required Scopes
One of the following combinations of scopes is required:

Scenario             | Scopes Required
-------------------- | -----
**UAA Admin**        | `cloud_controller.admin` <br> `uaa.admin`
**Zones UAA Admin**  | `cloud_controller.admin` <br> `zones.uaa.admin`
**Zone writer**      | `cloud_controller.admin` <br> `zones.write`
**Zone reader**      | `cloud_controller.admin` <br> `zones.read`

### HTTP Request

`GET /v1/plans`

### Response Body

[Plan Object](#the-plan-object) array
