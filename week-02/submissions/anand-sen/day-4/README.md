# Week 2 - Day 4: AWS Organizations and Service Control Policies

## Name

Anand Sen

## Tasks Completed

- [x] Studied AWS Organizations, organizational units (OUs), and Service Control Policies (SCPs)
- [x] Created and organized AWS accounts for separate environments
- [x] Used IAM Identity Center for account access
- [x] Attached an SCP to the Dev-Env OU
- [x] Verified that an explicit SCP deny overrides an IAM allow
- [x] Added screenshots as proof of the implementation

---

## Architecture Diagram

![AWS Organizations structure and SCP evaluation flow](./screenshots/00-scp-architecture.png)

---

## Topics Practiced

- AWS Organizations
- Root, accounts, and organizational units
- AWS IAM Identity Center
- Permission sets and AWSReservedSSO roles
- Service Control Policies (SCPs)
- Explicit deny evaluation
- AWS STS temporary credentials
- Multi-account governance

---

## What I Built

I organized AWS accounts into separate environments and used a Service Control Policy to centrally control permissions for the Dev environment.

| Resource | Value |
| --- | --- |
| Organization | AWS Organizations |
| Organizational unit | `Dev-Env` |
| SCP | `Deny-S3-Bucket-Creation` |
| Restricted action | `s3:CreateBucket` |
| Access method | IAM Identity Center |
| Permission set | `CloudAdhar-Admin` |

The SCP was attached to the `Dev-Env` OU. Any account inside this OU inherits the policy, so bucket creation is denied even when an IAM role otherwise allows the action.

---

## Part 1 - Create AWS Organization Structure

Created the AWS Organizations hierarchy with a `Root` account, a `Dev-Env` organizational unit, and the development account under the correct OU.

![AWS Organizations overview showing Root, Dev-Env OU, and member accounts](./screenshots/01-aws-organizations-overview.png)

**Result**

- Created and reviewed the AWS Organizations hierarchy.
- Organized the development account under the `Dev-Env` OU.
- Kept the management account separate from the member account.

---

## Part 2 - Centralized Account Access

Configured AWS IAM Identity Center to provide access to the AWS accounts through the AWS access portal.

![AWS access portal showing available AWS accounts and AdministratorAccess](./screenshots/02-aws-access-portal.png)

**Result**

- Access to AWS accounts is managed from one place.
- The required account and permission set are visible in the AWS access portal.
- Users can sign in without creating separate IAM users in every account.

---

## Part 3 - Attach SCP to the Dev-Env OU

Created the `Dev-Env` organizational unit and attached the `Deny-S3-Bucket-Creation` Service Control Policy directly to it.

![Dev-Env OU with the Deny-S3-Bucket-Creation SCP attached](./screenshots/03-dev-env-scp-attached.png)

**Result**

- The `Dev-Env` OU contains the development account.
- The SCP is attached directly to the OU.
- All accounts in the OU inherit the bucket-creation restriction.

---

## Part 4 - Permission Evaluation Flow

AWS evaluates permissions in layers. IAM Identity Center provides the permission set and role, while the SCP sets the maximum permissions that accounts in the OU can use.

```text
IAM Identity Center permission set
            |
            v
AWSReservedSSO role allows an action
            |
            v
SCP checks organization-level guardrails
            |
            v
Explicit SCP deny -> AccessDenied
```

**Key takeaway:** An explicit deny in an SCP always overrides an allow from an IAM policy. In this lab, `s3:CreateBucket` is denied for accounts under the `Dev-Env` OU.

---

## What I Learned

- AWS Organizations helps manage multiple AWS accounts from a central place.
- Organizational units make it easier to apply rules to groups of accounts.
- SCPs are guardrails; they define the maximum permissions available in member accounts.
- SCPs do not grant permissions by themselves.
- IAM Identity Center simplifies access management across multiple accounts.
- Explicit deny always wins during AWS permission evaluation.

---

## Security Note

No access keys, secret keys, account IDs, or other credentials are included in this submission.

---

## Cleanup

- Reviewed the accounts and OUs created for the lab.
- Kept the SCP attached only where the guardrail is required.
- Confirmed that the policy scope is limited to the `Dev-Env` OU.

---

## LinkedIn Post

[LinkedIn Link](YAHAN_APNA_LINKEDIN_POST_LINK_DAALNA)

---

[Back to Week 2](../../../README.md)
