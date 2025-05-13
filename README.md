## Automatically Apply Terraform With AWS CodeBuild

## Project Description
This DevOps project demonstrates how to automatically deploy AWS infrastructure using Terraform and AWS CodeBuild. The primary goal is to integrate Infrastructure as Code (IaC) into a CI/CD pipeline that provisions resources on AWS with no manual intervention.

Using this pipeline, any update or change made to the Terraform code in the GitHub repository will trigger AWS CodeBuild to automatically apply the infrastructure changes. The infrastructure provisioned includes:

A custom VPC

Associated Subnets and Security Groups

An EC2 instance to host a web application

This approach enables a fully automated and version-controlled infrastructure provisioning workflow, increasing deployment speed, consistency, and scalability.

## Key Components
Terraform: For defining and provisioning AWS infrastructure as code.

AWS CodeBuild: To run scripts that install and execute Terraform commands.

GitHub: Source control for storing Terraform code and automation scripts.

S3: To store the remote state file for Terraform.

IAM: For creating users and roles with proper permissions.

## Implemental Steps
Create an IAM User
Created an IAM user with programmatic access and full administrative permissions to manage AWS resources and interact with CodeBuild securely.

Create and Clone GitHub Repository
Set up a GitHub repository to store all Terraform code, automation shell scripts, and build configurations.

Write and Test Terraform Scripts
Wrote modular and reusable Terraform code to provision:

A VPC

A public subnet

Internet Gateway and route table

Security group allowing SSH (port 22) and HTTP (port 80)

An EC2 instance configured to host a simple web app

Verified the scripts locally using terraform init, plan, and apply.

Create Automation Shell Scripts
Added bash scripts to automate Terraform commands during the CodeBuild phase. The script handles init, validate, plan, and apply commands.

Create buildspec.yml for CodeBuild
Defined the CodeBuild build phases (install and build) in a buildspec.yml file. This file instructs CodeBuild to:

Install Terraform

Run shell scripts to provision infrastructure

Generate GitHub Personal Access Token (PAT)
Created a PAT to allow AWS CodeBuild to authenticate with GitHub and pull the repository during build time.

Store Terraform State in S3
Configured Terraform to use an S3 bucket for storing the remote state file. This ensures state is preserved between builds and supports team collaboration.

Create AWS CodeBuild Project
Configured a new CodeBuild project:

Connected it to the GitHub repository using the PAT

Used the aws/codebuild/standard:7.0 image

Pointed to the buildspec.yml for instructions

Assigned an IAM role with permissions to access EC2, VPC, S3, and GitHub

## Final Outcome
With all components in place, any change committed to the GitHub repository now triggers AWS CodeBuild. CodeBuild automatically pulls the latest Terraform code, executes it, and applies the infrastructure changes on AWS.

This automation streamlines the infrastructure provisioning process, eliminates manual errors, and supports rapid DevOps practices by enabling consistent and repeatable deployments.

## Key Benefits
Infrastructure as Code (IaC) automation

Continuous integration for infrastructure

Version-controlled infrastructure using GitHub

Scalable, repeatable, and fast deployments

Secure handling of state files using S3

## Conclusion
This project illustrates how to integrate Terraform with AWS CodeBuild to create a seamless CI/CD pipeline for infrastructure automation. It promotes DevOps best practices by automating infrastructure changes through GitHub version control and AWS native tools, enabling faster and safer deployments.
