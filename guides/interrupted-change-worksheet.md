# Interrupted Terraform change: evidence worksheet

Use this to prepare a recovery decision with the workspace owner. It is not a universal recovery algorithm and does not authorize another apply, state replacement or unlock.

## First separate the questions

“The command failed” does not identify how far the operation progressed. Resource operations, remote state persistence and lock handling have separate outcomes. Preserve the original runner and records while the responsible team establishes those outcomes.

| Question | What to record internally | What it does not establish by itself |
| --- | --- | --- |
| Was a resource request dispatched? | Original runner records and exact execution interval. | Absence of a local success message does not establish absence of a cloud-side change. |
| What exists in the approved resource scope now? | Authorized independent readback and relevant original events. | Current configuration alone may not identify every historical action. |
| Which state snapshot is currently remote? | Backend object/version reference and state lineage/serial where available. | A serial alone is not enough to prove which bytes were committed. |
| Is a retained candidate state available? | Its origin, associated execution and byte reference. | A candidate file is not proof that it was safely committed. |
| Did a state write receive a known outcome? | Request/result records and corresponding backend observations. | A lost response does not establish that the write failed. |
| Is any writer still active? | Runner/process evidence and the agreed ownership mechanism. | A stale-looking lock is not proof that no writer can resume. |
| Who owns each lock? | Lock reference, expected owner and coordinated disposition. | Another run failing to obtain a lock does not authorize deleting it. |

## Record the actual situation

| Observation | Decision still required |
| --- | --- |
| Evidence supports no resource dispatch | Determine whether only local cleanup remains and who may perform it. |
| Cloud-side changes occurred but state persistence is unresolved | Identify the exact resulting resources and the candidate state before choosing a recovery path. |
| State-write response was lost | Reconcile backend observations with the original request and candidate; do not infer failure from the missing response. |
| A competing writer or external lock is present | Resolve ownership with that team before any recovery action. |
| Original runner evidence or candidate state is missing | Record the unresolved facts and escalate to the workspace owner. |

These rows organize questions, not automatic permission to perform the next write. Backend behavior, tool versions and your organization's procedures determine the actual recovery method.

## Handoff record

- Original change and approved scope:
- Workspace owner and recovery decision owner:
- Tool and provider versions:
- Last confirmed remote snapshot:
- Retained candidate and its provenance:
- Cloud resources independently observed:
- Known active writers and locks:
- Missing facts:
- Proposed recovery action and separate approval:
- Post-recovery configuration, state and application checks:

Keep this completed record private. Terraform state and plan files can contain sensitive data; a display-level sensitive marker is not a reason to publish them. See [Terraform sensitive-data guidance](https://developer.hashicorp.com/terraform/language/manage-sensitive-data).

For S3-specific configuration and locking behavior, use the documentation for your deployed version. The [S3 backend reference](https://developer.hashicorp.com/terraform/language/backend/s3) describes locking and recommends bucket versioning for recovery from accidental deletion and human error. Versioning is a recovery aid; it does not itself decide which snapshot is correct after a partially completed change.
