# Data Protection Services
1) Amazone Macie - descover and protect sensitive data
2) Aws Key management - store and manage encryption keys
3) AWS CloudHSM - hardware base key storage
4) AWS secret manager - Rotate manage and retrieve secrets
5) AWS certificate manager - manage and deploy ssl

### Infrastructure Protection
1) AWS Shield - Denial of service protection
2) AWS Web Application Firewall - Filter malicious website traffic
3) AWS Firewall Manager - Centrally manage firewall rules

### Threat Detection
1) Amaxon GuardDuty - Automatically detect threats
2) Amazon Inspector - Analyze application security
3) AWS Config - record and evaluate configuration of resources
4) AWS Cloud Trail - Track user activity and API usages

### Identity Management
1) IAM -securely manage access to AWS account
2) AWS single sign on -implement single sign on
3) Amazon Cognito - Manage identity inside application
4) AWS Directory services - implement and manage Microsoft active directory
5) AWS Organization - Centrally govern and manager multiple AWS account in one place


### Illustrating IAM Users
1) IAM user policy example that allow access to s3 bucket
  - Granting permissions to multiple accounts with added conditions
  
![S3 Bucket example](https://github.com/sabiut/-conceptualize/blob/master/AWS/s3.png)



# Identity and Access Management(IAM) Practice

## Manage and Inline Policy
manage policy are predefined policy define by AWS while inline policy are custom policy that are define by a user. The inline policy can be define for a group or individual user 
### Inline Policy
![S3 Inline Policy example](https://github.com/sabiut/-conceptualize/blob/master/AWS/inlinepolicy.png)

# Three Types of Storage

-   File (Amazon EFS, Amazon FSx)
-   Block (Amazon EBS)
-  Objects (Amazon s3)

# Data Transfer

-  AWS Storage Gateway
- AWS DataSync
- AWS Transfer Family