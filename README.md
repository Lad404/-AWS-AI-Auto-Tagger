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


# 🐞 Known Issues & Fixes
## ❌ max_tokens_to_sample required

Cause: Used Anthropic legacy API

✅ Fix: Use Messages API

## ❌ "prompt must start with Human:"

Cause: Using Anthropic older model

✅ Fix: Switched to openai.gpt-oss-20b-1:0

## ❌ Deployment not supported / Inference Profile required

Cause: Claude requires inference profiles

✅ Fix: Use supported ON_DEMAND model

## ❌ JSON parse errors

Model produced:

<reasoning> ... </reasoning>


✅ Fix: Strip <reasoning> tokens
✅ Clean output before parsing

## ❌ AccessDeniedException

Cause: Missing IAM permissions

✅ Fix: Add IAM actions for

EC2

S3

Lambda

Bedrock


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


# 📈 Future Enhancements

Add RDS, DynamoDB, EKS resource tagging

Include billing tags like:

BusinessUnit

OwnerEmail

EnvironmentTier

Store tagging logs in DynamoDB

Send notifications to Slack/SNS

Auto-remediation for missing tags









