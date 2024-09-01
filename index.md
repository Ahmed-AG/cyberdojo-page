---
layout: default
---
<!-- ## Welcome to Cyberdojo
My name is [Ahmed Abugharbia](https://www.linkedin.com/in/ahmedabugharbia/){:target="_blank"}, founder of Cyberdojo. my mission is to help you build robust, business-driven security programs through practical training and expert guidance.

With over 17 years in the cybersecurity field, I've worked with leading companies to solve complex security challenges. My journey started with securing networks and applications, eventually leading to cloud security, DevSecOps and finally, GenAI. As a SANS Certified instructor for [SEC540: Cloud Security and DevSecOps Automation](https://www.sans.org/cyber-security-courses/cloud-security-devsecops-automation/){:target="_blank"}, I focus on strategic planning and hands-on implementation of security controls.
Looking forward to helping you achieve your security goals!

At Cyberdojo, we offer a range of services designed to enhance your security posture. From expert training and consulting to specialized cloud security solutions, my goal is to equip you with the knowledge and tools needed for immediate, measurable improvements. I hold several industry certifications, including GIAC GSEC, GPEN, AWS Certified DevOps Engineer Professional, and AWS Certified Solutions Architect Associate.

Reach out on <a href="mailto:info@cyberdojo.cloud" target="_blank">info@cyberdojo.cloud</a>. Looking forward to helping you achieve your security goals!
---
-->
## <center> <a id="services"></a>Services </center>
---
<div style="width: 80%; margin: 0 auto; padding: 20px;">
  <table style="width: 100%; border-spacing: 20px;">
    <tr>
      <td style="padding: 20px; border: 2px solid #ddd; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); text-align: center; vertical-align: middle;">
        <h3 style="margin-bottom: 10px;">Strategic Plan</h3>
        <p>Ensures your organization’s seamless and secure transition to the cloud, aligning with your business goals.</p>
      </td>
      <td style="padding: 20px; border: 2px solid #ddd; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); text-align: center; vertical-align: middle;">
        <h3 style="margin-bottom: 10px;">Cloud Security Assessment</h3>
        <p>Conduct a thorough evaluation of your cloud infrastructure’s security posture, identifying potential risks.</p>
      </td>
    </tr>
    <tr>
      <td style="padding: 20px; border: 2px solid #ddd; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); text-align: center; vertical-align: middle;">
        <h3 style="margin-bottom: 10px;">Managed Services</h3>
        <p>Proactively manage and optimize your cloud infrastructure with ongoing monitoring, maintenance, and expert support, ensuring continuous security and operational excellence.</p>
      </td>
      <td style="padding: 20px; border: 2px solid #ddd; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); text-align: center; vertical-align: middle;">
        <h3 style="margin-bottom: 10px;">GenAI Security</h3>
        <p>Secure your AI models and data with a robust design and architecture, employing advanced threat detection, stringent access controls, and continuous monitoring to mitigate vulnerabilities and safeguard against threats.</p>
      </td>
    </tr>
  </table>
</div>

---

- **Strategic plan:** Ensures your organization’s seamless and secure transition to the cloud, aligning with your business goals.
- **Cloud Security Assessment:** Conduct a thorough evaluation of your cloud infrastructure's security posture, identifying vulnerabilities, misconfigurations, and potential risks, while providing a detailed remediation plan to fortify your defenses.
- **Managed Services:** Proactively manage and optimize your cloud infrastructure with ongoing monitoring, maintenance, and expert support, ensuring continuous security and operational excellence.
- **GenAI Security :** Secure your AI models and data with a robust design and architecture, employing advanced threat detection, stringent access controls, and continuous monitoring to mitigate vulnerabilities and safeguard against threats.

---
## <a id="research-projects"></a>Research:

### Why the focus on GenAI?
- **The Need for Security in GenAI Applications:** Generative AI (GenAI) applications are revolutionizing industries by automating tasks, generating content, and enhancing decision-making processes. However, these advancements come with significant security challenges. GenAI systems are vulnerable to various threats, including data poisoning, adversarial attacks, and misuse of generated content. Ensuring the security of GenAI applications is critical to prevent malicious exploitation, protect sensitive information, and maintain the integrity and trustworthiness of AI-generated outputs.

- **Leveraging GenAI for Enhanced Security:** The rise of GenAI is also transforming how we approach cybersecurity. GenAI tools can enhance threat detection, automate response strategies, and predict potential vulnerabilities with unprecedented accuracy. By integrating GenAI into our security frameworks, we can stay ahead of emerging threats and continuously adapt to the evolving digital landscape.

### hackerBot
hackerBot is an AI-driven cybersecurity tool based on OpenAI's models, designed to perform various cybersecurity tasks. It can be run in a Docker container or installed locally. The tool is equipped with skills such as AWS CLI, port scanning using nmap, Netcat, and reading AWS logs using LangChain Agent. It allows users to execute custom commands with or without AI assistance, offering flexibility and control.

<center>
<img src="/static/hackerBot.png" alt="HackerBot searching through logs and answering questions" width="800" height="450" />
</center>

<i class="fab fa-github"></i> [hackerBot Project](https://github.com/Ahmed-AG/hackerbot){:target="_blank"}

### Aviata-chatbot

[Aviata-chatbot](https://github.com/Ahmed-AG//aviata-chatbot){:target="_blank"} is a purposefully designed vulnerable Generative AI (GenAI) application created to investigate and analyze potential security issues that could arise in GenAI systems. By intentionally incorporating known vulnerabilities, Aviata-chatbot allows us to study a wide range of security threats, such as data breaches, adversarial attacks, unauthorized access, and the manipulation of AI outputs. This research is crucial for understanding the specific risks associated with GenAI applications and for developing effective strategies to mitigate these risks and enhance the overall security of AI-driven technologies.

<center>
<img src="https://raw.githubusercontent.com/Ahmed-AG/aviata-chatbot/feature/readme/images/aviata-chatbot.png" alt="Aviata-chatbot vulnerable GenAI application" width="800" height="450" />
</center>

<i class="fab fa-github"></i> [Aviata-chatbot Project](https://github.com/Ahmed-AG//aviata-chatbot){:target="_blank"}

### Cloudwatch-bot
Cloudwatch-bot is a proof-of-concept project that demonstrates how AI can be utilized to interface with security solutions. The project has a user interface that is built using HTML and JavaScript and is hosted on a public S3 bucket. The UI communicates with a backend system that includes an API Gateway and a Lambda function, which is written in Python and has permission to access OpenAI and CloudWatch. When a user makes a request, the API Gateway triggers the Lambda function, which translates the request using OpenAI into a CloudWatch query that searches for relevant information in CloudWatch logs. <a id="cloudwatch-bot-demo"></a>[Use it LIVE here.](/cloudwatch-bot.html){:target="_blank"}

<i class="fab fa-github"></i> [AWS CloudWatch-bot Sample Code](https://github.com/Ahmed-AG/Cloudwatch-bot){:target="_blank"}

--- 

## <a id="read"></a>Posts:
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

## <a id="contact"></a>Contact
<center>
<a href="mailto:info@cyberdojo.cloud" target="_blank"><i class="fas fa-envelope"></i></a> | 
<A href="https://www.linkedin.com/in/ahmadabugharbieh/" target="_blank"> <i class="fab fa-linkedin"></i></A> | 
<A href="https://twitter.com/aagsec" target="_blank"> <i class="fab fa-twitter"></i></A>
</center>