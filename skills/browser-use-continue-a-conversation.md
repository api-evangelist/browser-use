---
name: browser-use-continue-a-conversation
description: >-
  Keep one Browser Use session alive across multiple runs, queue follow-up turns, cancel a turn that
  has not started yet, and persist files between turns in a workspace.
api: browser-use:browser-use-api-v4
base_url: https://api.browser-use.com/api/v4
operations:
  - create_workspace_workspaces_post
  - upload_workspace_files_workspaces__workspace_id__files_upload_post
  - create_run_runs_post
  - list_sessions_sessions_get
  - get_session_sessions__session_id__get
  - queue_session_message_sessions__session_id__queue_post
  - list_session_queue_sessions__session_id__queue_get
  - cancel_queued_message_sessions__session_id__queue__message_id__delete
  - purge_session_sessions__session_id__purge_post
generated: '2026-08-29'
method: generated
source: >-
  openapi/browser-use-api-v4-openapi.json + https://docs.browser-use.com/cloud/agent/sessions +
  https://docs.browser-use.com/cloud/agent/workspaces
---

# Continue a Browser Use conversation across runs

## 1. Create a workspace for anything that must survive the turn

`POST /workspaces` (`create_workspace_workspaces_post`), then
`POST /workspaces/{workspace_id}/files/upload`
(`upload_workspace_files_workspaces__workspace_id__files_upload_post`). A 409 means one or more files
would replace existing workspace files — rename or delete first.

## 2. Start the first run bound to that workspace

`POST /runs` (`create_run_runs_post`) with `workspaceId`. The response gives you a `sessionId`; there is
no separate session-create operation in v4.

## 3. Queue the follow-up

`POST /sessions/{session_id}/queue` (`queue_session_message_sessions__session_id__queue_post`). Read the
queue back with `list_session_queue_sessions__session_id__queue_get`.

A 429 here means the session message queue is full — drain it before enqueuing more.

## 4. Take a turn back before it runs

`DELETE /sessions/{session_id}/queue/{message_id}`
(`cancel_queued_message_sessions__session_id__queue__message_id__delete`) works **only while the
message is still pending**. Once it has been picked up you get 409 "The message is no longer pending
and cannot be cancelled." That 409 is the edge of the reversal window — check it, do not assume.

## 5. Clean up

`POST /sessions/{session_id}/purge` (`purge_session_sessions__session_id__purge_post`) is destructive
with no published restore path. So is `delete_workspace_file_workspaces__workspace_id__files_delete`.
`delete_workspace_workspaces__workspace_id__delete` archives rather than hard-deletes and is idempotent
for missing, archived and foreign ids — but no restore operation is published, so treat it as final too.

## Gotchas

- Starting a second run against a session that already has an active run returns 409.
- Zero Data Retention projects cannot use v4 at all (403 on 15 operations).
