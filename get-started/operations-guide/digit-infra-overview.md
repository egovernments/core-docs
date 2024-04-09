---
description: Operational Guidelines & Security Standards
---

# DIGIT - Infra Overview

## Objective&#x20;

The objective is to provide a clear guide for efficiently using DIGIT infrastructure on various platforms like SDC, NIC, or commercial clouds. This document outlines the infrastructure overview, operational guidelines, and recommendations, along with the [segregation of duties (SoD)](https://medium.com/@jeehad.jebeile/devops-and-segregation-of-duties-9c1a1bea022e). It helps to plan the procurement and build the necessary capabilities to deploy and implement DIGIT.

**In a shared control scenario, the state program team must adhere to these guidelines and develop their own control implementation for the state's cloud infrastructure and collaborations with partners. This ensures standardized and smooth operational excellence in the overall system.**

## DIGIT Infrastructure Overview

&#x20;DIGIT Platform is designed as a microservices architecture, using open-source technologies and [containerized](https://www.docker.com/resources/what-container) apps and services. DIGIT components/services are deployed as docker containers on a platform called [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/), which provides flexibility for running cloud-native applications anywhere like physical or virtual infrastructure or hypervisor or HCI and so on. Kubernetes handles the work of scheduling containerized services onto a compute cluster and manages the workloads to ensure they run as intended. And it substantially simplifies the deployment and management of microservices.

Provisioning the Kubernetes cluster will vary across from [commercial clouds](https://docs.google.com/spreadsheets/d/1RPpyDOLFmcgxMCpABDzrsBYWpPYCIBuvAoUQLwOGoQw/edit#gid=907731238) to state data centres, especially in the absence of [managed Kubernetes services](https://medium.com/swlh/state-of-managed-kubernetes-2020-4be006643360) like AWS, Azure, GCP and NIC. Kubernetes clusters can also be provisioned on state data centres with bare-metal, virtual machines, hypervisors, HCI, etc. However providing integrated networking, monitoring, logging, and alerting is critical for operating Kubernetes Clusters when it comes to State data centers. DIGIT Platform also offers add-ons to monitor Kubernetes cluster performance, logging, tracing, service monitoring and alerting, which the implementation team can take advantage.

Below are the useful links to understand Kubernetes:

* [Understand containers, dockers](https://medium.com/faun/containers-docker-kubernetes-introduction-part-1-fed143dafc05)
* [What is Kubernetes](https://medium.com/easyread/step-by-step-introduction-to-basic-concept-of-kubernetes-e20383bdd118) and [Architecture](https://medium.com/edureka/kubernetes-architecture-c43531593ca5)
* [Requirements to setup Kubernetes cluster](https://medium.com/faun/kubernetes-prerequisites-for-setup-kubenetes-cluster-part-2-699b3f93d6cc)
* [Provider Managed Cluster vs Self-provisioning Cluster](https://www.magalix.com/blog/provider-managed-vs.-self-managed-kubernetes)&#x20;
* [DIGIT Deployment](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/27459718/DIGIT+Deployment) on Kubernetes

### DIGIT On Kubernetes - High-Level Deployment Diagram

<img src="https://lh5.googleusercontent.com/Onn_9Fk7ePpOfEOjchCgESufKHVCRrr9gK8Pki-Csj8Pl5CxcX25rWLtVDe4JA_gLQ0jcgNIoW_Yk9UMQdzBqj2daXWH-yd84_Gv76_B-wxrosiaXav_2zUoVl0oVC4WeIJQ855OeRjIQNDYjQ49lSIe0SAOzbjE9byiTX3DQeCCiF0BsgDQtPRylOUU" alt="" data-size="original">

### DIGIT Infra Specification On SDC or NIC Or Any Commercial Cloud

| Systems                                                        | Specification                                                                                                                                | Spec/Count                               | Comment                                                          |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ---------------------------------------------------------------- |
| User Accounts/VPN                                              | Dev, UAT and Prod Envs                                                                                                                       | 3                                        | <p><br></p>                                                      |
| User Roles                                                     | Admin, Deploy, ReadOnly                                                                                                                      | 3                                        | <p><br></p>                                                      |
| OS                                                             | Any Linux (preferably Ubuntu/RHEL)                                                                                                           | All                                      | <p><br></p>                                                      |
| Kubernetes as a managed service or VMs to provision Kubernetes | <p>Managed Kubernetes service with HA/DRS</p><p>(Or) VMs with 2 vCore, 4 GB RAM, 20 GB Disk</p>                                              | <p>If no managed k8s</p><p>3 VMs/env</p> | <p>Dev - 3 VMs</p><p>UAT - 3VMs</p><p>Prod - 3VMs</p><p><br></p> |
| Kubernetes worker nodes or VMs to provision Kube worker nodes. | VMs with 4 vCore, 16 GB RAM, 20 GB Disk / per env                                                                                            | 3-5 VMs/env                              | <p>DEV - 3VMs</p><p>UAT - 4VMs</p><p>PROD - 5VMs</p>             |
| Disk Storage (NFS/iSCSI)                                       | Storage with backup, snapshot, dynamic inc/dec                                                                                               | 1 TB/env                                 | <p>Dev - 1000 GB</p><p>UAT - 800 GB</p><p>PROD - 1.5 TB</p>      |
| VM Instance IOPS                                               | Max throughput 1750 MB/s                                                                                                                     | 1750 MS/s                                | <p><br></p>                                                      |
| Disk IOPS                                                      | Max throughput 1000 MB/s                                                                                                                     | 1000 MB/s                                | <p><br></p>                                                      |
| Internet Speed                                                 | Min 100 MB - 1000MB/Sec (dedicated bandwidth)                                                                                                | <p><br></p>                              | <p><br></p>                                                      |
| Public IP/NAT or LB                                            | Internet-facing 1 public ip per env                                                                                                          | 3                                        | 3 Ips                                                            |
| Availability Region                                            | VMs from the different region is preferable for the DRS/HA                                                                                   | at least 2 Regions                       | <p><br></p>                                                      |
| Private vLan                                                   | Per env all VMs should within private vLan                                                                                                   | 3                                        | <p><br></p>                                                      |
| Gateways                                                       | NAT Gateway, Internet Gateway, Payment and SMS gateway                                                                                       | 1 per env                                | <p><br></p>                                                      |
| Firewall                                                       | Ability to configure Inbound, Outbound ports/rules                                                                                           | <p><br></p>                              | <p><br></p>                                                      |
| <p>Managed DataBase </p><p>(or) VM Instance</p>                | <p>Postgres 12 above Managed DB with backup, snapshot, logging. </p><p>(Or) 1 VM with 4 vCore, 16 GB RAM, 100 GB Disk per env.</p>           | per env                                  | <p>DEV - 1VMs</p><p>UAT - 1VMs</p><p>PROD - 2VMs</p>             |
| CI/CD server self hosted (or) Managed DevOps                   | <p>Self Hosted Jenkins : Master, Slave (VM 4vCore, 8 GB each) </p><p>(Or) Managed CI/CD:  NIC DevOps or AWS  CodeDeploy or Azure DevOps </p> | 2 VMs (Master, Slave)                    | <p><br></p>                                                      |
| Nexus Repo                                                     | Self hosted Artifactory Repo (Or) NIC Nexus Artifactory                                                                                      | 1                                        | <p><br></p>                                                      |
| DockerRegistry                                                 | DockerHub (Or) SelfHosted private docker reg                                                                                                 | 1                                        | <p><br></p>                                                      |
| Git/SCM                                                        | GitHub (Or) Any Source Control tool                                                                                                          | 1                                        | <p><br></p>                                                      |
| DNS                                                            | main domain & ability to add more sub-domain                                                                                                 | 1                                        | <p><br></p>                                                      |
| SSL Certificate                                                | NIC managed (Or) SDC managed SSL certificate per URL                                                                                         | 2 urls per env                           | <p><br></p>                                                      |

## Operational Recommendations

DIGIT strongly recommends [Site reliability engineering](https://medium.com/@alexbmeng/site-reliability-engineering-principals-fd52229bfcd6) (SRE) principles as a key means to bridge development and operations gaps by applying a software engineering mindset to system and IT administration topics.  In general, an SRE team is responsible for the availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning.

### Monitoring Tools Recommendations

Commercial clouds like [AWS](https://aws.amazon.com/cloudwatch/), [Azure](https://adinermie.com/azure-monitoring-tools-explained-part-10-network-watcher/) and GCP offer sophisticated monitoring solutions across various infra levels like CloudWatch and StackDriver. In the absence of such managed services to monitor, we can look at various best practices and tools listed below which help in [debugging and troubleshooting](https://raygun.com/blog/best-practices-microservices/) efficiently.

* [Network monitoring](https://www.dnsstuff.com/network-scanning), [Diagnosis](https://www.dnsstuff.com/network-troubleshooting-steps), [Assessment](https://www.dnsstuff.com/best-network-assessment-tools-and-network-assessment-checklist),  [Identify the latency](https://www.dnsstuff.com/network-latency)&#x20;
* [Systems](https://www.dnsstuff.com/systems)
* [Application monitoring](https://medium.com/@Alibaba\_Cloud/system-monitoring-using-prometheus-and-grafana-8007d3aaf400)
* [Web application monitoring](https://medium.com/flask-monitoringdashboard-turtorial/monitor-your-flask-web-application-automatically-with-flask-monitoring-dashboard-d8990676ce83)
* [Alert management](https://medium.com/@abhishekbhardwaj510/alertmanager-integration-in-prometheus-197e03bfabdf), [Alert Types](https://awesome-prometheus-alerts.grep.to/rules.html)
* [Distributed Tracing](https://medium.com/velotio-perspectives/a-comprehensive-tutorial-to-implementing-opentracing-with-jaeger-a01752e1a8ce)
* [Telemetry](https://medium.com/jaegertracing/jaeger-and-opentelemetry-1846f701d9f2)

## Key Standard Operating Procedures (SOPs)

* Segregation of duties and responsibilities.
* SME and SPOCs for [L1.5](https://www.quora.com/What-is-L1-5-support-in-the-IT-industry-especially-in-Cognizant-What-is-the-scope-in-this-type-of-project) support along with the SLAs defined.
* [Ticketing system](https://medium.com/swlh/incident-management-process-5655ba586cf4) to manage incidents, converge and collaborate on various operational issues.
* Monitoring dashboards at various levels like Infrastructure, networks and applications.
* Transparency of monitoring data and collaboration between teams.
* Periodic remote sync-up meetings, acceptance and attendance to the meeting.
* Ability to see stakeholders' availability of calendar time to schedule meetings.
* Periodic (weekly, monthly) summary reports of the various infra, operations incident categories.
* Communication channels and synchronization regularly and also upon critical issues, changes, upgrades, releases etc.

## Segregation Of Duties

While DIGIT is deployed at state cloud infrastructure, it is essential to identify and distinguish the responsibilities between Infrastructure, Operations and Implementation partners. Identify these teams and assign SPOC, define responsibilities and ensure the Incident Management process is followed to visualize, track issues and manage dependencies between teams. Essentially these are monitored through dashboards and alerts are sent to the stakeholders proactively. eGov team can provide consultation and training on a need basis depending on any of the below categories.

State IT/Cloud team -Refers to state infra team for the Infra, network architecture, LAN network speed, internet speed, OS Licensing and upgrade, patch, compute, memory, disk, firewall, IOPS, security, access, SSL, DNS, data backups/recovery, snapshots, capacity monitoring dashboard.&#x20;

* State program team - Refers to the owner for the whole DIGIT implementation, application rollouts, and capacity building. Responsible for identifying and synchronizing the operating mechanism between the below teams.&#x20;
* Implementation partner - Refers to the DIGIT Implementation, application performance monitoring for errors, logs scrutiny, TPS on peak load, distributed tracing, DB queries analysis, etc.&#x20;
* Operations team - this team could be an extension of the implementation team that is responsible for DIGIT deployments, configurations, CI/CD, change management, traffic monitoring and alerting, log monitoring and dashboard, application security, DB Backups, application uptime, etc.

## Skills To Setup, Operate & Maintain DIGIT On SDC

<table><thead><tr><th width="196">Tools/Skills</th><th width="491">Specification</th><th width="219">Weightage (1-5)</th><th>Yes/No</th></tr></thead><tbody><tr><td>System Administration</td><td>Linux Administration, troubleshooting, OS Installation, Package Management, Security Updates, Firewall configuration, Performance tuning, Recovery, Networking, Routing tables, etc</td><td>4</td><td><br></td></tr><tr><td>Containers/Dockers</td><td>Build/Push docker containers, tune and maintain containers, Startup scripts, Troubleshooting dockers containers.</td><td>2</td><td><br></td></tr><tr><td>Kubernetes</td><td><p>Setup kubernetes cluster on bare-metal and VMs using kubeadm/kubespary, terraform, etc. Strong understanding of various kubernetes components, configurations, kubectl commands, RBAC. Creating and attaching persistent volumes, log aggregation, deployments, networking, service discovery, Rolling updates. Scaling pods, deployments, worker nodes, node affinity, secrets, configMaps, etc..</p><p>Skills Needed: <a href="https://docs.google.com/document/d/1CM_w6Q82b70ir8m8O_0XAaJuf9fv11DRhjT0M85LaTA/edit">https://docs.google.com/document/d/1CM_w6Q82b70ir8m8O_0XAaJuf9fv11DRhjT0M85LaTA/edit</a></p></td><td>3</td><td><br></td></tr><tr><td>Database Administration</td><td>Setup PostGres DB, Set up read replicas, Backup, Log, DB RBAC setup, SQL Queries</td><td>3</td><td><br></td></tr><tr><td>Docker Registry</td><td>Setup docker registry and manage</td><td>2</td><td><br></td></tr><tr><td>SCM/Git</td><td>Source Code management, branches, forking, tagging, Pull Requests, etc.</td><td>4</td><td><br></td></tr><tr><td>CI Setup</td><td>Jenkins Setup, Master-slave configuration, plugins, jenkinsfile, groovy scripting, Jenkins CI Jobs for Maven, Node application, deployment jobs, etc.</td><td>4</td><td><br></td></tr><tr><td>Artifact management</td><td>Code artifact management, versioning</td><td>1</td><td><br></td></tr><tr><td>Apache Tomcat</td><td>Web server setup, configuration, load balancing, sticky sessions, etc</td><td>2</td><td><br></td></tr><tr><td>WildFly JBoss</td><td>Application server setup, configuration, etc.</td><td>3</td><td><br></td></tr><tr><td>Spring Boot</td><td>Build and deploy spring boot applications</td><td>2</td><td><br></td></tr><tr><td>NodeJS</td><td>NPM Setup and build node applications</td><td>2</td><td><br></td></tr><tr><td>Scripting</td><td>Shell scripting, python scripting.</td><td>4</td><td><br></td></tr><tr><td>Log Management</td><td>Aggregating system, container logs, troubleshooting. Monitoring Dashboard for logs using prometheus, fluentd, Kibana, Grafana, etc.</td><td>3</td><td><br></td></tr><tr><td>WordPress</td><td>Multi-tenant portal setup and maintain</td><td>2</td><td><br></td></tr></tbody></table>

## Resource Requirement

<table><thead><tr><th width="119.66666666666666">Team</th><th width="151">Roles</th><th>Responsibility</th></tr></thead><tbody><tr><td>Program Management</td><td><br></td><td>Responsible for driving the Transformation Vision for State Team Formation, reviewing them and resolving hurdles for the teams.</td></tr><tr><td><br></td><td>Program Leader</td><td><p>Overall responsibility to Drive Vision of the program.</p><p> Identify Success Metrics for the program and the budgets for it. Staff the teams with the right / capable people to drive the outcomes. </p><p>Define program Structure and ensure that the various teams work in tandem towards the Program Plan/ Schedule. </p><p>Review program Progress and remove bottlenecks for the Implementation Teams</p></td></tr><tr><td><br></td><td>Procurement</td><td>Help timely procurements of various items/ services needed for the Program</td></tr><tr><td><br></td><td>Program Manager</td><td><p>Plan, establish tracking mechanism, </p><p>Track and Manage Program activities,</p><p> Conduct reviews with various teams to drive the Program. Ensure that the efforts of various teams are aligned.</p><p> Escalate/ seek support as appropriate to the Program Leader.</p></td></tr><tr><td><br></td><td>Program Coordinator</td><td><p>Track progress of activities, </p><p>Help documentation of the Program team,</p><p>Coordinate meeting schedules and logistics.</p></td></tr><tr><td><br></td><td>Implementation Review</td><td><p>Reports to program leader</p><p>Ensures Processes and System adoption happens in the ULB </p><p>Ensures the Program metrics are headed in the right direction (Their responsibility will extend well beyond the technical rollout)</p></td></tr><tr><td>Domain Team</td><td><br></td><td><p>Finalize finance and other related processes for all ULBs, Provide Specific Inputs to Technical Implementation team, Capacity Building,</p><p> Data Preparation </p><p>Oversee UAT </p><p>Monitor data to identify process execution on ground, Identify improvement areas for the Finance function. </p></td></tr><tr><td><br></td><td>State Finance Accounting Leader</td><td><p>Should be a TRUSTED Line Function person, who can be the guide to all the Accounting Head at the ULBs. </p><p>Should be able to take decisions for the state on all ULB Finance processes and appropriate automation related to that.</p></td></tr><tr><td><br></td><td>Finance Advisors / Consultants/ Accounts officers</td><td>Finalise Standardised Finance processes that need to be there on the ground to realise the State's vision.</td></tr><tr><td>Technology Implementation Team</td><td><br></td><td><p>Technical Specialist team that has knowledge of the eGov Platform, technologies, the DIGIT modules. </p><p>Configure/ customise the product to the needs of the state. Integrate the product with other systems as needed and manage and support the State</p></td></tr><tr><td><br></td><td>Technical Program Manager</td><td><p>Has a good understanding of the eGov Platform/ Product.</p><p>Plans the Technical Track of the Product Manage Technical team Coordinates with various stakeholders during different phases of Implementation to get the Product ready for rollout in the ULBs. Plan and schedule activities as needed in the program. </p><p>He/She will be part of the Program Management team.</p></td></tr><tr><td><br></td><td>Business Analysts</td><td><p>Study and design State specific Accounting and other taxation Processes working with the Domain team. </p><p>Capture and document all Processes </p><p>Ensure that the Product will meet the needs of the State</p></td></tr><tr><td><br></td><td>Software Designers / Architects</td><td>Designing Software requirements based on the requirements finalised by the Business Analysts and leveraging platform as appropriate.</td></tr><tr><td><br></td><td>Business Analysts</td><td><p>Study and design State specific Processes working with the Domain team. </p><p>Capture and document all Processes and ensure that the Product will meet the needs of the State.</p></td></tr><tr><td><br></td><td>Software Designers / Architects</td><td>Designing Software requirements based on the requirements finalised by the Business Analysts and leveraging platform as appropriate.</td></tr><tr><td><br></td><td>Developers</td><td>Configurations, Customization and Data Loads.</td></tr><tr><td><br></td><td>Testers</td><td>Test configuration / customisation and regression testing for each release</td></tr><tr><td><br></td><td>Project Coordinator</td><td>Coordinate activities amongst the various stakeholder and logistics support</td></tr><tr><td><br></td><td>DevOps &#x26; Cloud Monitoring</td><td>Release Management, Managing Repository, Security and Build tools</td></tr><tr><td><br></td><td>DBA</td><td>Postgres DBA. Database Tuning, backup, Archiving</td></tr><tr><td>Field Team</td><td><br></td><td><p>Statewide capacity building (Including Change Management). Experience in Finance Area preferred. </p><p>Measure training effectiveness and fine-tune approach.</p><p> Plan refresher training as needed. </p></td></tr><tr><td><br></td><td>Content Developer</td><td>Prepare content for training different roles in DIGIT. </td></tr><tr><td><br></td><td>Trainers</td><td><p>Execute training as per content developed for the different roles in DIGIT. </p><p>Capture feedback and identify additional training needs if required</p></td></tr><tr><td>Help Desk and Support</td><td><br></td><td><p>Central help desk</p><p> Onground support in a planned manner to each ULB during the first 2 months after rolling out.</p></td></tr><tr><td><br></td><td>Help Desk leader</td><td><p>Organise and run the help desk operations.</p><p> Ensure that tickets are handled as per agreed SLAs, Coordinate with Technical team as needed.</p><p> Analyse Help desk calls and identify potential areas for the Domain / Business Analysts to work on.</p></td></tr><tr><td><br></td><td>Central Help Desk</td><td><p>To take care of L1 and L2 Support.</p><p>Ensure Tracking of issues on the help desk tool.</p></td></tr><tr><td><br></td><td>Provide On ground support (Face to face) during the first 2 months of rollout</td><td>At Least 1 person per 3-4 Ulbs who can travel during the first 2 months to provide support to end users. This is more for confidence building and ensuring adoption.</td></tr></tbody></table>

## DIGIT - Security Standards & Operational Recommendations

This section provides insights on security principles, security layers and the line of control that we focus on to prevent DIGIT security from the code, application, access, infra and operations. The target audience of this section are internal teams, partners, ecosystems and states to understand what security measures to be considered to secure DIGIT from an infrastructure and operations perspective .

### DIGIT - Key Security Principles

Subscribe to the DIGIT applicable [OWASP top 10](https://owasp.org/www-project-top-ten/) standard across various security layers.

1. **Minimize attack surface area**
2. Implement a strong identity foundation - Who accesses what and who does what.
3. Apply security at all possible layers&#x20;
4. Automate security best practices
5. **Separation of duties (SoD).**
6. **The principle of Least privilege (PoLP)**
7. Templatized design - (Code, Images, Infra-as-code, Deploy-as-code, Conf-as-code, etc)
8. Align with [MeiTY Standards](https://meity.gov.in/content/general-guidelines-secure-application-and-infrastructure) to meet SDC Infra policies.

### Security Layers & Line of Control

<table><thead><tr><th width="243">Security Layers</th><th>Line Of Controls</th></tr></thead><tbody><tr><td>Application Layer</td><td>WAF, IAM, VA/PT, XSS, CSRF,  SQLi, DDoS Defense. </td></tr><tr><td>Code</td><td>Defining security in the code, Static/Dynamic vulnerabilities scan</td></tr><tr><td>Libraries/Containers</td><td>Templatize Design, Vulnerabilities scanning at CI</td></tr><tr><td>Data</td><td>Encryption, Backups, DLP</td></tr><tr><td>Network</td><td>TLS, Firewalls, Ingress/Egress, Routing. </td></tr><tr><td>Infra/Cloud</td><td>Configurations/Infra Templates, ACL, user/privilege mgmt, Secrets mgmt</td></tr><tr><td>Operations</td><td>(PoLP) Least Privilege, Shared Responsibilities, CSA, etc</td></tr></tbody></table>

### Application Layer

The presentation layer is likely to be the #1 attack vector for malicious individuals seeking to breach security defences like DDoS attacks, Malicious bots, Cross-Site Scripting (XSS) and SQL injection. Need to invest in web security testing with the powerful combination of tools, automation, process and speed that seamlessly integrates testing into software development, helping to eliminate vulnerabilities more effectively, deploy a web application firewall (WAF) that monitors and filters traffic to and from the application, blocking bad actors while safe traffic proceeds normally.

### Key Security Measures&#x20;

1\. TLS-protocols/Encryption: Access control to secure authentication and authorization. All APIs that are exposed must have HTTPS certificates and encrypt all the communication between client and server with transport layer security (TLS).

2\. Auth Tokens: An authorization framework that allows users to obtain admittance to a resource from the server. This is done using tokens in microservices security patterns: resource server, resource owner, authorization server, and client. These tokens are responsible for access to the resource before its expiry time. Also, Refresh Tokens that are responsible for requesting new access after the original token has expired.

3\. Multi-factor Authentication: authorize users on the front end, which requires a username and password as well as another form of identity verification to offer users better protection by default as some aspects are harder to steal than others. For instance, using OTP for authentication takes microservice security to a whole new level.

4\. Rate Limit/DDoS: denial-of-service attacks are the attempts to send an overwhelming number of service messages to cause application failure by concentrating on volumetric flooding of the network pipe. Such attacks can target the entire platform and network stack.&#x20;

To prevent this:&#x20;

* We should set a limit on how many requests in a given period can be sent to each API.&#x20;
* If the number exceeds the limit, block access from a particular API, at least for some reasonable interval.&#x20;
* Also, make sure to analyze the payload for threats.&#x20;
* The incoming calls from a gateway API would also have to be rate-limited.&#x20;
* Add filters to the router to drop packets from suspicious sources.

5\. Cross-site scripting (XSS): scripts that are embedded in a webpage and executed on the client side, in a user’s browser, instead of on the server side. When applications take data from users and dynamically include it in webpages without validating the data properly, attackers can execute arbitrary commands and display arbitrary content in the user’s browser to gain access to account credentials.&#x20;

How to prevent:

* Applications must validate data input to the web application from user browsers.
* All output from the web application to user browsers must be encoded.
* Users must have the option to disable client-side scripts.

6\. Cross-Site Request Forgery (CSRF): is an attack whereby a malicious website will send a request to a web application that a user is already authenticated against from a different website. This way an attacker can access functionality in a target web application via the victim's already authenticated browser. Targets include web applications like social media, in-browser email clients, online banking and web interfaces for network devices. To prevent this CSRF tokens are appended to each request and associated to the user’s session. Such tokens should at a minimum be unique per user session, but can also be unique per request.&#x20;

How to prevent:

* By including a challenge token with each request, the developer can ensure that the request is valid and not coming from a source other than the user.&#x20;

8\. SQL Injection (SQLi): allows attackers to control an application’s database – letting them access or delete data, change an application’s data-driven behaviour, and do other undesirable things – by tricking the application into sending unexpected SQL commands. SQL injections are among the most frequent threats to data security.

How to prevent:

* Using parameterized queries which specify placeholders for parameters so that the database will always treat them as data rather than part of an SQL command. Prepared statements and object-relational mappers (ORMs) make this easy for developers.
* Remediate SQLi vulnerabilities in legacy systems by escaping inputs before adding them to the query. Use this technique only where prepared statements or similar facilities are unavailable.
* Mitigate the impact of SQLi vulnerabilities by enforcing the least privilege on the database. Ensure that each application has its database credentials and that these credentials have the minimum rights the application needs.

### Security In The Code

The primary causes of commonly exploited software vulnerabilities are consistent defects, bugs, and logic flaws in the code. Poor coding practices can create vulnerabilities in the system that can be exploited by cybercriminals.&#x20;

\
What defines a security in the code:

1\. White-box code analysis:  As developers write code, the IDE needs to provide focused, real-time security feedback with white-box code analysis. It also helps developers remediate faster and learn on the job through positive reinforcement, remediation guidance, code examples, etc.&#x20;

2\. Static Code Analysis (SAST):  A static analysis tool reviews program code, searching for application coding flaws, back doors or other malicious code that could give hackers access to critical data or customer information. However, most static analysis tools can only scan source code.

3: Vulnerability assessment: Vulnerability assessment for the third-party libraries/artefacts as part of CI and GitHub PR process. Test results are returned quickly and prioritized in a Fix-First Analysis that identifies both the most urgent flaws and the ones that can be fixed most quickly, allowing developers to optimize efforts and save additional resources.&#x20;

4\. Secure PII/Encrypt: Personally identifying information – to make sure that it is not being displayed as plain text. All the passwords and usernames must be masked during the storing in logs or records. However, adding extra encryption above TLS/HTTP won’t add protection for traffic travelling through the wire. It can only help a little bit at the point where TLS terminates, so it can protect sensitive data (such as passwords or credit card numbers) from accidental dumping into a request log. Extra encryption (RSA 2048+ or Blowfish) might help protect data against those attacks that aim at accessing the log data. But it will not help with those who try accessing the memory of the application servers or the main data storage.

5\. Manual Penetration Testing: Some categories of vulnerabilities, such as authorization issues and business logic flaws, cannot be found with automated assessments and will always require a skilled penetration tester to identify them. Need to employ Manual Penetration Testing that uses proven practices to provide extensive and comprehensive security testing results for web, mobile, desktop, and back-end with detailed results, including attack simulations.&#x20;

### Libraries/Containers

&#x20;Components, such as libraries, frameworks, container images, and other software modules, almost always run with full privileges. If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover. Applications using components with known vulnerabilities may undermine application defences and enable a range of possible attacks and impacts.&#x20;

Automating dependency checks for the libraries and container auditing, as well as using other container security processes as part of the CI periodically or as part of PRs can largely prevent these vulnerabilities.  Subscribing to tools that comply with vulnerable library databases such as OSVDB, Node Security Project, CIS,  [National Vulnerability Database](https://nvd.nist.gov/), and Docker Bench for Security can help identify and fix the vulnerabilities periodically. A private docker registry can help.

### Data Security

Data Security involves putting in place specific controls, standard policies, and procedures to protect data from a range of issues, including:

* Enforced encryption: Encrypt, manage and secure data by safeguarding it in transit. Password-based, easy to use and very efficient.&#x20;
* Unauthorized access: Blocking unauthorized access plays a central role in preventing data breaches. Implementing Strong Password Policy and MFA.
* Accidental loss: All data should be backed up. In the event of hardware or software failure, breach, or any other error to data; a backup allows it to continue with minimal interruption. Storing the files elsewhere can also quickly determine how much data was lost and/or corrupted.
* Destruction: Endpoint Detection and Response (EDR) – provides visibility and defensive measures on the endpoint itself, when attacks occur on endpoint devices this can eliminate gaining access systems and avoid destruction of the data.

### Infra/Cloud

&#x20;In microservices and the Cloud Native architectural approach, the explosion of ephemeral, containerized services that arise from scaling applications developed increases the complexity of delivery. Fortunately, Kubernetes was developed just for this purpose. It provides DevOps teams with an orchestration capability for managing the multitude of deployed services, with in-built automation, resilience, load balancing, and much more. It's perfect for the reliable delivery of Cloud Native applications. Below are some of the key areas to get more control to establish policies, procedures and safeguards through the implementation of a set of rules for compliance. These rules cover infra privacy, security, breach notification, enforcement, and an omnibus rule that deals with security compliance.

* Strong stance on authentication and authorization
* Role-Based Access Control (RBAC)&#x20;
* Kubernetes infrastructure vulnerability scanning
* Hunting misplaced secrets
* Workload hardening from Pod Security to network policies
* Ingress Controllers for security best practices
* Constantly watch your Kubernetes deployments
* Find deviations from desired baselines
* Should alert or deny on policy violation
* Block/Whitelist (IP or DNS) connections before entering the workloads.
* Templatize the deployment/secrets configs and serve as config-as-code.

### Network Security

&#x20;Kubernetes brings new requirements for network security, because applications, that are designed to run on Kubernetes, are usually architected as microservices that rely on the network. They make API calls to each other. Steps must be taken to ensure proper security protocols are in place. The following are the key areas for implementing network security for a Kubernetes platform:

* Container Groups: Coupled communication between grouped containers, is achieved inside the Pod that contains one or more containers.&#x20;
* Communication between Pods: Pods are the smallest unit of deployment in Kubernetes. A Pod can be scheduled on one of the many nodes in a cluster and has a unique IP address. Kubernetes places certain requirements on communication between Pods when the network has not been intentionally segmented. These requirements include:&#x20;
* Containers should be able to communicate with other Pods without using network address translation (NAT).&#x20;
* All the nodes in the cluster should be able to communicate with all the containers in the cluster.&#x20;
* The IP address assigned to a container should be the same that is visible to other entities communicating with the container.&#x20;
* Pods and Services: Since Pods are ephemeral in nature, an abstraction called a Service provides a long-lived virtual IP address that is tied to the service locator (e.g., a DNS name). Traffic destined for that service VIP is then redirected to one of the Pods and offers the service using that specific Pod’s IP address as the destination.&#x20;
* Traffic Direction: Traffic is directed to Pods and services in the cluster via multiple mechanisms. The most common is via an ingress controller, which exposes one or more service VIPs to the external network. Other mechanisms include node ports and even publicly-addressed Pods.

### Operational Security

It is a procedural security that manages risk and encourages to view of operations from the perspective of an adversary to protect sensitive information from falling into the wrong hands. Following are a few best practices to implement a robust, comprehensive operational security program:

* Implement precise change management processes: All changes should be logged and controlled so they can be monitored and audited.
* Restrict access to network devices using AAA authentication: a “need-to-know” is a rule of thumb regarding access and sharing of information.
* Least Privilege (PoLP): Give the minimum access necessary to perform their jobs.&#x20;
* Implement dual control: Those who work on the tasks are not the same people in charge of security.
* Automate tasks: reduce the need for human intervention. Humans are the weakest link in any organization’s operational security initiatives because they make mistakes, overlook details, forget things, and bypass processes.

Incident response and disaster recovery planning: are always crucial components of a sound security posture, we must have a plan to identify risks, respond to them, and mitigate potential damages.
