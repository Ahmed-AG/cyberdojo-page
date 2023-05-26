---
layout: reads
title:  "Moving to the cloud - Skills wise"
date:   05-25-2023
author: "Ahmed Abugharbia - Assisted by AI"
author_link: "https://twitter.com/aagsec"
---

## Introduction
Securing public clouds is not fundamentally different from securing traditional networks at a high level. The same principles still apply. However, there are significant technical differences that need to be considered. One of the key distinctions is the required skills set for effectively securing public clouds like `AWS`, `Azure`, and `GCP`.

A major challenge in cloud security is the paradigm of building and maintaining everything through code. This poses a significant hurdle for many cybersecurity professionals who may not have extensive experience with coding in their day-to-day work. In the cloud, the concept of "everything as code" also necessitates the use of different tools such as [git](https://git-scm.com){:target="_blank"}, [Jenkins](https://www.jenkins.io){:target="_blank"}, [Jira](https://jira.atlassian.com){:target="_blank"}, and others.

This article is based on the author's personal experience transitioning from traditional security to cloud security. Its aim is to provide a suggested roadmap for acquiring the necessary skills to excel in cloud security. While some of these skills may not initially appear directly related to security, it is crucial to remember that <b>we cannot secure what we don't understand.</b> The depth to which one should explore each topic is an individual decision, typically based on the available time. It is recommended to cover the basics of all these topics and then delve deeper into each one as time permits.

## Linux

Our first skill is [Linux](https://en.wikipedia.org/wiki/Linux){:target="_blank"}. Linux knowledge serves as the fundamental cornerstone across various computer science disciplines. It holds significant importance in traditional security and becomes indispensable in the realm of cloud security.

It is enough to say that every tool mentioned in this article operates on Linux. While some of these tools may have Windows support, it often proves more sensible to run them on Linux. Additionally, Linux being the predominant operating system for running these tools, a solid understanding of Linux facilitates easier comprehension of troubleshooting steps and tutorials shared by others. This aspect is not be underestimated.

When it comes to learning Linux, there are endless resources, ranging from YouTube videos to concise online tutorials. Udemy offers numerous excellent classes, and considering a certification like CompTIA Linux+ might not be a bad idea to enhance one's proficiency in Linux.

## Cloud(s)

The next logical progression involves selecting one or more cloud providers and delving into understanding their workings. Each provider offers a range of training and certification paths that align with their offerings. It is recommended to start with pursuing these certifications. Also, unless you are in a management or sales role, it is advisable to skip the AWS Certified Cloud Practitioner and instead begin with the AWS Certified Solutions Architect - Associate. The former certification is too basic for our purposes.

While studying cloud technologies, it is essential to cover the core services provided by the chosen provider(s). Additionally, it is crucial to gain proficiency in utilizing command-line interfaces such as `awscli` and `az`. It is also important to start learning how to deploy using infrastructure as code, for instance, through tools like `CloudFormation`. We should not be deploying things manually in the cloud.


## Source Code Management (SCM)
Now that we've started working with code, it's important to learn about Source Code Management (SCM) or Version Control. SCM is a system that keeps track of changes to files, especially source code. It allows collaboration among multiple people, maintains a history of modifications, and makes merging changes easier. [git](https://git-scm.com){:target="_blank"} is a popular version control system widely used in software development.

As cloud security professionals, we'll need to deploy certain infrastructure components as code, which means we also need to learn Git. Even if deployment isn't our primary responsibility, understanding how cloud engineers manage code is crucial for providing security recommendations.

An additional reason for learning about SCMs, is the fact that SCMs bring about security risks. One notable concern is the potential for secrets, such as keys or passwords, to be inadvertently pushed by engineers and stored within the SCM. This makes SCM systems an attractive target for attackers, and makes it our job to protect SCMs.

Learning Git can be challenging for many security professionals. However, once you grasp the basics, create a GitHub repository or two, and start working with it, using Git will become second nature.

To get started, you can refer to these resources:

- Git documentation: [https://git-scm.com/doc](https://git-scm.com/doc){:target="_blank"}
- Introduction to version control video: [https://git-scm.com/video/what-is-version-control](https://git-scm.com/video/what-is-version-control){:target="_blank"}

## Infrastrucure as code
Having acquired essential foundational tools, we can now dig deeper into Infrastructure as Code (IaC). For AWS, mastering [CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html){:target="_blank"} is crucial. However, it is equally valuable to learn a cloud-agnostic IaC tool, considering the likelihood of working with multiple cloud platforms as security professionals. Learning a tool like [Terraform](https://www.terraform.io){:target="_blank"} is highly recommended.

To effectively learn Terraform, it is best to engage in a project that allows hands-on experience. If you don't have a specific project in mind, create one as a learning exercise.

The [Terraform website](https://developer.hashicorp.com/terraform/intro){:target="_blank"} itself is the ideal starting point for your Terraform journey. It offers comprehensive resources and guidance to facilitate your understanding of the tool and its usage.

## DevOps Concepts (CI/CD)
DevOps is a broad topic encompassing various practices and tools. To gain an introduction, I recommend watching [this](https://www.youtube.com/watch?v=Xrgk023l4lI){:target="_blank"} video, which provides a useful overview.

Continuous Integration and Continuous Delivery/Deployment or `CI/CD` is a crucial aspect of DevOps. It involves continuously adding code and automatically delivering or deploying it to production. This approach enables fast and efficient deployments.

Initially, when starting with Infrastructure as Code (IaC), we often deploy directly from our computers by running commands such as `terraform plan` and `terraform apply`. However, in production environments, deployment pipelines are typically utilized. Tools like [Jenkins](https://www.jenkins.io){:target="_blank"}, [AWS CodePipeline](https://aws.amazon.com/codepipeline/){:target="_blank"}, [Azure DevOps](https://azure.microsoft.com/en-us/products/devops/){:target="_blank"}, and [Github Actions](https://docs.github.com/en/actions){:target="_blank"} act as orchestrators, creating deployment pipelines to move code from repositories to production. This is where our `Linux` knowledge will come in very handy.

When organizations embrace DevOps practices, they usually rely on a suite of tools, including orchestrators and others. As security professionals, it is important for us to learn these tools for several reasons. Firstly, we can utilize the same tools to deploy our own infrastructure. Secondly, we need to understand the risks associated with these tools and how to secure them. Lastly, we can leverage these tools to enforce secure deployments, ensuring that security measures are embedded throughout the deployment process.


## To be continued..
- Scripting
- Configuration Management
- Containers
- Container Orchestration
  
<!--  
## Devops concepts

## Infrastrucure as code
### Cloudformation
### Terraform

## Scripting
### bash
### Pythong

## Configuration Management

## Containers

## Container Orchestration -->