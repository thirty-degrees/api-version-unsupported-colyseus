# API Version Unsupported

A minimal nginx service that returns a standardized error response for unsupported API versions. This service returns a JSON error message telling clients that the API version is no longer available and requires an update.

## Special case for colyseus routes

- For routes beginning with /matchmake, the error is returned in the format which colyseus expects

## Deployment

Pushes to `main` build and publish an ARM64 image tagged with the commit SHA.
After the build succeeds, the workflow sends a
`new-api-version-unsupported-colyseus-image` event to `Calfur/calfur-dev`.
That repository updates the Party Battle fallback manifest and runs its existing
Kubernetes deployment workflow. Manual builds on other branches do not deploy.

Configure the `GH_PAT_ACTIONS_TRIGGER` repository secret, or grant this repository
access to an organization secret with that name. Use a token that can dispatch
events to `Calfur/calfur-dev`; a fine-grained token needs Contents read/write access
to that target repository. The default `GITHUB_TOKEN` cannot dispatch across
repositories. See the [repository-dispatch token documentation](https://github.com/peter-evans/repository-dispatch#token).

Merge the matching event-handler change in `Calfur/calfur-dev` before enabling
this workflow. A missing trigger secret fails the deployment job with an explicit
error after the image has been published.
