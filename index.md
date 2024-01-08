---
layout: default
---

## <a id="read"></a>Posts
- [Kubernetes Crash Course](/read/Kubernetes-crash-course.html)
- [SANS Webcast: Deep Dive: Building Security Applications with Generative AI](https://www.sans.org/webcasts/deep-dive-building-security-applications-generative-ai/){:target="_blank"}
- [Transitioning from Traditional Cybersecurity to Cloud Security: Skills You Can't Ignore](/read/transitioning-from-traditional-cybersecurity-to-cloud-security.html)
- [Running Docker remotely on kali Linux server](/read/run-docker-remotley-on-kali.md)
- [Q&A blog post: Beyond ChatGPT and using OpenAI API Q&A](https://www.sans.org/blog/how-to-build-ai-powered-cybersecurity-applications/){:target="_blank"}
- [Using jq with AWS](/read/jq-for-AWS.md)
- [SANS Webcast: Beyond ChatGPT Building Security Applications using OpenAI API](https://www.youtube.com/watch?v=Dcj2bLrgemw){:target="_blank"}
- [ACE Podcast: Ahmed Abugharbia: Upskilling your Security Teammates for Cloud and DevSecOps](https://www.sans.org/podcasts/cloud-ace/ahmed-abugharbia-upskilling-your-security-teammates-for-cloud-and-devsecops-10/){:target="_blank"}
- [بودكاست سكيوريتي بالعربي - مع أحمد أبو غربيه AI & Cybersecurity ](https://open.spotify.com/show/4SEZywCqLqOInZtVy2kqHY){:target="_blank"}
- [Installing Cloud Deployment Framework (CDF)](/read/cloud-deployment-framework.md)

---

## <a id="research-projects"></a>Projects
<!-- - [hackerBot](/projects/hackerbot.md)
- [Cloudwatch-bot](/projects/cloudwatch-bot.md) -->
### hackerBot
hackerBot is an AI-driven cybersecurity tool based on OpenAI's models, designed to perform various cybersecurity tasks. It can be run in a Docker container or installed locally. The tool is equipped with skills such as AWS CLI, port scanning using nmap, Netcat, and reading AWS logs using LangChain Agent. It allows users to execute custom commands with or without AI assistance, offering flexibility and control.

<center>
<img src="/static/hackerBot.png" alt="HackerBot searching through logs and answering questions" width="800" height="450" />
</center>

<i class="fab fa-github"></i> [hackerBot Project](https://github.com/Ahmed-AG/hackerbot){:target="_blank"}

### Cloudwatch-bot
Cloudwatch-bot is a proof-of-concept project that demonstrates how AI can be utilized to interface with security solutions. The project has a user interface that is built using HTML and JavaScript and is hosted on a public S3 bucket. The UI communicates with a backend system that includes an API Gateway and a Lambda function, which is written in Python and has permission to access OpenAI and CloudWatch. When a user makes a request, the API Gateway triggers the Lambda function, which translates the request using OpenAI into a CloudWatch query that searches for relevant information in CloudWatch logs. <a id="cloudwatch-bot-demo"></a>[Use it LIVE here.](/cloudwatch-bot.html){:target="_blank"}

<i class="fab fa-github"></i> [AWS CloudWatch-bot Sample Code](https://github.com/Ahmed-AG/Cloudwatch-bot){:target="_blank"}

---

## <a id="contact"></a>Contact
<center>
<a href="mailto:info@cyberdojo.cloud" target="_blank"><i class="fas fa-envelope"></i></a> | 
<A href="https://www.linkedin.com/in/ahmadabugharbieh/" target="_blank"> <i class="fab fa-linkedin"></i></A> | 
<A href="https://twitter.com/aagsec" target="_blank"> <i class="fab fa-twitter"></i></A>
</center>