# 🚀 SageMaker Studio Domain CloudFormation Template

This CloudFormation template sets up a **SageMaker Studio domain**, **user profile**, **JupyterLab & CodeEditor spaces**, and optionally, an **MLflow Tracking Server**. It's designed to support MLOps workflows with full lifecycle support including Canvas settings, lifecycle configurations, and custom roles.

---

## 📦 What's Included

- SageMaker Studio Domain + User Profile
- IAM Roles for Lambda, SageMaker, ServiceCatalog
- Lifecycle Config to auto-clone workshop repo
- JupyterLab & CodeEditor Spaces
- Optional MLflow Tracking Server
- Custom Lambda-backed resources (for VPC, S3 CORS, Canvas, etc.)

---

## 🛠 Parameters

| Parameter              | Default Value             | Description |
|------------------------|---------------------------|-------------|
| `UserProfileNamePrefix` | `studio-user`            | Prefix for user profile name |
| `DomainNamePrefix`      | `mlops-workshop-domain`  | Prefix for domain name |
| `JupyterLabAppInstance` | `ml.m5.2xlarge`          | Instance type for Jupyter App space |
| `OwnerID`               | `not-set`                | Owner tag for resources |
| `CreateMLflowServer`    | `YES`                    | Set to `NO` to skip MLflow server |

---

## 🚀 Deployment Instructions

### 1. Prerequisites
- AWS CLI installed and configured
- Permissions to create IAM roles, Lambda, SageMaker, etc.

### 2. Deploy the Stack

```bash
aws cloudformation deploy \
  --template-file cfnStudioDomain.yaml \
  --s3-bucket <bucket-name>
  --stack-name sagemaker-studio-deployment \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides \
    UserProfileNamePrefix=studio-user \
    DomainNamePrefix=mlops-workshop-domain \
    JupyterLabAppInstance=ml.t3.medium \
    OwnerID=vivek.t \
    CreateMLflowServer=YES
