# Day 3 Learning Notes

- A trust policy controls which principal can assume an IAM role.
- A permission policy controls which AWS API actions the assumed role can perform.
- An EC2 instance receives a role through an instance profile.
- AWS STS supplies temporary, automatically rotated credentials to the instance.
- The AWS CLI credential provider chain can use the EC2 role without static access keys.
- Least privilege was verified by allowing S3 read operations and denying `s3:PutObject`.
- All temporary lab resources were removed after verification.
