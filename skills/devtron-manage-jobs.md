---
name: Create and list Devtron jobs
description: Create or clone a Devtron job, list jobs, and inspect a job's CI pipeline.
api: openapi/devtron-openapi-original.yml
operations: [createOrCloneJob, listJobs, getJobCiPipelineList]
---

# Create and list Devtron jobs

Manage Devtron Jobs (pipeline-driven tasks that run outside the app deploy flow).

## Auth
- Send the Devtron API token in the `token` header with Devtron Apps / Jobs RBAC.

## Steps
1. **createOrCloneJob** — create a new job or clone an existing one (POST a
   `CreateJob` body; set the source job id when cloning).
2. **listJobs** — retrieve the job list (`JobListResponse`) to confirm creation.
3. **getJobCiPipelineList** — read the CI pipelines attached to the job.

## Rules
- Responses and errors follow the platform conventions in
  `conventions/devtron-conventions.yml`; errors use the `ErrorResponse` envelope.
- Cloning copies pipeline config — review the cloned CI pipeline via
  `getJobCiPipelineList` before triggering it.
