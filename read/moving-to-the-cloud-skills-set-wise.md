---
layout: reads
title:  "moving-to-the-cloud-skills-set-wise"
date:   2023-05-25
author: "Ahmed Abugharbia - Assisted by AI"
author_link: "https://twitter.com/aagsec"
---

Cloud Secuirty Skills

## Introduction
Securing public clouds is not fundamentally different from securing traditional networks at a high level. The same principles still apply. However, there are significant technical differences that need to be considered. One of the key distinctions is the required skill set for effectively securing public clouds like AWS, Azure, and GCP.

A major challenge in cloud security is the paradigm of building and maintaining everything through code. This poses a significant hurdle for many cybersecurity professionals who may not have extensive experience with coding in their day-to-day work. In the cloud, the concept of "everything as code" also necessitates the use of different tools such as git, Jenkins, Jira, and others.

This article is based on the author's personal experience transitioning from traditional security to cloud security. Its aim is to provide a suggested roadmap for acquiring the necessary skills to excel in cloud security. While some of these skills may not initially appear directly related to security, it is crucial to remember that "we cannot secure what we don't understand." The depth to which one should explore each topic is an individual decision, typically based on the available time. It is recommended to cover the basics of all these topics and then delve deeper into each one as time permits.

## Linux

Linux knowledge serves as the fundamental cornerstone across various computer science disciplines. It holds significant importance in traditional security and becomes indispensable in the realm of cloud security.

It is worth noting that every tool mentioned in this article operates on Linux. While some of these tools may have Windows support, it often proves more sensible to run them on Linux. Additionally, Linux being the predominant operating system for running these tools, a solid understanding of Linux facilitates easier comprehension of troubleshooting steps and tutorials shared by others. This aspect should not be underestimated.

When it comes to learning Linux, there are endless resources, ranging from YouTube videos to concise online tutorials. Udemy offers numerous excellent classes, and considering a certification like CompTIA Linux+ might not be a bad idea to enhance one's proficiency in Linux.

## Cloud(s)

The next logical progression involves selecting one or more cloud providers and delving into understanding their workings. Each provider offers a range of training and certification paths that align with their offerings. It is recommended to start with pursuing these certifications. ALso, unless you are in a management or sales role, it is advisable to skip the AWS Certified Cloud Practitioner and instead begin with the AWS Certified Solutions Architect - Associate. The former certification is too basic for our purposes.

While studying cloud technologies, it is essential to cover the core services provided by the chosen provider(s). Additionally, it is crucial to gain proficiency in utilizing command-line interfaces such as `awscli` and `az`. It is also important to start learning how to deploy using infrastructure using code, for instance, through tools like `CloudFormation`. We should not be deploying things manually in clouds.


## Source Code Management (SCM)
Now that we've started working with code, it's important to learn about Source Code Management (SCM) or Version Control. SCM is a system that keeps track of changes to files, especially source code. It allows collaboration among multiple people, maintains a history of modifications, and makes merging changes easier. `git` is a popular version control system widely used in software development.

As cloud security professionals, we'll need to deploy certain infrastructure components, which means we also need to learn Git. Even if deployment isn't our primary responsibility, understanding how cloud engineers write code is crucial for providing security recommendations.

An additional reason for learning about SCMs, is the fact that SCMs bring about security risks. One notable concern is the potential for secrets, such as keys or passwords, to be inadvertently pushed by engineers and stored within the SCM. This makes SCM systems an attractive target for attackers, and makes it our job to protect SCMs.
Learning Git can be challenging for many security professionals. However, once you grasp the basics, create a GitHub repository or two, and start working with it, using Git will become second nature.

To get started, you can refer to these resources:

- Git documentation: [https://git-scm.com/doc](https://git-scm.com/doc){:target="_blank"}
- Introduction to version control video: [https://git-scm.com/video/what-is-version-control](https://git-scm.com/video/what-is-version-control){:target="_blank"}

## Devops concepts

## Infrastrucure as code
### Cloudformation
### Terraform

## Scripting
### bash
### Pythong

## Configuration Management

## Containers

## Container Orchestration