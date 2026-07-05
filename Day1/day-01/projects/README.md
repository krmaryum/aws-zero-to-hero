# README – Day 1 AWS Hands-on Practice Notes

## Overview

This README explains the four Day 1 AWS hands-on study note files.

These files cover the practical part of AWS Day 1, including:

- AWS CLI configuration
- EC2 instance creation
- IAM user, access key, AWS CLI, and S3 mini project
- S3 bucket access, prefix/folder listing, and file upload using AWS CLI

Together, these notes build a strong beginner foundation for AWS practical work.

---

## Files Covered

| No. | File | Topic | Purpose |
|---:|---|---|---|
| 1 | `day-1-aws-cli-configure-study-notes.md` | AWS CLI Configure | Learn how to configure AWS CLI using IAM user credentials |
| 2 | `day-1-aws-ec2-create-study-notes.md` | EC2 Instance Creation | Learn how to create an EC2 virtual server from AWS Console |
| 3 | `day-1-aws-mini-project-iam-cli-s3-study-notes.md` | IAM + AWS CLI + S3 Mini Project | Learn how IAM user, access key, CLI, and S3 bucket work together |
| 4 | `day-1-aws-s3-cli-bucket-access-upload-study-notes.md` | S3 CLI Practice | Learn how to list S3 buckets, list prefixes, and upload files using AWS CLI |

---

# 1. AWS CLI Configure Study Notes

## File Name

```text
day-1-aws-cli-configure-study-notes.md
```

## Summary

This file explains how to configure AWS CLI using an IAM user access key.

It covers:

- What AWS CLI is
- Why AWS CLI needs credentials
- How to run `aws configure`
- How to enter Access Key ID and Secret Access Key
- How to set default region
- How to set output format
- How to verify identity using `aws sts get-caller-identity`
- How AWS CLI stores credentials and config files

## Important Commands

```bash
aws configure
aws sts get-caller-identity
aws s3 ls
ls -la ~/.aws
cat ~/.aws/config
cat ~/.aws/credentials
```

## Key Learning

```text
AWS CLI connects the terminal to AWS using IAM user credentials, region, and output format.
```

---

# 2. EC2 Create Study Notes

## File Name

```text
day-1-aws-ec2-create-study-notes.md
```

## Summary

This file explains how to create an Amazon EC2 instance from the AWS Console.

It covers:

- What EC2 is
- EC2 as IaaS
- How to launch an EC2 instance
- Choosing AMI
- Choosing instance type
- Creating/selecting key pair
- Configuring security group
- Configuring storage
- Verifying instance state
- Optional SSH connection

## Important Commands

```bash
ssh -i key-name.pem ubuntu@public-ip
ssh -i key-name.pem ec2-user@public-ip
chmod 400 key-name.pem
whoami
hostname
cat /etc/os-release
```

## Key Learning

```text
Amazon EC2 allows users to create virtual servers in AWS within minutes without buying physical hardware.
```

---

# 3. IAM + AWS CLI + S3 Mini Project Notes

## File Name

```text
day-1-aws-mini-project-iam-cli-s3-study-notes.md
```

## Summary

This file explains a complete beginner mini project where an IAM user named `ali` is created, given S3 permission, configured in AWS CLI, and used to list S3 buckets.

It covers:

- Creating IAM user `ali`
- Attaching `AmazonS3FullAccess`
- Creating an access key
- Configuring AWS CLI
- Creating S3 bucket
- Verifying CLI identity
- Listing S3 buckets
- Uploading/downloading test files
- Cleanup and security steps

## Important Commands

```bash
aws configure
aws sts get-caller-identity
aws s3 ls
aws s3 ls s3://ali--s3-t
echo "Hello from AWS Day 1 project" > day1.txt
aws s3 cp day1.txt s3://ali--s3-t/
aws s3 cp s3://ali--s3-t/day1.txt downloaded-day1.txt
cat downloaded-day1.txt
```

## Key Learning

```text
IAM controls identity, policies control permissions, AWS CLI sends commands, and S3 stores files in the cloud.
```

---

# 4. S3 CLI Bucket Access and Upload Notes

## File Name

```text
day-1-aws-s3-cli-bucket-access-upload-study-notes.md
```

## Summary

This file explains how to access an S3 bucket from an EC2 Ubuntu terminal using AWS CLI, list a folder-like prefix, and upload a file.

It covers:

- Listing all S3 buckets
- Listing contents of a bucket
- Understanding `PRE`
- Listing S3 prefixes/folders
- Using quotes for S3 paths with spaces
- Using `--recursive`
- Creating a local `test.txt` file
- Uploading file to S3 with `aws s3 cp`
- Verifying upload from CLI

## Important Commands

```bash
aws s3 ls
aws s3 ls s3://ali-s3-t1
aws s3 ls "s3://ali-s3-t1/Prophet-Muhammad PBUH/"
aws s3 ls s3://ali-s3-t1 --recursive
echo "Test from EC2 CLI" > test.txt
aws s3 cp test.txt "s3://ali-s3-t1/Prophet-Muhammad PBUH/"
```

## Key Learning

```text
S3 folders are prefixes, and S3 paths with spaces must be wrapped in quotes when using AWS CLI.
```

---

# Recommended Study Order

Study these files in this order:

| Order | File | Why |
|---:|---|---|
| 1 | AWS CLI Configure | CLI must be configured before running AWS commands |
| 2 | EC2 Create | EC2 gives hands-on compute/server practice |
| 3 | IAM + CLI + S3 Mini Project | Connects identity, permission, CLI, and S3 |
| 4 | S3 CLI Bucket Access and Upload | Gives deeper S3 CLI practice |

---

# Main Concepts Covered

| Concept | Meaning |
|---|---|
| IAM User | AWS identity used to access services |
| IAM Policy | Defines what actions a user can perform |
| Access Key | Credentials used for CLI/programmatic access |
| AWS CLI | Command-line tool to manage AWS services |
| EC2 | Virtual server in AWS |
| AMI | Template used to create EC2 instance |
| Security Group | Virtual firewall for EC2 |
| S3 Bucket | Main storage container in S3 |
| S3 Object | File stored in S3 |
| S3 Prefix | Folder-like path in S3 |
| `PRE` | Prefix shown in AWS CLI output |
| `--recursive` | Lists all objects inside bucket/prefix |

---

# Common Commands Cheat Sheet

## AWS CLI

```bash
aws configure
aws sts get-caller-identity
```

## EC2 SSH

```bash
chmod 400 key-name.pem
ssh -i key-name.pem ubuntu@public-ip
ssh -i key-name.pem ec2-user@public-ip
```

## S3

```bash
aws s3 ls
aws s3 ls s3://bucket-name
aws s3 ls s3://bucket-name --recursive
aws s3 cp file.txt s3://bucket-name/
aws s3 cp s3://bucket-name/file.txt .
```

## S3 Path with Spaces

```bash
aws s3 ls "s3://bucket-name/folder with spaces/"
aws s3 cp test.txt "s3://bucket-name/folder with spaces/"
```

---

# Common Errors and Fixes

| Error | Reason | Fix |
|---|---|---|
| `Unable to locate credentials` | AWS CLI is not configured | Run `aws configure` |
| `InvalidAccessKeyId` | Wrong access key | Recreate key and configure again |
| `SignatureDoesNotMatch` | Wrong secret key | Re-enter secret key carefully |
| `AccessDenied` | IAM user lacks permission | Attach required IAM policy |
| `NoSuchBucket` | Bucket name is wrong | Verify bucket name |
| SSH permission denied | Wrong key or username | Use correct `.pem` file and username |
| Bad permissions on key file | Key file permissions too open | Run `chmod 400 key-name.pem` |
| S3 path fails with spaces | Path was not quoted | Wrap full S3 path in quotes |

---

# Security Reminders

Never share or upload:

```text
Access Key ID
Secret Access Key
~/.aws/credentials
.pem private key
.env files with secrets
```

If a key is exposed:

1. Go to AWS Console.
2. Open IAM.
3. Select the user.
4. Open Security credentials.
5. Deactivate/delete the exposed key.
6. Create a new key only if needed.
7. Run `aws configure` again.

---

# Cleanup Reminder

To avoid unwanted charges:

- Stop or terminate unused EC2 instances.
- Delete unused EBS volumes.
- Delete unused Elastic IPs.
- Remove test files from S3.
- Delete unused S3 buckets if not needed.
- Monitor AWS billing.

Example S3 cleanup:

```bash
aws s3 rm s3://bucket-name/file.txt
aws s3 rb s3://bucket-name --force
```

---

# Final Summary

These four files complete the Day 1 AWS hands-on practice foundation.

They explain how to configure AWS CLI, create an EC2 instance, connect IAM permissions with S3 access, and perform real S3 CLI operations such as listing buckets, listing prefixes, uploading files, and verifying results.

```text
AWS CLI = Terminal access to AWS
IAM = Identity and permissions
EC2 = Virtual server
S3 = Cloud object storage
```

Alhamdulillah, these notes provide a strong practical base for moving into Day 2.
