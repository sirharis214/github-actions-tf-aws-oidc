# Overview

<img src="./images/oidc_overview.png">

[Reference](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#getting-started-with-oidc)

The above image is taken directly from githubs oidc documentaion and it does a great job explaining the overall workflow of github actions and OIDC authentication. 
To sum up the above in Layman Terms:

1. During the first few steps of a github action workflow, there must be a step where the job authenticates into our AWS account
    - the authentication method we're choosing is OIDC
    - In this auth method, AWS provide the github action job a temporary access token to be able to access the AWS account and perform actions based on the configured permissions
2. As a pre-req to github actions authentication, we must create this trust in our AWS account with github OIDC provider
    - part of the configuration in the aws account is a validation portion that the requester (action job) must meet
    - when github actions job via oidc makes a request for the access token, it carries various metadata in the request 
    - on the AWS Identity Provider configuration we can parse these various values to determine wether this job itteration should be provided the access token or not
    - --ie the repo name must be xxx and the branch name the action job is running for has to be xxx
    - Worth noting that different metadata values are sent in the request based on what triggers a github action job
        - as in a github actions job triggered based off a pull request event will carry different attributes than that ran on a push event
3. Now we create our github actions workflow to authenticate into the AWS account using OIDC which requires providing the role created in the previous step
    - after the job is complete, regardless of status - failed or successful, that access token will expire

# Configuring Trust between AWS IAM Identity Provider and GitHub OIDC Provider 
