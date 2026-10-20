# Week 2 - IAM & Security Foundations

## Policy files

- `policies/S3UploaderOnly-rachel.json`

## Policy explanation

The `S3UploaderOnly-rachel` policy allows the attached identity to call `s3:PutObject` and `s3:GetObject`. Both actions are limited to objects whose keys are inside `my-training-bucket-rachel`, represented by the `/*` suffix in the resource ARN. The policy does not allow `s3:ListAllMyBuckets` or `s3:ListBucket`, so `aws s3 ls --profile s3test` should return `AccessDenied`. It also does not allow deleting objects, changing bucket settings, or accessing objects in another bucket. The policy is identity based because it is attached directly to the `s3-test-user` IAM user. The permission is implemented as a customer managed policy so it can be reused and reviewed separately from the user. An explicit deny from another applicable policy would override this allow because explicit denies always win during policy evaluation.

## Week 2

- IAM Access Analyzer created.
- Expected fresh account result: `0 active findings`.
- Test profile created for `s3-test-user`.
- `aws s3 ls --profile s3test` returned `AccessDenied`.
- Policy tested against the exact bucket/object ARN.