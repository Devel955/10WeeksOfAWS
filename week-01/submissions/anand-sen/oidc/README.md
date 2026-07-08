# GitHub OIDC with AWS

## Objective

Configure GitHub Actions to access AWS securely using OIDC without storing long-lived AWS access keys.

## AWS Configuration

- OIDC Provider: token.actions.githubusercontent.com
- Audience: sts.amazonaws.com
- IAM Role: GitHubActionsOIDCRole
- Policy: AmazonS3ReadOnlyAccess

## Repository

https://github.com/Devel955/10WeeksOfAWS

## Files

- aws-oidc-challenge.yml
- trust-policy.json

## Result

Successfully configured GitHub OIDC authentication with AWS IAM Role.
