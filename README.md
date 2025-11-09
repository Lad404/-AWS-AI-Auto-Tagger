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



