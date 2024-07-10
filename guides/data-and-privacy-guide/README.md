---
description: Security & Privacy In DIGIT
---

# Data & Privacy Guide

## Introduction

DIGIT (**D**igital **I**nfrastructure for **G**overnance and **I**nclusive **T**ransformation) is an open-source platform designed to enable the delivery of public services efficiently and effectively. It consists of common services and shared data registries that various government agencies can leverage to build sector-specific solutions.&#x20;

Ensuring security and privacy within DIGIT is paramount to protecting sensitive information and maintaining public trust. As an open-source platform, DIGIT can enable certain aspects of security and privacy, and provide guidelines to product and solution developers, those who install and implement the platform in production, and those who use it to deliver public services.

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXc5ih8E9nxqXO3SxyvgLl9yP30DVXTbPh5VEFRbNDb8dpG9VoXeEK8__qtWq-cntnZuw9jVK_x22EXAt04ur_bOEuNc-cH83Ofge2TNBCrmlyAxhs-R29moR4mo_s41icFtwUBRyv59vnubtjVQJA9lfFvi?key=bclaamtiUjLQJjHpWEekfA" alt=""><figcaption><p>High-Level View of DIGIT</p></figcaption></figure>

</div>

## What is a DIGIT Implementation?

The DIGIT platform, with its suite of products and building blocks, is a [DPG](https://digitalpublicgoods.net/blog/unpacking-concepts-definitions-digital-public-infrastructure-building-blocks-and-their-relation-to-digital-public-goods/). Several steps and actors (listed below) are involved in converting the DIGIT platform into a DPI – a live instance used to deliver services to citizens.

* A Program Owner (typically a government agency) decides to implement the DIGIT platform or specific DIGIT products as its software platform for service delivery.
* The Program Owner procures the services of a Solution Implementing Agency (also known as a System Integrator) to implement the DIGIT platform/products in that specific context.
* The Solution Implementing Agency implements the DIGIT platform/products for the Program Owner. This includes:
  * Customising or extending DIGIT products as needed for that specific context.
  * Creating an instance of the DIGIT platform/products, on a server (cloud-based or physical) designated by the Program Owner
  * Configuring the products implemented in that instance to create a solution.
  * Conducting user acceptance testing, training, etc. with the persons (typically employees of the Program Owner) who will use those solutions.
* The Program Owner directs its employees to use these solutions to perform their work/deliver services to citizens.
* The Solution Implementing Agency or a Support Agency may continue to provide technical support, helpdesk services, etc. to the Program Owner, to resolve any difficulties or errors that arise when the Program Owner’s employees use these solutions.
* The DIGIT platform team at eGov supports this process in multiple ways:
  * Periodically releasing major and minor versions, updates, and patches to the DIGIT platform. (Implementing these into the specific solution is the responsibility of the Solution Implementing Agency and/or Support Agency.)
  * Resolving technical issues that pertain to the platform itself. (Issues that pertain to changes made by the Solution Implementing Agency are the responsibility of the Solution Implementing Agency.)
  * Training and enabling employees of Solution Implementing Agencies, to enhance their capacity to develop and implement solutions using the DIGIT platform.
  * Advising the Program Owner on program design and governance, including the technical requirements in its procurement process, and improving the adoption of the solutions implemented.

## Security and Privacy are Shared Responsibilities

When building, deploying, and using solutions built on the DIGIT platform, security and privacy are shared responsibilities between the DIGIT Platform, Product Developers, Solution Implementing Agencies (Systems Integrators), and Program Owners. The DIGIT Platform team incorporates key security and privacy features into the DIGIT code and installation scripts. It provides guidelines to Product Developers, Solution Implementing Agencies, and Program Owners to ensure comprehensive protection.

The responsibilities of key actors are as follows:

* **DIGIT Platform Team:** Custodian of the DIGIT platform roadmap and building blocks. Ensures key security and privacy features are incorporated in DIGIT, and provides guidelines for other actors.
* **Software Product Developers:** Use and extend DIGIT building blocks, possibly in combination with other DPGs or proprietary code, to create software products. Should follow guidelines for secure and privacy-protecting product development.
* **Solution Implementing Agencies (System Integrators):** Implement (customize, configure, install, deploy, support) solutions built on DIGIT for a specific client (presumably a government agency). Should follow guidelines for secure and privacy-protecting implementation, and ensure compliance with specific local laws/regulations.
* **Support Providers:** May be contracted to provide technical support and helpdesk services to an implementation of DIGIT for a specific client (presumably a government agency). Should follow guidelines for secure implementation, to the extent relevant to their work, and support users to follow secure operating procedures.
* **Program Owners:** Typically a government agency. Procures the services of solution implementers to implement solutions built on DIGIT based on their needs/mandate.&#x20;
  * The understanding of roles, levels of access, and the minimal data needed to perform a given task comes from the program owner’s administrative structures and operating procedures.&#x20;
  * Ensure that solution implementers, support providers, and government employees using those solutions follow secure implementation guidelines and operating procedures, as well as all relevant local laws/regulations.

## DIGIT Platform Practices

1. **Secure By Default -**
   * Default Security Settings: DIGIT is designed with default security settings that provide robust protection. While administrators can adjust these settings to fit specific needs, the out-of-the-box configuration is secure.
   * Minimal Privilege Principle: Users and services are granted the minimum levels of access necessary to perform their functions, reducing the risk of unauthorized access.
2. **Authentication and Authorization -**
   * One Time Password using SMS and Email is recommended wherever possible.
   * Passwords are hashed and stored in a secure database.
   * Password length, max invalid can be configured values for min and max password length and regex. (Default min=8, max=15 and invalidAttempts =5). Using this, we can configure the password strength.&#x20;
     * We can also configure the maximum number of invalid attempts allowed, and the account lock duration.&#x20;
     * Password can be changed using existing password.
     * Role-Based Access Control (RBAC): Implemented to ensure users have access only to necessary data and functionalities, as determined by their role.
3. **Data Encryption -**
   * In-Transit Encryption: All data is transmitted using HTTPS (TLS Encryption).
   * At-Rest Encryption: Encryption Service enables encryption of all sensitive data stored within the platform.
4. **Secure Development Practices -**
   * [DIGIT Security Handbook](https://core.digit.org/accelerators/checklists/security-checklist/security-guidelines-handbook) and [DIGIT Security Checklist](https://core.digit.org/accelerators/checklists/security-checklist) lists down all the secure development practices.
   * Code Reviews and Audits: Regular reviews and audits are conducted to identify and rectify vulnerabilities for all platform building blocks.
   * OWASP Security Guidelines: The platform development team adheres to OWASP security guidelines to prevent common vulnerabilities. These are verified during manual and automated code reviews (using AI code reviewers).&#x20;
   * Tracking Security Updates: The platform team monitors security updates in dependent open-source libraries and software and provides upgrade releases to address any critical vulnerabilities.&#x20;
5. **Infrastructure Security -**
   * Installation scripts implement, by default, several security best practices through automation e.g. on AWS
     * S3 Backend Encryption: The Terraform state is stored in an S3 bucket with encryption enabled.
     * VPC Configuration: The network module sets up a Virtual Private Cloud (VPC) to isolate resources and provide a secure network boundary.
     * Database Security: The PostgreSQL database is deployed within private subnets and security group rules are applied to control access.
     * IAM Role and Policy Management: IAM roles and policies are defined to grant necessary permissions while following the principle of least privilege.
     * OIDC Authentication: The EKS cluster is configured to use OpenID Connect (OIDC) for authentication, enhancing security through federated identity.
     * TLS Certificate Management: The TLS certificate resource ensures secure communication with the EKS cluster.
     * Kubernetes Service Accounts with IAM Roles: Service accounts in Kubernetes have specific IAM roles attached to ensure necessary AWS permissions without using static credentials.
     * Security Group Rules: Specific security group rules control ingress traffic to the RDS database from worker nodes only.
     * EKS Add-ons Management: Managed add-ons like kube-proxy, coredns, and aws-ebs-csi-driver are deployed using aws\_eks\_addon to keep these critical components up-to-date with security patches.
     * IAM Role Assumption Policy: The aws\_iam\_role resource includes a policy for secure and temporary access tokens using the OIDC provider.
     * Environment Variables and Secrets Management: Sensitive data such as database credentials and cluster names are managed as variables to avoid hard coding in configuration files.
     * AWS Security Group for Worker Nodes: The security group for worker nodes ensures only necessary traffic is allowed, improving the cluster’s security posture.
     * Backup Retention for Database: Backup retention is configured for the PostgreSQL database to ensure regular backups.
6.  **Signed Audit Logs -**

    * Non-Repudiation: Implementation of signed audit logs to ensure actions cannot be denied after they have been performed, enhancing accountability and traceability.



    <div align="left">

    <figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXcQhdl7MTNWtCIoUQFLYLuGIp291sQD1zHS9nKPr6qpJKvMidYYYidKXYXtgng9XCixpEQMkx8RYlt7Wr4d7_bgDB7nf2CNMrKozXzgRgVFSYg_hRspViSTa2VQnZBWcsPnjqAqRQJnYcLfz77v0hA-aT3C?key=bclaamtiUjLQJjHpWEekfA" alt=""><figcaption><p>DIGIT Platform - Default Configuration and Security Settings</p></figcaption></figure>

    </div>

## DIGIT Platform Building Blocks

The key building blocks that play a crucial role in ensuring security and privacy are as follows.

1. [API Gateway](../../platform/core-services/api-gateway/): Ensures that no data is accessible without authentication and authorization.
2. [User Services](../../platform/core-services/user/): Manages users and passwords. Provides authentication services.
3. [Role Services](../../platform/core-services/access-control-services.md): Allows configuration of roles and limits access each role has to specified data and services.
4. [Encryption Services](../../platform/core-services/encryption-service/): Provides the ability to encrypt and decrypt data.
5. [Signed Audit Services](../../platform/core-services/audit-service/signed-audit-performance-testing-results.md): Logs all changes made to all data in a signed audit log.

The diagram below illustrates how information flows in DIGIT, and how these services enable security and privacy during such information flow.

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXfnNZu8B2f4-uN7CldVv7RfgCVCO2CiatRC-hGnFPxngfC5brNl9-OlHB80ub8TOsRvyZ3qmbak9h_IwGdKvIZFMmGpzIqLuspDZqDEsHF-M38q5TmqBUnIDGXPOAXWtzxWJSuQimsOokrX5X0RJTAXFYh1?key=bclaamtiUjLQJjHpWEekfA" alt=""><figcaption><p>Information flow with security measures in DIGIT</p></figcaption></figure>

Click on the links below to browse through the role-specific data and privacy guidelines:

* [Security & Privacy Guidelines For Product Developers](security-and-privacy-guidelines-for-product-developers.md)
* [Security & Privacy Guidelines For Solution Implementing Agencies](security-and-privacy-guidelines-for-solution-implementing-agencies.md)
* [Security & Privacy Guidelines For Program Owners](security-and-privacy-guidelines-for-program-owners.md)
