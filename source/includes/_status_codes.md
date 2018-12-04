# Status Codes

The SSO API uses the following status codes:


Code | Status | Description
---------- | ------- | -------
200 | OK | Successfully retrieved or updated SSO plan(s)
201 | Created | Successfully created an SSO plan
204 | No Content | Successfully deleted an SSO plan
400 | Bad Request | Request body is malformed
401 | Unauthorized | Invalid or missing access token
403 | Forbidden | Missing required scopes for a requested operation
404 | Not Found | Failed to find the requested SSO plan
500 | Internal Server Error | The server encountered an unexpected condition which prevented it from fulfilling the request
