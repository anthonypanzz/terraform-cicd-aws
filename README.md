# Automatically Apply Terraform With AWS CodeBuild

![Screenshot 2025-05-12 235014](https://github.com/user-attachments/assets/681467cd-0347-40d8-bfb6-74d9d5505204)



## Project Description
This DevOps project demonstrates how to automatically deploy AWS infrastructure using Terraform and AWS CodeBuild. The primary goal is to integrate Infrastructure as Code (IaC) into a CI/CD pipeline that provisions resources on AWS with no manual intervention.

Using this pipeline, any update or change made to the Terraform code in the GitHub repository will trigger AWS CodeBuild to automatically apply the infrastructure changes. The infrastructure provisioned includes:

A custom VPC

Associated Subnets and Security Groups

An EC2 instance to host a web application

This approach enables a fully automated and version-controlled infrastructure provisioning workflow, increasing deployment speed, consistency, and scalability.

---

## Key Components
Terraform: For defining and provisioning AWS infrastructure as code.

AWS CodeBuild: To run scripts that install and execute Terraform commands.

GitHub: Source control for storing Terraform code and automation scripts.

S3: To store the remote state file for Terraform.

IAM: For creating users and roles with proper permissions.

---

## Implemental Steps
Created an IAM User
Created an IAM user with programmatic access and full administrative permissions to manage AWS resources and interact with CodeBuild securely.

Created and Clone GitHub Repository
Set up a GitHub repository to store all Terraform code, automation shell scripts, and build configurations.

Write and Test Terraform Scripts
Wrote modular and reusable Terraform code to provision:

A VPC

A public subnet

Internet Gateway and route table

Security group allowing SSH (port 22) and HTTP (port 80)

An EC2 instance configured to host a simple web app
![Screenshot 2025-05-12 223504](https://github.com/user-attachments/assets/cf27e54d-4d33-4622-bf22-ea70f459fed4)
![Screenshot 2025-05-12 223546](https://github.com/user-attachments/assets/ec7eb625-06e9-44bb-8b0f-2b505d0bfb10)
![Screenshot 2025-05-12 223601](https://github.com/user-attachments/assets/c37757e1-d659-4aef-9773-f84a7ac9e1e9)
![Screenshot 2025-05-12 223624](https://github.com/user-attachments/assets/7b835257-da48-4bc2-b13f-77bdb227f5de)
![Screenshot 2025-05-12 225111](https://github.com/user-attachments/assets/4f0373cf-4856-44d8-bb6b-792eee9b979e)
![Screenshot 2025-05-12 225130](https://github.com/user-attachments/assets/97101332-4fda-4c5f-b488-b63c3c8da06f)
![Screenshot 2025-05-12 225212](https://github.com/user-attachments/assets/31abcc18-fca5-425b-bdfc-7f900c5e79fe)

---


Verified the scripts locally using terraform init, plan, and apply.

Created Automation Shell Scripts
Added bash scripts to automate Terraform commands during the CodeBuild phase. The script handles init, validate, plan, and apply commands.
![Screenshot 2025-05-12 223650](https://github.com/user-attachments/assets/625fad5a-2cb1-4841-9088-985dc86e0567)

---

Created buildspec.yml for CodeBuild
![Screenshot 2025-05-12 223740](https://github.com/user-attachments/assets/cf76813e-9354-4e2c-8958-de7c71f04e20)

---

Defined the CodeBuild build phases (install and build) in a buildspec.yml file. This file instructs CodeBuild to:

Installed Terraform
![Screenshot 2025-05-12 223721](https://github.com/user-attachments/assets/82a960e3-180b-4507-9971-1f6d38dd5354)

---

Ran shell scripts to provision infrastructure

Generated GitHub Personal Access Token (PAT)
Created a PAT to allow AWS CodeBuild to authenticate with GitHub and pull the repository during build time.
![Screenshot 2025-05-12 223705](https://github.com/user-attachments/assets/cffa847d-9b90-428e-8e19-02b8df1253f0)

---

Stored Terraform State in S3
Configured Terraform to use an S3 bucket for storing the remote state file. This ensures state is preserved between builds and supports team collaboration.
![Screenshot 2025-05-12 225325](https://github.com/user-attachments/assets/409f19da-7290-40b8-9ace-0ebe6dc53a95)

---

Created AWS CodeBuild Project
Configured a new CodeBuild project:

Connected it to the GitHub repository using the PAT

Used the aws/codebuild/standard:7.0 image

Pointed to the buildspec.yml for instructions

Assigned an IAM role with permissions to access EC2, VPC, S3, and GitHub
![Screenshot 2025-05-12 225822](https://github.com/user-attachments/assets/83ac6319-881a-45ef-ac3a-d7b06112d4f9)
![Screenshot 2025-05-12 225727](https://github.com/user-attachments/assets/d4733056-12fb-4dee-90d4-b07a0b5315ca)


---

## Final Outcome
With all components in place, any change committed to the GitHub repository now triggers AWS CodeBuild. CodeBuild automatically pulls the latest Terraform code, executes it, and applies the infrastructure changes on AWS.

This automation streamlines the infrastructure provisioning process, eliminates manual errors, and supports rapid DevOps practices by enabling consistent and repeatable deployments.
![Screenshot 2025-05-12 223026](https://github.com/user-attachments/assets/e42124b1-c605-4f0a-8ee3-936033a8f1a6)
![Screenshot 2025-05-12 223056](https://github.com/user-attachments/assets/d6ba555a-31a8-4f27-b26d-a36eee1a0ce9)
![Screenshot 2025-05-12 223113](https://github.com/user-attachments/assets/5221b50e-86b1-42b3-8aad-d5b8d5b22339)
![Screenshot 2025-05-12 223132](https://github.com/user-attachments/assets/5fbb45f2-8737-4846-89bd-b9e1805c6b54)
![Screenshot 2025-05-12 224416](https://github.com/user-attachments/assets/e29e495a-ba27-4664-beba-9fd5a42bcd34)
![Screenshot 2025-05-12 225042](https://github.com/user-attachments/assets/0020484e-1e05-4bde-816c-a2e07fe61c02)
![Screenshot 2025-05-12 224937](https://github.com/user-attachments/assets/72cb9592-fac3-498e-bd22-2cb1d92046cc)
![Screenshot 2025-05-12 224955](https://github.com/user-attachments/assets/46a17634-2b6e-4c0e-ad16-33f72c3b37a4)


---

## Key Benefits
Infrastructure as Code (IaC) automation

Continuous integration for infrastructure

Version-controlled infrastructure using GitHub

Scalable, repeatable, and fast deployments

Secure handling of state files using S3

---

## Conclusion
This project illustrates how to integrate Terraform with AWS CodeBuild to create a seamless CI/CD pipeline for infrastructure automation. It promotes DevOps best practices by automating infrastructure changes through GitHub version control and AWS native tools, enabling faster and safer deployments.
