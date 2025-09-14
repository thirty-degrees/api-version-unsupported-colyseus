# API Version Unsupported

A minimal nginx service that returns a standardized error response for unsupported API versions. This service returns a JSON error message telling clients that the API version is no longer available and requires an update.

## Special case for colyseus routes

- For routes beginning with /matchmake, the error is returned in the format which colyseus expects
