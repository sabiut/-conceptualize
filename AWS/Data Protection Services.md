1) Amazone Macie - descover and protect sensitive data
2) Aws Key management - store and manage incryption keys
3) AWS CloudHSM - hardware base key storage
4) AwS secret manager - Rotate manage and retrive secrets
5) AWS cretificate manager - manage and deploy ssl

### Infrastructure Protection
1) AWS Shield - Denial of service protection
2) AWS Web Application Firewall - Filter malicious website traffice
3) AWS Firewall Manager - Centerally manage firewall rules

### Threat Detection
1) Amaxon GuardDuty - Automatically detect threats
2) Amazon Inspector - Analyze application security
3) AWS Config - record and ecaluate configuration of resources
4) AWS Cloud Trail - Track user activity and API usages

### Identity Management
1) IAM -securly manage access to aws account
2) aws single signon -implement single signon
3) Amazon Cognito - Manage identiy inside application
4) AWS Directory services - impliment and manage Microsoft active directory
5) AWS Organization - Centrally govern and manager multiple aws account in one place


### Illustrating IAM Users
1) IAM user policy example that allow access to s3 bucket
  - Granting permissions to multiple accounts with added conditions
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddCannedAcl",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::111122223333:root",
                    "arn:aws:iam::444455556666:root"
                ]
            },
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": [
                        "public-read"
                    ]
                }
            }
        }
    ]
}


# Identitiy and Access Management(IAM) Practice