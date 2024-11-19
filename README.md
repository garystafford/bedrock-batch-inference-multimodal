# Multimodal Batch Inference on Amazon Bedrock with Anthropic Claude 3.5

Explore the use of Amazon Bedrock's batch inference capabilities with multimodal models like Anthropic Claude 3.5 Sonnet to generate cost-effective bulk image descriptions.

## Bedrock Batch Inference IAM Permissions

See the AWS [documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/batch-inference-prereq.html#batch-inference-permissions) for more details.

### IAM Policy Permissions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PermissionsBatchInference",
      "Effect": "Allow",
      "Action": [
        "bedrock:ListFoundationModels",
        "bedrock:GetFoundationModel",
        "bedrock:TagResource",
        "bedrock:UntagResource",
        "bedrock:ListTagsForResource",
        "bedrock:CreateModelInvocationJob",
        "bedrock:GetModelInvocationJob",
        "bedrock:ListModelInvocationJobs",
        "bedrock:StopModelInvocationJob",
        "s3:ListBucket",
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "*"
    }
  ]
}
```

### IAM Role Trusted Entities

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Principal": {
        "Service": "bedrock.amazonaws.com"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "<your_account_id>"
        },
        "ArnEquals": {
          "aws:SourceArn": "arn:aws:bedrock:us-east-1:<your_account_id>:model-invocation-job/*"
        }
      }
    }
  ]
}
```
