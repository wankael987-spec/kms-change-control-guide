# KMS authorization and revocation review worksheet

Use this worksheet inside your organization. It organizes evidence for a scoped change; it is not an assertion that all possible permission paths have been enumerated. Collection and tests need the resource owner's authorization.

## Define the change before checking it

| Field | Internal record |
| --- | --- |
| Change reference and responsible owner | |
| Approved account, region, key and principal scope | |
| Intended allowed operations and required encryption context | |
| Operations expected to fail after revocation | |
| Existing workspace, state reference and tool versions | |
| Required observation window and propagation deadline | |
| Reviewer and final acceptance owner | |

Keep exact identifiers in your internal record. A public example should describe the scenario without reproducing identifiers or files.

## Before execution

| Question | Evidence to retain | Outcome: confirmed / unknown / not applicable |
| --- | --- | --- |
| Does the approved plan describe the intended change? | The reviewed plan reference and its binding to the workspace and input state. | |
| Is the applicant distinct from the required approvers? | Your identity and approval-system records. Two signing keys alone do not establish two people. | |
| Is there a single agreed writer and locking procedure? | Workspace owner, runner, coordination window and lock mechanism. | |
| Is the prior application behavior recorded? | Approved test operation, actual identity, result and time. | |

## After authorization or revocation

| Question | Evidence to retain | Outcome |
| --- | --- | --- |
| Did the intended resource change? | Independent configuration readback, including the actual grant identity where applicable. | |
| Has the required application behavior been observed? | The agreed test call, identity/session, result and observation time. | |
| Were expected denial cases checked? | Wrong or missing context tests only when relevant to the agreed policy; keep actual request receipts. | |
| Were other applicable authorization paths considered? | Scope of reviewed key policy, IAM policy and grants, plus explicitly excluded or unknown paths. | |
| Does revocation cover the required session scenarios? | Results for the agreed existing and new sessions; include timing. | |
| Did the workspace return to its intended baseline? | State and configuration comparison, and disposition of remaining locks or unresolved work. | |

AWS considers grants together with key policies and IAM policies. Grant changes are eventually consistent. Therefore define what must be observed and when before declaring a scoped revocation complete. Removing a grant does not remove data that a caller has already obtained. See [AWS grant documentation](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html).

## Evidence handoff

| Question | Internal answer |
| --- | --- |
| Where are the original execution records and independent readbacks? | |
| Which CloudTrail files, regions, sources and time window were included? | |
| Which calls have independent request IDs or other defensible correlations? | |
| Which fields or events remain missing? | |
| Does the conclusion concern configuration, observed behavior, or both? | |
| Who accepts unresolved items and what remains outside the conclusion? | |

An API denial establishes an observed result, not necessarily the unique policy statement that caused it. A file checksum supports byte comparison against the retained reference, not the cloud origin of the bytes. Retain these distinctions in the handoff.

## Completion statement

Use a bounded statement such as:

> For the approved change and observation window, we confirmed the listed configuration and application tests. The evidence references and unresolved items are recorded above. No conclusion is made about excluded accounts, principals, operations or time periods.

If a required answer is unknown, the corresponding acceptance item remains open. Avoid replacing that answer with a dashboard status or a successful export.
