# Cloud Deployment Framework (CDF) Project - Beta
## Overview
Cloud Deployment Framework (CDF) provides an automated, cloud native, and secure way to deploy cloud resources. 
Based on JSON configuration files, CDF uses AWS CDK to automatically create Codepipeline Pipelines that clone repos, run secrutiy checks on code, and deploy resources. It will also build any needed docker containers for Codebuild Projects

![alt text](https://github.com/Ahmed-AG/cdf/blob/v0-1/cdf.jpg?raw=true)

## Supported tools
### Deployment tools
Infrastructure as Code Tools  | Link |
--- | --- |
Cloud Formation | https://aws.amazon.com/cloudformation/
Terraform (Coming soon) | https://www.terraform.io

### Security testing tools
Tools | Description | Link |
--- | --- | --- |
cfn_nag | The cfn-nag tool looks for patterns in CloudFormation templates that may indicate insecure infrastructure | https://github.com/stelligent/cfn_nag
checkov (Coming soon) | Checkov uses a common command line interface to manage and analyze infrastructure as code (IaC) scan results across platforms such as Terraform, CloudFormation, Kubernetes, Helm, ARM Templates and Serverless framework | https://www.checkov.io
Semgrep (Coming soon) | Static analysis at ludicrous speed Find bugs and enforce code standards | https://semgrep.dev
