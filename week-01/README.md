# Week 1 - Cloud Fundamentals & Account Setup

## Files

- MFA enabled: `mfa-enabled.png`
- Budget alert created: `zero-spend-budget.png`

## What I learned

The AWS root user owns the AWS account and has unrestricted access, so I protect it with MFA and avoid using it for everyday work. An IAM user represents a person or workload inside the account and should receive only the permissions needed for its job. I use my IAM administrator user for normal AWS console and CLI work instead of signing in as root. AWS is responsible for security of the cloud, including the physical data centers, hardware, and core infrastructure. I am responsible for security in the cloud, including IAM permissions, MFA, data, network settings, and application configuration. Regions are separate geographic areas, Availability Zones are isolated locations within a Region, and Edge Locations help deliver content closer to users. The shared responsibility model means AWS and the customer each secure different parts of the overall system.

## Verification notes

- Root MFA tested by signing out and signing back in.
- Zero spend budget created with my email as an alert recipient.
- Daily work account: `rachel-admin`.
- CLI verification: `aws sts get-caller-identity`.