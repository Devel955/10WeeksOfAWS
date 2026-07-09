# Week 1 Submission - Anand Sen

**Challenge:** #10WeeksOfAWS (CloudAdhar × TrainWithShubham) — AWS SAA-C03 Prep
**Week 1 Focus:** Cloud Foundations & IAM

---

## Tasks Completed
- [x] Watched/read the weekly content
- [x] Completed hands-on labs
- [x] Added screenshots or proof
- [x] Posted on LinkedIn
- [x] Cleaned up AWS resources

## What I Built
- Secured my AWS account by enabling Root MFA and configuring Billing and Budget alerts.
- Created IAM users, groups, and roles following the principle of least privilege.
- Built and tested a custom S3 read-only IAM policy using JSON.
- Configured IAM Switch Role for temporary read-only access.
- Integrated GitHub Actions with AWS using OIDC authentication without storing long-lived AWS access keys.

## What I Learned
- AWS security best practices, including enabling Root MFA and avoiding daily use of the root user.
- How IAM users, groups, roles, and policies together implement least-privilege access.
- How to write and apply custom IAM policies using JSON for fine-grained permissions.
- Hands-on experience with IAM Switch Role and temporary AWS credentials.
- How GitHub Actions can securely access AWS using OIDC and AWS STS without storing long-lived access keys.

## LinkedIn Post
[LinkedIn Link](YAHAN_APNA_LINKEDIN_POST_LINK_DAALNA)

## Topics Practiced
- AWS account security
- Root MFA
- Billing alert
- IAM users
- IAM groups
- Least privilege
- IAM roles and OIDC-based temporary access
- GitHub OIDC with AWS
- IAM policies (JSON)
<!-- - IAM roles / Switch Role -->

---

## Lab 1 — Secure Your AWS Account

**Goal:** Create a safe AWS account foundation for the next 10 weeks.

**Steps:**
1. Create or log in to your AWS account.
2. Enable MFA on the root user.
3. Open the Billing Dashboard.
4. Turn on billing alerts / budget alerts.
5. Create an alert for estimated charges (e.g. $5).
6. Stop using root user for daily activities.

**Before creating an AWS Billing Alarm, make sure these prerequisites are completed:**

1. Enable Billing Alerts
   - Sign in as the AWS account root user, or an IAM identity with the required billing permissions.
   - Open the Billing and Cost Management console.
   - Go to Billing Preferences.
   - Enable Receive CloudWatch billing alerts.
   - Save the changes.

2. Use the North Virginia (us-east-1) AWS Region
   - Billing metrics are available only in US East (N. Virginia) (`us-east-1`).
   - Create the CloudWatch alarm in this region.

**Deliverables:**

### Root MFA enabled
![Root MFA enabled](./Root%20MFA%20enabled.png)

### Billing Alert
![Billing Alert](./Billing%20Alert.png)

### Budget Alerts
![Budget Alerts](./Budget%20Alerts.png)

### Where I Got Stuck
![CloudWatch billing alerts disabled](./cloudwatch-billing-alerts-disabled.png)

Issue: Initially, I couldn't create the Billing Alarm because CloudWatch billing alerts were not enabled and billing metrics were unavailable.

Resolution: I enabled "Receive CloudWatch billing alerts" in Billing Preferences, selected the US East (N. Virginia) (us-east-1) region, and then successfully created the Billing Alarm.

![CloudWatch billing alerts enabled](./cloudwatch-billing-alerts-enabled.png)

### Why should the AWS root user not be used daily?


- The root user has full access to the entire AWS account.
- Using it every day is risky because one mistake can affect all resources.
- If the root account is hacked, the attacker gets complete control of the AWS account.
- For daily work, we should use IAM users or IAM roles with only the required permissions.
- The root user should be used only for account setup and a few critical administrative tasks.
- MFA should always be enabled on the root account for extra security.


### Why billing should be monitored from Day 1?


- Helps avoid unexpected charges.
- Keeps AWS spending under control.
- Sends alerts when the budget limit is reached.
- Helps use AWS resources wisely.
- Makes it easier to stay within the Free Tier.

---

## Lab 2 — S3 Read-Only IAM Group and User

**Goal:** Understand IAM group-based access.

```text
Group name: S3ReadOnlyGroup
Policy: AmazonS3ReadOnlyAccess

User name: learner-s3
Added to: S3ReadOnlyGroup
```

**Test:** Logged in as `learner-s3`, confirmed S3 view/list works, confirmed a disallowed action returns Access Denied.

**Deliverables:**

### Group created & Policy Attached
![Group created and policy attached](./Group%20created%20%26%20Policy%20Attached.png)

### User Added to group
![User added to group](./User%20Added%20to%20group.png)

### Allowed S3 view action
![Allowed S3 view action](./Allowed%20S3%20view%20action.png)

### Denied Action
![Denied action](./Denied%20Action.png)

---

## Lab 3 — EC2 Read-Only Access

**Goal:** Apply least privilege to EC2.

```text
Group name: EC2ReadOnlyGroup
Policy: AmazonEC2ReadOnlyAccess

User name: learner-ec2
Added to: EC2ReadOnlyGroup
```

**Test:** Logged in as `learner-ec2`, confirmed EC2 dashboard is visible, confirmed instances cannot be created/terminated.

**Deliverables:**

### EC2ReadOnlyGroup & Policy attached
![EC2ReadOnlyGroup and policy attached](./EC2ReadOnlyGroup%20%26%20Policy%20attached.png)

### User Added to group
![User added to group](./User%20Added%20to%20group%20%282%29.png)

---

## Lab 4 — Billing View Access

**Goal:** Understand billing access with limited permissions.

```text
Group name: BillingViewGroup
Policy: AWSBillingReadOnlyAccess

User name: learner-billing
Added to: BillingViewGroup
```

**Deliverables:**

### BillingViewGroup & Policy attached
![BillingViewGroup and policy attached](./BillingViewGroup%20%26%20Policy%20attached.png)

### learner-billing cannot manage unrelated services
![learner-billing cannot manage unrelated services](./learner-billing%20user%20cannot%20manage%20unrelated%20AWS%20services.png)

---

## Lab 5 — Custom S3 Read-Only JSON Policy

**Goal:** Read and create a basic JSON policy.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME"
    },
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

**Deliverables:**

### Custom Policy Created
![Custom S3 policy](./Custom%20S3%20Policy.png)

### Policy Attached to learner-s3 user
![Policy attached to learner-s3 user](./Policy%20Attached%20to%20learner-s3%20user.png)

### Allowed action
![Allowed action](./Allowed%20action.png)

### Denied action
![Denied action](./Allowed%20action%20%282%29.png)

---

## Optional Advanced Lab — Switch Role

**Goal:** Understand role assumption and temporary access.

```text
Role name: TrainingReadOnlyRole
Policy: ReadOnlyAccess
```

**Deliverables:**

### TrainingReadOnlyRole with ReadOnlyAccess
![TrainingReadOnlyRole with ReadOnlyAccess](./TrainingReadOnlyRole%20with%20ReadOnlyAccess.png)

### Switch Role
![Switch Role](./Switch%20Role.png)

### Verify Role Access
![Verify Role Access](./Verify%20Role%20Access.png)

---

## Optional Advanced Challenge — GitHub OIDC with AWS

**Goal:** Configure secure GitHub Actions access to AWS without storing long-lived AWS access keys in GitHub Secrets.

```text
GitHub Actions
      │  OIDC Token
      ▼
AWS IAM OIDC Provider
      │
      ▼
AWS STS AssumeRoleWithWebIdentity
      │  Temporary Credentials
      ▼
AWS Resources (S3, EC2, etc.)
```

**Steps:**
1. Created a GitHub OIDC Identity Provider in AWS IAM (`token.actions.githubusercontent.com`, audience `sts.amazonaws.com`).
2. Created an IAM Role trusted by that OIDC provider, scoped to my GitHub repo, with `AmazonS3ReadOnlyAccess` attached.
3. Updated the role's trust policy to allow `sts:AssumeRoleWithWebIdentity` only from my repo.
4. Added a GitHub Actions workflow (`.github/workflows/aws-oidc-challenge.yml`) that assumes the role via OIDC and runs `aws sts get-caller-identity` and `aws s3 ls`.
5. Ran the workflow manually and confirmed the assumed-role ARN in the logs — no static AWS access keys stored anywhere in GitHub.

**Deliverables:**

### OIDC Provider
![OIDC Provider](./OIDC%20Provider.png)

### IAM Role (github-oidc-challenge-role)
![IAM Role github-oidc-challenge-role](./IAM%20Role%28github-oidc-challenge-role.png)

### OIDC Trust Policy
![OIDC Trust Policy](./OIDC%20Trust%20Policy.png)

### GitHub Action Success
![GitHub Action Success](./Github%20Action%20Success.png)

### STS Assumed Role Output
![STS Assumed Role Output](./STS%20Assumed%20Role%20Output.png)

### Validate S3 Read Access
![Validate S3 Read Access](./Validate%20S3%20Read%20Access.png)

---

## Key Takeaway
- Least privilege is not just a setting — it is a mindset.
- Every IAM user, group, and role should have only the permissions required for their job.
- Use IAM groups to manage policies centrally instead of attaching policies to individual users.
- Use IAM roles for temporary access instead of sharing long-lived credentials.
- Use OIDC for CI/CD pipelines to eliminate the need for storing AWS access keys in GitHub Secrets — this reduces the AWS account attack surface.
- Billing alerts from Day 1 avoid surprise charges and keep spend within Free Tier.
