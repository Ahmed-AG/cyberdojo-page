---
layout: reads
title:  "Installing CDF"
date:  2022-07-20
author: "Ahmed Abugharbia"
author_link: "https://twitter.com/aagsec"
---

## Introduction
Cloud Deployment Framework (CDF) automatically builds secure deployment piplines using AWS CodePipeline and CodeBuild.

<i class="fab fa-github"></i> [Cloud Deployment Framework](https://github.com/Ahmed-AG/cdf){:target="_blank"}


## Requirements
You will need the following on your local machine:
1. Python3
2. awscli
3. cdk: run the Bootstrapping process four at [https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html](https://docs.aws.amazon.com/cdk/v2/guide/bootstrapping.html)
```bash
cdk bootstrap aws://ACCOUNT-NUMBER-1/REGION-1
```
4. docker

## Configuration
1. Clone the repo

```bash
git clone https://github.com/Ahmed-AG/cdf.git
```

2. Rename `config.d.templates` to `config.d`
3. Edit `config.d/config.json` to set pipelines names, sources, deployment options, and any parameters needed

Sample config.json file:

```bash
{
    "pipelines" :[
        {
            "name" : "Production-Pipeline1",
            "provider" : "aws",
            "source" : {
                "source_type" : "codecommit",
                "repo_name" : "cdf-repo1",
                "branch" : "main"
            },
            "deployment" : {
                "assume_role" :{
                    "role": "TODO"
                },
                "aws_account" : "",
                "iam_policy_file" : "config.d/iam-policy.json",
                "region" : "us-east-1",
                "type" : "cfn",
                "parameters" : "VpcCIDR=10.0.0.0/16 Region=$REGION",
                "capabilities" : "CAPABILITY_IAM CAPABILITY_NAMED_IAM",
                "deployment_file" : "main.yaml",
                "checks" : [
                    "general_all",
                    "cfn_nag", 
                    "checkov"
                ]
            }
        }
    ]
}
```
4. Edit the IAM policy file used by the pipeline to deploy resources `config.d/iam-policy.json`
   Note: This file is referenced in `config.d/config.json`. It is recomended to have different policies for each pipeline

5. Run:
```bash
cdk deploy --all
```
6. Verify that your pipelines were created in Codepipline in AWS console