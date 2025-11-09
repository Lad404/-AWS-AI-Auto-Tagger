# 🤖 AWS AI Auto-Tagger

An automated, AI-driven resource tagging solution for AWS that uses **Amazon Bedrock** + **AWS Lambda** to dynamically infer and apply metadata tags to AWS resources such as **EC2**, **S3 buckets**, and **Lambda functions**.

This project eliminates manual tagging effort, improves compliance, and simplifies cost allocation by enforcing a consistent tagging strategy—powered by AI.

---

## 🚀 Features

- ✅ Automatically detects and tags EC2 instances
- ✅ Automatically detects and tags S3 buckets
- ✅ Uses Amazon Bedrock AI (OpenAI OSS model) to infer meaningful metadata tags
- ✅ Fallback tags when AI output fails
- ✅ EventBridge rule to auto-run every 5 minutes
- ✅ Built with cost-efficient components (Lambda + On-Demand Bedrock)
- ✅ Supports extensible resource tagging (RDS, DynamoDB, Lambda, EKS)

---

## 🏗️ Architecture
<img width="707" height="509" alt="image" src="https://github.com/user-attachments/assets/d372dc6d-3691-4602-a5ec-2525c3c5cb1a" />

Architecture Description

EventBridge Scheduler triggers a Lambda function at a fixed interval.
The Lambda function:

Uses Boto3 to list EC2 instances and S3 buckets

Calls Amazon Bedrock with a supported model (openai.gpt-oss-20b-1:0)

Parses or builds tag dictionaries

Applies tags using EC2 CreateTags, S3 PutBucketTagging, and Lambda TagResource

Components Used

AWS Lambda with Python runtime

Amazon Bedrock Runtime

Amazon EC2

Amazon S3

AWS EventBridge

Boto3 SDK

IAM roles and policies







