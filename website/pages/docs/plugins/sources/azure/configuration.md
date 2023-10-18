# CloudQuery Azure Source Plugin Configuration Reference

## Example

This example connects a single Azure subscription to a single destination. The (top level) source spec section is described in the [Source Spec Reference](/docs/reference/source-spec).

:configuration

## Azure Spec

This is the (nested) spec used by the Azure source plugin.

- `subscriptions` (`[]string`) (default: empty. Will use all visible subscriptions)

  Specify which subscriptions to sync data from.

- `cloud_name` (`string`) (default: empty)

  The name of the cloud environment to use. Possible values are `AzureCloud`, `AzureChinaCloud`, `AzureUSGovernment`.
  See the [Azure CLI documentation for more information](https://learn.microsoft.com/en-us/cli/azure/manage-clouds-azure-cli).

- `concurrency` (`int`) (default: `50000`):

  A best effort maximum number of Go routines to use. Lower this number to reduce memory usage.

- `discovery_concurrency` (`int`) (default: `400`)

  During initialization the Azure source plugin discovers all resource groups and enabled resource providers per subscription, to be used later on during the sync process.
  The plugin runs the discovery process in parallel. This setting controls the maximum number of concurrent requests to the Azure API during discovery.
  Only accounts with many subscriptions should require modifying this setting, to either lower it to avoid network errors, or to increase it to speed up the discovery process.

- `skip_subscriptions` (`[]string`) (default: empty)

  A list of subscription IDs that CloudQuery will skip syncing.
  This is useful if CloudQuery is discovering the list of subscription IDs and there are some subscriptions that you want to not even attempt syncing.

- `normalize_ids` (`bool`) (default: `false`)

  Enabling this setting will force all `id` column values to be lowercase. This is useful to avoid case sensitivity and uniqueness issues around the `id` primary keys

- `oidc_token` (`string`) (default: empty)

An OIDC token can be used to authenticate with Azure instead of `AZURE_CLIENT_SECRET`. This is useful for Azure AD workload identity federation. When using this option, the `AZURE_CLIENT_ID` and `AZURE_TENANT_ID` environment variables must be set.