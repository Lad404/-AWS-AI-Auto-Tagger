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

⚙️ Components Used

AWS Lambda

Amazon Bedrock (OpenAI OSS model)

EventBridge Scheduler

IAM Roles and Permissions

CloudWatch (logging and monitoring)

EC2 + S3 sample resources

# 🔐 IAM Permissions Needed

The Lambda execution role must include:

EC2: DescribeInstances, CreateTags

S3: ListBuckets, GetBucketTagging, PutBucketTagging

Bedrock: InvokeModel

CloudWatch logs

# ⚠️ Errors Experienced & Resolutions

During development, multiple issues were encountered.
Here is a full breakdown:

Bedrock Model Errors

DeploymentNotFound / 403 Access Errors

Cause: Using Azure-style API endpoints or keys

Fix: Use AWS Bedrock runtime client with correct region

Model does not support ON_DEMAND

Cause: Attempting to use Claude Sonnet models requiring inference profiles

Fix: Switched to openai.gpt-oss-20b-1:0 with ON_DEMAND support

Invalid JSON from AI

Cause: Model includes reasoning in output

Fix: Add strict JSON extraction logic + fallback deterministic tags

Unknown character or weird output

Cause: OSS model returning additional tags

Fix: Use regex or safe parser before JSON decode

Lambda Errors

Timeout

Cause: Slow Bedrock API responses

Fix: Increase timeout to 30 seconds

AccessDenied when listing Lambda functions

Cause: Lambda role lacked lambda:ListFunctions

Fix: Remove Lambda scanning entirely to avoid unnecessary permissions

# 🧪 Testing the System
Manual Test from Lambda Console

Go to Lambda → Select your function

Go to Test tab

Use the sample event:

{
  "manual": true
}


Click Test

You should see:

EC2 and S3 resources listed

AI generating tags

Tags applied

# 🔄 Automatic Tagging via EventBridge

Open EventBridge → Rules

Create Rule

Event Source: “Schedule”

Cron expression: rate(5 minutes)

Target: Lambda function










