# AWS KMS change-control field guide

Practical review worksheets for teams managing KMS access with Terraform. Use them to separate an approved change, the resulting configuration, observed application behavior, and the evidence you can hand to another engineer.

[中文说明](README.zh-CN.md)

## Start with a question

| Your question | Read this |
| --- | --- |
| We revoked a grant. What should we check before closing the change? | [KMS authorization and revocation checklist](guides/kms-change-checklist.md) |
| An apply was interrupted. Which facts do we need before deciding how to recover? | [Interrupted-change evidence worksheet](guides/interrupted-change-worksheet.md) |
| Can our team hand the work to another engineer without retelling the incident? | Fill in the worksheet locally and review the evidence references together. |

These documents can be used with your existing tools. They contain no executable recovery procedure and do not require an account, installation, AWS access or a software purchase. Keep completed worksheets in your own environment.

## A small example

An operator removes a grant and sees a successful API result. That establishes a result for that request. Closing the access-change task may also require checking the intended grant, other applicable permission paths, the required application operations, and the agreed observation window. Those are distinct questions.

The checklist gives each question its own evidence field. An unknown stays unknown; it is not silently converted into a pass.

## Contribute a correction

Open an issue for a documentation correction or an anonymized conceptual example. Include public references when possible. Do not upload state, plans, credentials, cloud logs or customer identifiers. This project is not an emergency support channel.

## Optional software demonstration

The maintainer also develops customer-hosted **AWS KMS governance and audit software**. The evaluation covers three separate tasks:

| Task | Delivery and acceptance |
| --- | --- |
| Terraform key, role and permission governance | Plan-bound approvals, separate administrative/audit duties, independent readback, revocation and bounded recovery. New-resource and existing-workspace workflows have different entry points. |
| Management contracts with native application SDK calls | Business applications call AWS KMS directly. A fixed reference application is checked before and after permission changes; customer application compatibility is verified separately. |
| CloudTrail intake, storage and audit | Scoped collection or original-file intake, retained originals plus normalized records, queries, an HTML report and independently verifiable exports. Collection and file import are distinct paths. |

[View the product evaluation site](https://kms.seacompasslabs.com/) · [Evaluate each of the three functions](https://kms.seacompasslabs.com/#review)

Demonstrations distinguish offline service models from separately identified records of our own AWS tests. Neither is a customer production reference. Independent people, customer applications and production acceptance require deployment-specific evidence. Historical source-field gaps remain visible; account-wide completeness and a continuous collection SLA are not claimed.

Request a 20-minute demonstration through the [Demo or partner conversation issue template](https://github.com/wankael987-spec/kms-change-control-guide/issues/new?template=demo-request.md), or email [wankael987@gmail.com](mailto:wankael987@gmail.com) for a private initial conversation. State only your role and the general task. GitHub issues and replies are public; do not include customer identifiers, logs, plans, state or credentials. Email is also not a channel for sending credentials.

Software installation, terms and distribution are arranged separately. This repository contains documentation only: no product source, binaries or real AWS experiment materials. A repository visit, star or demonstration request is not evidence of a paid customer.

## References

- [AWS KMS grants](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html)
- [Terraform S3 backend](https://developer.hashicorp.com/terraform/language/backend/s3)
- [Terraform sensitive data](https://developer.hashicorp.com/terraform/language/manage-sensitive-data)

Reviewed: 2026-11-15. AWS and Terraform are third-party products; this guide is independent and does not imply their endorsement.
