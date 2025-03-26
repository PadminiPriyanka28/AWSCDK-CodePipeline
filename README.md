# **AWS CDK Project: CI/CD Pipeline with AWS CodePipeline**

## **Project Overview**
This project demonstrates how to use the **AWS Cloud Development Kit (CDK)** to create a **CI/CD pipeline** using **AWS CodePipeline**. The pipeline automates the deployment of three AWS resources:
1. **Amazon S3 Bucket** - A simple bucket to store static files or code artifacts.
2. **AWS Lambda Function** - A basic Lambda function triggered by an event (S3 in this case).
3. **Amazon DynamoDB Table** - A table for CRUD operations.

The CI/CD pipeline is configured using AWS CodePipeline, which automatically deploys these resources whenever changes are pushed to the GitHub repository.

## **Table of Contents**
1. [Prerequisites](#prerequisites)
2. [Project Setup](#project-setup)
3. [Deploying the Application](#deploying-the-application)
4. [Testing the Pipeline](#testing-the-pipeline)
5. [Resources](#resources)

## **Prerequisites**
Before you begin, ensure you have the following tools installed and configured:
- **AWS Account** - Either your personal or lab account.
- **AWS CLI** - Installed and configured with your credentials (`aws configure`).
- **AWS CDK** - Installed globally: `npm install -g aws-cdk`.
- **Node.js** - Version 14 or higher is recommended.
- **Git** - For source control.
- **GitHub** - A repository to store the project files.

Ensure that you have configured your GitHub account and linked it to your AWS CodePipeline.

## **Project Setup**

### **1. Clone the GitHub Repository**
Clone the repository to your local machine:
```sh
git clone https://github.com/PadminiPriyanka28/AWSCDK-CodePipeline.git
cd AWSCDK-CodePipeline
```

### **2. Install Dependencies**
Install the required dependencies for the project:
```sh
npm install
```

### **3. AWS CDK Initialization**
Run the following command to initialize the AWS CDK environment:
```sh
cdk bootstrap
```

This will set up the necessary CloudFormation resources in your AWS environment.

### **4. Define Resources in CDK**
The project defines the following resources using AWS CDK in `lib/my-cdk-project-stack.ts`:
- **Amazon S3 Bucket** (`MyFirstBucket`) to store static files.
- **AWS Lambda Function** (`MyLambda`) to log events when triggered.
- **Amazon DynamoDB Table** (`MyTable`) for basic CRUD operations.

### **5. Build and Deploy with AWS CDK**
To deploy the resources, use the following CDK command:
```sh
cdk deploy
```
This command synthesizes the CloudFormation template and deploys the stack. It will create the S3 bucket, Lambda function, and DynamoDB table in your AWS account.

## **Deploying the Application with AWS CodePipeline**
The deployment pipeline is created using **AWS CodePipeline** to automate the process. The pipeline uses **GitHub** as the source, **AWS CodeBuild** to build the project, and **CloudFormation** to deploy resources.

### **Steps to Set Up CodePipeline:**
1. **Source Stage**: Links to your GitHub repository to pull the CDK code.
2. **Build Stage**: Uses **AWS CodeBuild** to build and synthesize the CloudFormation template.
3. **Deploy Stage**: Uses **AWS CloudFormation** to deploy the resources.

### **`buildspec.yml` Explanation:**
The `buildspec.yml` defines the build steps for CodeBuild:
```yaml
version: 0.2

phases:
  install:
    commands:
      - npm install -g aws-cdk
      - npm install
  build:
    commands:
      - cdk synth

artifacts:
  files:
    - '**/*'
```

### **GitHub Integration**
After pushing changes to GitHub, **AWS CodePipeline** will automatically trigger and deploy the updated resources.

## **Testing the Pipeline**
### **Step 1: Modify Lambda Function**
Make any changes to any resource in `lib/assignment2-stack.ts`

### **Step 2: Push Changes to GitHub**
```sh
git add .
git commit -m "Updated changes"
git push origin main
```

### **Step 3: Verify Deployment**
Check **AWS CodePipeline** for the execution of the pipeline:
- The pipeline should trigger automatically.
- Once completed, check the AWS resources (S3, Lambda, DynamoDB) to verify the changes.

## **Resources**
1. **AWS CDK Documentation**: [https://docs.aws.amazon.com/cdk/latest/guide](https://docs.aws.amazon.com/cdk/latest/guide)
2. **AWS CodePipeline Documentation**: [https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
3. **BuildSpec Reference**: [https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)


