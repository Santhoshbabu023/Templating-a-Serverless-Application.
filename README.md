# Templating-a-Serverless-Application.
This guide helps you create and deploy a serverless application using AWS SAM with API Gateway, Lambda, and DynamoDB. You’ll set up the app locally, deploy it via CloudFormation, and manage the code in GitLab. The goal is to create a template, deploy it, and test the application’s functionality.


Serverless Application using AWS SAM
Overview
This project demonstrates how to create a serverless application using AWS SAM (Serverless Application Model), API Gateway, AWS Lambda, and DynamoDB. The application template includes a basic Lambda function, an API Gateway endpoint, and a DynamoDB table.

The project also covers how to deploy the application using CloudFormation, validate it locally, and push code to GitLab for version control.

Prerequisites
Before you begin, make sure you have the following:

AWS CLI installed and configured.
Git installed.
AWS SAM CLI installed.
GitLab Account for creating and pushing to a self-managed repository.
Access to AWS Cloud9 or a similar environment for running the project.
Setup and Deployment Steps

1. Set up AWS CloudFormation Stack
Log in to the AWS Management Console and open CloudFormation.
Create or find the stack starting with Lab Stack.
Go to the Outputs tab and copy the following values:
SamArtifactBucket
GitLabInstanceURL
GitLabInstancePassword
VsCodeEndpoint

2. Configure AWS and Check Tools
Run the following commands in your terminal:

aws configure list
git --version
sam --version
Verify that your AWS Region is set to us-east-1 and Git, SAM CLI versions are correct.

3. Initialize a New Serverless Application
In the terminal, run:

sam init

Choose the following options:
Template Source: 1 (Quick Start Templates)
Template: 1 (AWS Quick Start)
Runtime: Python 3.9
Project Name: HelloWorld

4. Review Project Files
Open the template.yaml file and verify that the HelloWorldFunction Lambda function is defined with Python 3.9 as the runtime.
Review app.py for the default Lambda function code.
Check requirements.txt for any dependencies.

5. Validate, Build, and Deploy the Application

Validate the template.yaml file:

sam validate

Build the application:

sam build

Deploy the application:

sam deploy --guided
Follow the on-screen prompts to specify the deployment settings.

6. Test the API Gateway and Lambda
After deployment, get the API Gateway URL from the CloudFormation Outputs.
Open the URL in your browser. You should see a basic "Hello World" message from the Lambda function.
Test the function with an additional query parameter:

https://<your-api-url>?id=1

7. Push Code to GitLab
Create a GitLab project named sam_application.
In the terminal, initialize a new Git repository:

git init
git add .
git commit -m "First commit"

Add the GitLab remote repository:

git remote add origin <GitLab_Repository_URL>
git push -u origin main

8. Add DynamoDB Table (DIY Section)
In the template.yaml file, add the following DynamoDB table configuration under Resources:

SimpleTable:
  Type: AWS::Serverless::SimpleTable
  Properties:
    TableName: app_table
   
Validate the updated template.yaml file:

sam validate

Rebuild and redeploy the application:

sam build
sam deploy --guided

Conclusion
By following these steps, you will have successfully created and deployed a serverless application with:

Lambda for executing code.
API Gateway to expose an HTTP endpoint.
DynamoDB for storing data.
A GitLab repository to manage the codebase.
You can further expand this application by adding more functionality or resources as needed.

Additional Notes
Ensure that your AWS credentials are properly configured before starting the deployment process.
If you're using a self-managed GitLab instance, ensure the correct repository URL and credentials are used during the Git setup steps.
The DynamoDB addition to the SAM template can be used as a starting point for more advanced integrations.
