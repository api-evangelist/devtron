---
name: Create and inspect a Devtron application
description: Create a new Devtron application, list applications, and read its metadata and labels.
api: openapi/devtron-openapi-original.yml
operations: [createApplication, listApplications, getAppMetaInfo, getAppLabels]
---

# Create and inspect a Devtron application

Use the Devtron orchestrator API to onboard and inspect an application.

## Auth
- Every call sends the Devtron API token in the `token` HTTP header.
- The token must have RBAC permission for Devtron Apps. A `401` means the token
  is missing/invalid; a `403` means it lacks the permission.
- Base URL is `https://{devtronHost}/orchestrator` (your self-hosted install).

## Steps
1. **createApplication** — create the app (POST). Supply the app name and
   project/team in the body. Handle `400` (bad payload) and `403` (no permission).
2. **listApplications** — confirm the app appears in the app listing.
3. **getAppMetaInfo** — read the created app's metadata (id, project, created-by).
4. **getAppLabels** / **listAppLabels** — read the labels applied to the app.

## Rules
- Errors return the `ErrorResponse` envelope (`code`, `status`, `errors`, `result`)
  — see `errors/devtron-problem-types.yml`.
- No idempotency-key header exists; do not blindly retry `createApplication` on a
  timeout — check `listApplications` first (see `conventions/devtron-conventions.yml`).
