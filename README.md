# GitHub Actions for Terraform CI/CD in AWS using OIDC Authentication

This repository serves as a guide to configure GitHub Actions for continuous integration and continuous deployment (CI/CD) of Terraform infrastructure to AWS. The CI/CD pipeline is designed to deploy resources to different environments based on the branch being deployed. Additionally, this repository will help configure OpenID Connect (OIDC) for authentication, providing a more secure and scalable way to manage access to AWS resources.

OIDC offers significant advantages over traditional authentication methods by dynamically generating short-lived tokens, thereby reducing the risk of credential leaks and minimizing the need for managing and rotating long-lived access keys. This guide will explain how OIDC works, walk you through its configuration, and provide official documentation links for further reading.

For more information on OIDC, you can refer to the [GitHub documentation](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect) and the[AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html).

## The Guide

[The guide](./docs/creating_cicd.md) to creating github-actions for CI/CD for deploying terraform infrastructure in AWS using OIDC Authentication.

## Overview

The branch naming convention determines the environment where the resources will be deployed:
- **Feature branches**: These branches contain Terraform code for new features or changes. When a feature branch is merged into the `dev` branch, the CI/CD workflow deploys resources to the AWS sandbox environment.
- **Dev branch**: The `dev` branch serves as the staging environment. Merging changes into this branch triggers the deployment of resources to the AWS dev environment.
- **Main branch**: The `main` branch represents the production environment. Merging changes into this branch triggers the deployment of resources to the AWS production environment.

## Getting Started

Follow these steps to set up and configure GitHub Actions for your Terraform CI/CD pipeline:

1. **Clone the Repository**: Clone this repository to your local machine to access the Terraform code and GitHub Actions workflows.

2. **Configure Terraform Code**: Write your Terraform code or use the existing code provided in the repository. Organize your code within the `build/dev/` directory for the dev environment.

3. **Set up AWS Credentials**: Configure your AWS credentials securely using GitHub Secrets. Add AWS access keys and secret access keys as secrets in your repository settings.

4. **Create GitHub Actions Workflows**: Review and customize the GitHub Actions workflows located in the `.github/workflows/` directory. These workflows define the CI/CD process, including steps to validate and deploy Terraform code.

5. **Trigger CI/CD Workflow**: Create a feature branch for your changes and open a pull request to merge into the `dev` branch. Once the pull request is merged, the GitHub Actions workflow will automatically trigger and deploy the changes to the dev environment.

6. **Monitor and Test**: Monitor the workflow execution and verify the deployment in the AWS dev environment. Test the deployed resources to ensure they meet the expected requirements.

7. **Promote to Production**: After testing in the dev environment, promote the changes to the production environment by merging the `dev` branch into the `main` branch. This action will trigger another GitHub Actions workflow to deploy the changes to the production environment.

## File Structure

The repository follows a specific file structure to organize the Terraform code and GitHub Actions workflows:

- **`.github/workflows/`**: Contains YAML files defining GitHub Actions workflows for CI/CD.
- **`build/dev/`**: Directory for Terraform code specific to the dev environment.
- **`build/prod/`**: Directory for Terraform code specific to the production environment.
- **`scripts/`**: Additional scripts or utilities used in the CI/CD pipeline.

## Feedback and Contributions

Your feedback and contributions are valuable in improving this repository and making it more useful for others. Feel free to open issues or pull requests if you have suggestions for improvements or encounter any issues. Let's collaborate to enhance our CI/CD practices with GitHub Actions and Terraform!

[The guide](#the-guide) to creating github-actions for CI/CD for deploying terraform infrastructure in AWS using OIDC Authentication.
