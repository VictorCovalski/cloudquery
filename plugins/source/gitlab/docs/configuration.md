# GitLab Source Plugin Configuration Reference

## Example

This example syncs from GitLab to a Postgres destination, using API Key authentication. The (top level) source spec section is described in the [Source Spec Reference](/docs/reference/source-spec).

:configuration

See [tables](/docs/plugins/sources/gitlab/tables) for a list of supported tables.

## GitLab Spec

This is the (nested) spec used by the GitLab source plugin:

- `access_token` (string, required):
  An access token for your GitLab server. For instructions on how to generate an access token [visit the GitLab docs](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#create-a-personal-access-token).

- `base_url` (string, optional):
  URL for your self hosted GitLab server. Leave empty for GitLab SaaS. Not all tables are supported for GitLab SaaS.

- `concurrency` (int, optional, default: 10000):
  A best effort maximum number of Go routines to use. Lower this number to reduce memory usage.
