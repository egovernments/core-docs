---
description: >-
  DevSecOps is the philosophy of integrating security practices within the
  DevOps pipeline
---

# DevSecOps

As we scale DIGIT to a core platform and leverage the same across multiple product streams, concerns about platform security, services and the underlying Kubernetes infrastructure have increased. How do we adapt security practices for a containerized hybrid cloud environment? Security needs to be declarative, built-in, and automated. Apps need to be natively more secure. Security needs to shift left in the application life cycle. Whereas standard security practices start after the application deployment.

![Current State](<../.gitbook/assets/image (199).png>)



![Wayforward](<../.gitbook/assets/image (93).png>)

## **DevSecOps - Principles Into Practice**

![](<../.gitbook/assets/image (253).png>)

By developing security as code, we strive to create awesome products and services, provide insights directly to developers, and generally favour iteration over trying to always come up with the best answer before every release and deployment.&#x20;

We will not simply rely on scanners and reports to make code better. We will attack products and services like an outsider to defend what we've created. We will learn the loopholes, look for weaknesses, and we will work to provide remediation actions instead of long lists of problems.

We will not wait for our organizations to fall victim to mistakes and attackers. We will not settle for finding what is already known; instead, we will look for anomalies yet to be detected. We will strive to be better partners by upholding platform values.

## **How can we adapt security best practices?**

* Best practices for automating security checks and remediation.
* Hardening the container and Kubernetes infrastructure and workloads.
* Detecting and responding to runtime threats with sustained efforts.
* **Integrate security scanners for containers:** This should be part of the process for adding containers to the registry.
* **Automate security testing in the CI process:** This includes running security static analysis tools as part of builds, as well as scanning any pre-built container images for known security vulnerabilities as they are pulled into the build pipeline.
* **Add automated tests for security capabilities into the acceptance test process:** Automate input validation tests, as well as verification authentication and authorization features.
* **Automate security updates, such as patches for known vulnerabilities:** Do this via the DevOps pipeline. It should eliminate the need for admins to log into production systems while creating a documented and traceable change log.
* **Automate system and service configuration management capabilities:** This allows for compliance with security policies and the elimination of manual errors. Audit and remediation should be automated as well.

## Rules For A DevSecOps Practitioner

* Security starts with engineering, try to understand the fact developers are engineers whereas hackers are reverse engineers.
* Encourage good security hygiene in engineering.
* Continuous assessments and compliance checks.
* Real-time threat alerting across apps and services.
* Enable developers to drive iterative security changes.

## Improving The Security DNA <a href="#ab24" id="ab24"></a>

### 1. Code Analysis

* Secure the CI/CD pipeline.
* Release in small and frequent batches.
* Embed code analysis into Q/A.
* Use tools to detect that private keys or API information are not pushed on the Version Control.

### 2. Change Management

* Empower teams to improve security practices and make changes.
* Quick review and approval process.
* Changes must leave the audit trial.
* Meet compliance requirements.

### 3. Compliance Monitoring

* Enforce operational and security hygiene.
* Establish strict password policies.
* Audit everything from code pushes, pipelines and compliances.
* Monitor systems for bad behaviour.

### 4. Threat Investigations

* Monitor apps and services to detect and alert on threats.
* Instrument services to identify comprises.
* Built-in real-time alerting and controls.
* Develop ansible playbooks and response scenarios for IT and Security.

### 5. Vulnerability Checks

* Conduct vulnerability scans and practices.
* Conduct periodic scans of product build.
* Code reviews and penetration tests.
* Establish remediation SLAs.

### 6. Security Training

* Transform the team into security ninjas.
* Participate in industry conferences.
* Invest in security certifications.
* Educate employees on security risks.
* Prepare teams for incident response.

## Integrating Security Into CI/CD Workflow

![Where to introduce security in CI/CD flow](<../.gitbook/assets/image (33).png>)

### 1. Pre-commit

* [x] Lightweight, Static analysis (SAST) checking in the engineer’s IDE.
* [x] Peer code reviews (for defensive coding and security vulnerabilities).

### 2. Commit stage (Continuous Integration)

* [x] Compile and build checks, ensuring the vulnerabilities are identified in third-party components, Libraries.
* [x] Dashboard the findings and Generating Alerts on high-risk code.
* [x] Automation of unit testing of security functions, with full coverage of code analysis.

### 3. Securing artefacts

* [x] It is extremely important that we know what goes as part of our build artefacts like the libraries that we use, the container layers, the deployment configs, etc.
* [x] We also must ensure that containers installed by third-party vendors do not download and run anything at runtime.
* [x] Tools like [Docker Bench](https://github.com/docker/docker-bench-security) can help identify the container-level scanning for&#x20;
  * Kernel Security
  * Denial Of Service
  * Image Security
  * Leakage of Credentials and Secrets.
* [x] Certain parameters must be followed before using the dependencies/libraries/images:-
  * Where did the image/library come from?
  * Do you trust the creator, which kind of security policy are they using?
  * How do you know nobody has been tampering with the image?
* [x] Best Practices to follow:-
  * Being in an open-source world, do not run unverified software and/or from sources you don’t explicitly trust.
  * Deploy a container-centric trust server using some of the Docker registry servers available in our Docker Security Tools list.
  * Enforce mandatory signature verification for any image that is going to be pulled or running on your system.

### 3. QA stage

* [x] Secure, automated configuration management and provisioning using tools like Terraforms and Helm Charts.
* [x] Automated functional and integration testing of security features and Deep static analysis scanning.
* [x] Targeted dynamic scanning (DAST) as part of QA, by simulating external attacks on an application while the application is running. It attempts to penetrate an application from the outside by checking its exposed interfaces for vulnerabilities and flaws.
* [x] Here are some [free/open-source tools](https://owasp.org/www-community/Vulnerability\_Scanning\_Tools) that we can adapt as part of our QA Process for manual penetration testing using web exploitation frameworks such as [Metasploit](https://www.metasploit.com/).

### 4. Production deployment and post-deployment

* [x] Automated deployment and release orchestration.
* [x] Automated runtime asserts and compliance checks.
* [x] Production monitoring/feedback.
* [x] Bug bounties.

## Tools That Can Help The DevSecOps Way

![Open source and DevSecOps tools](<../.gitbook/assets/image (119).png>)

1. **IDE Plugins** — IDE extensions that can work like spellcheck and help to avoid basic mistakes at the earliest stage of coding (IDE is a place/program where devs write their code for those who don’t know). The most popular ones are probably [DevSkim](https://github.com/microsoft/DevSkim), [JFrog Eclipse](https://jfrog.com/blog/shift-left-with-xray-plugins/), and [Snyk](https://plugins.jetbrains.com/plugin/10972-snyk-vulnerability-scanner).
2. **Pre-Commit Hooks** — Tools from this category prevent us from committing sensitive information like credentials into the code management platform. There are some open-source options available, like [git-hound](https://github.com/ezekg/git-hound), [git-secrets](https://github.com/awslabs/git-secrets), and [repo-supervisor](https://github.com/auth0/repo-supervisor).
3. **Secrets Management Tools** allow us to control which service has access to what password specifically. Big players like AWS, Microsoft, and Google have their solutions in this space, but we will use cloud-provider-agnostic when multi-cloud or hybrid-cloud is in place.
4. **Static Application Security Testing (SAST)** is about checking source code (when the app is not running). There are many free & commercial tools in the space (see [here](https://owasp.org/www-community/Source\_Code\_Analysis\_Tools)), as the category is over a decade old. Unfortunately, they often result in a lot of false positives, and can’t be applied to all coding languages. What’s worse is that they take hours (or even days) to run, so the best practice is to do incremental code tests during the weekdays and scan the whole code during the weekend.
5. **Source Composition Analysis (SCA)** tools are straightforward — they look at libraries that we use in our project and flag the ones with known vulnerabilities. There are [dozens of them](https://owasp.org/www-community/Component\_Analysis) on the market, and they are sometimes offered as a feature of different products — e.g. [GitHub](https://docs.github.com/en/free-pro-team@latest/github/visualizing-repository-data-with-graphs/exploring-the-dependencies-of-a-repository).
6. **Dynamic Application Security Testing (DAST)** is the next one in the security chain, and the first one testing running applications (not the source code as SAST — we can read about [other differences here](https://www.synopsys.com/glossary/what-is-sast.html)). It provides fewer false positives than SAST but is similarly time-consuming.
7. **Interactive Application Security Testing (IAST)** combines SAST and DAST elements by placing an agent inside the application and performing real-time analysis anywhere in the development process. As a result, the test covers both the source code and all the other external elements like libraries and APIs (this wasn’t possible with SAST or DAST, so the outcomes are more accurate). However, this kind of testing can have an adverse impact on the performance of the app.
8. **Secure infrastructure as code** — As containers are gaining popularity, they become an object of interest for malware producers. Therefore we need to scan Docker images that are downloaded from public repositories, and tools like [Clair](https://github.com/quay/clair) will highlight any potential vulnerabilities.
9. **Compliance as code** tools will turn compliance rules and policy requirements into automated tests. To make it possible dev teams need to translate human-readable rules received from non-tech people into code, and compliance-as-a-code tools should do the rest (point out where we are breaking the rules or block updates if they are not in line with the policies).
10. **Runtime application self-protection (RASP)** allows applications to run continuous security checks and react to attacks in real time by getting rid of the attacker (e.g. closing his session) and alerting the team about the attack. Similarly to IAST, it can hurt app performance. It’s 4th testing category that I show in the pipeline (after SAST, DAST, and IAST) and [we should have at least two of them](https://www.synopsys.com/blogs/software-security/sast-iast-dast-rasp-differences/) in the stack.
11. **Web Application Firewall (WAF)** lets us define specific network rules for a web application and filter, monitor, and block HTTP traffic to and from a web service when it corresponds to known patterns of attacks e.g. [SQL injection](https://www.w3schools.com/sql/sql\_injection.asp). All big cloud providers like [Google](https://cloud.google.com/blog/products/identity-security/new-waf-capabilities-in-cloud-armor), [AWS](https://aws.amazon.com/waf/) and [Microsoft](https://azure.microsoft.com/pl-pl/blog/azure-web-application-firewall-waf-generally-available/) have got their WAF, but there are also specialised companies like Cloudflare, Imperva and Wallarm, for example.
12. **Monitoring tools** — as mentioned in [a DevOps guide](https://medium.com/inside-inovo/devops-explained-venture-capital-perspective-156c5705e774?source=collection\_home---4------2-----------------------), monitoring is a crucial part of the DevOps manifesto. DevSecOps takes it to the next level and covers not only things like downtime but also security threats.
13. **Chaos engineering**. Tools from this category allow us to test the app under different scenarios and patch holes before problems emerge. “_Breaking things on purpose is preferable to be surprised when things break_” as said by Mathias Lafeldt from Gremlin.
14. **Vulnerability management** — these tools help identify the holes in the security systems. They classify weaknesses by the potential impact of malicious attacks taking advantage of them so that one can focus on fixing the most dangerous ones. Some of the tools might come with add-ons that automatically fix found bugs. This category is full of open-source solutions, and [here we can find the top 20](https://awesomeopensource.com/projects/vulnerability-management).

