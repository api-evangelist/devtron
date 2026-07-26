---
name: Bulk deploy and hibernate Devtron apps
description: Trigger a bulk deployment across apps/environments and hibernate or un-hibernate them to manage cost.
api: openapi/devtron-openapi-original.yml
operations: [BulkDeploy, BulkHibernate, BulkUnHibernate, getDeploymentHistory]
---

# Bulk deploy and hibernate Devtron apps

Operate on many applications at once for release trains and cost control.

## Auth
- Send the Devtron API token in the `token` header. Bulk actions typically
  require broad RBAC (often super-admin); expect `403` otherwise.

## Steps
1. **BulkDeploy** — trigger deployment across a selected set of apps/environments
   (POST a `BulkDeployRequest` with the name include/exclude selectors).
2. **getDeploymentHistory** — verify the rollout by reading each app's deployment history.
3. **BulkHibernate** — scale selected workloads to zero to save cost off-hours.
4. **BulkUnHibernate** — bring them back before they are needed.

## Rules
- Bulk responses return per-item success/failure detail
  (`BulkActionResponse` / `BulkActionFailureDetail`) — always inspect the
  per-item results, not just the top-level status.
- Errors use the `ErrorResponse` envelope; see `errors/devtron-problem-types.yml`.
- Selection is by name include/exclude patterns — scope them tightly to avoid
  deploying or hibernating unintended apps.
