---
description: Application security checklist by various functions
---

# Security Checklist

Application security is a critical topic. Being a good engineer requires being aware of Application security best practices. We should practice defensive programming and ensure run security checks much earlier and more frequently during every phase of the software development. The earlier we catch vulnerabilities, the less dramatic and expensive those violations are to resolve. Waiting until release will just leave us nervous and unprepared. Delivering security alongside the continuous delivery of software, we'll identify security problems before they become hopelessly entangled in the application and therefore more difficult, and costly, to resolve.&#x20;

Teams should ensure the following checks to deliver security.

1. [Design considerations](./#id-1.-design-considerations)
2. [Development considerations](./#id-2.-development-considerations)
3. [CI/CD considerations](./#id-3.-ci-cd-considerations)
4. [Testing considerations](./#id-4.-testing-considerations)
5. [Infra-security considerations](./#id-5.-infra-security-considerations)
6. [Deployment considerations](./#id-6.-deployment-considerations)

## 1. Design Considerations

Injecting Security in the design phase means addressing design decisions that take into account the perspective of an attacker that is trying to breach weaknesses and compromise the confidentiality, integrity and other important security aspects of your software.&#x20;

* [x] Protect Personally Identifiable Information (PII Data)
  * Personally identifiable information (PII) is any data that can be used to identify a specific individual
  * Protect Personally Identifiable Information in the applications by encrypting them
  * Follow the data privacy laws of the land
* [x] Secure File uploads
  * Whitelist-allowed extensions. Only allow safe and critical extensions for business functionality
  * Ensure that input validation is applied before validating the extensions.
  * Set a filename length limit. Restrict the allowed characters if possible
  * Only allow authorised users to upload files
  * In the case of public access to the files, use a handler that gets mapped to filenames inside the application (someid -> file.ext)
  * Run the file through antivirus or a sandbox, if available, to validate that it does not contain malicious data
  * Ensure that any libraries used are securely configured and kept up to date
  * Protect the file upload from CSRF attacks
* [x] Where possible, always log in and handle the exception
  * Input validation failures e.g. protocol violations, unacceptable encodings, invalid parameter names and values
  * Output validation failures e.g. database recordset mismatch, invalid data encoding
  * Authentication successes and failures, authorization (access control) failures
  * Session management failures e.g. cookie session identification value modification
  * Application errors and system events e.g. syntax and runtime errors, connectivity problems, performance issues, third-party service error messages, file system errors, file upload virus detection, configuration changes
  * Application and related systems startups and shutdowns, and logging initialization (starting, stopping or pausing)
  * Use of higher-risk functionality e.g. network connections, addition or deletion of users, changes to privileges, assigning users to tokens, adding or deleting tokens, use of systems administrative privileges, access by application administrators, all actions by users with administrative privileges, access to payment cardholder data, use of data encrypting keys, key changes, creation and deletion of system-level objects, data import and export including screen-based reports, submission of user-generated content especially file uploads
  * Legal and other opt-ins e.g. permissions for mobile phone capabilities, terms of use, terms & conditions, personal data usage consent, permission to receive marketing communications
* [x] In the event of an authentication exception, using any of the authentication mechanisms (login, password reset or password recovery), an application must respond with a generic error message regardless of whether:
  * The user ID or password was incorrect.
  * The account does not exist.
  * The account is locked or disabled.
* [x] In order to secure authorization-based transactions in such a system:
  * Authorization should be performed and enforced server-side
  * Transaction verification data should be generated server-side
  * Applications should prevent authorization credentials from brute-forcing
  * Transaction data should be protected against modification
  * Confidentiality of the transaction data should be protected during any client/server communications
  * When a transaction is executed, the system should check whether it was authorized
  * Authorization credentials should be valid only for a limited period of time
  * Authorization credentials should be unique for every operation
* [x] Enable logging and monitoring of authentication functions to detect attacks/failures on a real-time basis
  * Ensure that all failures are logged and reviewed
  * Ensure that all password failures are logged and reviewed
  * Ensure that all account lockouts are logged and reviewed
* [x] **Cross-Site-Scripting (XSS)**
  * Use templating engines or frameworks that automatically escape XSS by design, such as EJS, Pug, React, or Angular. - - Learn the limitations of each mechanism XSS protection and appropriately handle the use cases which are not covered
  * Escaping untrusted HTTP request data based on the context in the HTML output (body, attribute, JavaScript, CSS, or URL) will resolve Reflected and Stored XSS vulnerabilities
  * Applying context-sensitive encoding when modifying the browser document on the client-side acts against DOM XSS
  * Enabling a Content-Security Policy (CSP) as a defence-in-depth mitigating control against XSS
* [x] DB Security
  1. Data Encryption  - Encrypt database storage files and on-site/offsite backups.&#x20;
     * Identify the specific data sets on which encryption should be enabled. Which databases? Which Rows? Which Columns?&#x20;
     * Use different encryption keys to encrypt different datasets, Perhaps data that belongs to different clients sharing a single database?
  2. AUDITING -  Monitor internal and external access to data that is considered sensitive.
     * Identify the specific data assets that require auditing: databases, tables, columns.&#x20;
     * Track the username, originating from which server, accessing which specific dataset and when.&#x20;
     * Special auditing is needed if applications users are separate from database users.
  3. DATA GOVERNANCE - Track and monitor data including as it moves across different data silos.
     * Make sure to tag, track and catalog datasets as they travel from one database to another. Establish policies and workflows with checks along the way.&#x20;
     * Implement complete data lifecycle management policies across all databases including data provisioning, data cleansing and periodic dataset compliance checks.
  4. CLIENT SEGREGATION - In Multi-Tenant environments, multiple “clients” can share the same database server. These types of databases require special treatment across all security domains: encryption, auditing, authorization, etc…&#x20;
     * Encrypt individual client data using different keys. implement strong authorization and authentication, using different users for each client and restricting access to subsets of the entire database.&#x20;
     * Identify specific customers that cannot co-exist on the same database server.
  5. AUTHORIZATION - Enable polices on who can access which datasets, enable strict permissions.&#x20;
     * Different users should only be allowed access to specific datasets within a database: down to the specific row and column levels. Never grant excessive permissions.&#x20;
     * If application users and database users do not correlate, more sophisticated authorization needs to be configured to create a strong chain of identity.&#x20;
     * Set requirements for sophisticated authorization that goes beyond simple users: filter origin of access to data – server IP, time/date, application, etc…
     * Do you have “super” / system” users that can access all data? Are they required? These types of users require special attention.&#x20;
  6. AUTHENTICATION - Setup secure means by which users authenticate with the database.
     * Ensure strong authentication mechanisms such as single-sign on and restricting databases to only authenticate users from Directory Services and not using username/password combinations.&#x20;
     * If “web users” authenticate with your application and the application authenticates with the database using different users or using username/password combinations, special attention must be placed on creating strong authentication chains

## 2. Development Considerations

* [x] Lightweight, Static analysis (SAST) checking in the engineer’s IDE like VSCode, Eclipse, Intelli..
* [x] Peer code reviews (for defensive coding and security vulnerabilities), Code reviewers should always consider security guidelines during code reviews.
* [x] Audit your application's design, implementation and security with unit/integration tests coverage frequently

#### Authentication

* [x] &#x20;Don't use `Basic Auth`. Use standard authentication instead (e.g. [JWT](https://jwt.io/), [OAuth](https://oauth.net/)).
* [x] &#x20;Don't reinvent the wheel in `Authentication`, `token generation`, `password storage`. Use the standards.
* [x] &#x20;Use `Max Retry` and jail features in Login.
* [x] &#x20;Use encryption on all sensitive data.

#### JWT (JSON Web Token)

* [x] &#x20;Use a random complicated key (`JWT Secret`) to make brute-forcing the token very hard.
* [x] &#x20;Don't extract the algorithm from the header. Force the algorithm in the backend (`HS256` or `RS256`).
* [x] &#x20;Make token expiration (`TTL`, `RTTL`) as short as possible.
* [x] &#x20;Don't store sensitive data in the JWT payload, it can be decoded [easily](https://jwt.io/#debugger-io).

#### OAuth

* [x] &#x20;Always validate `redirect_uri` server-side to allow only whitelisted URLs.
* [x] &#x20;Always try to exchange for code and not tokens (don't allow `response_type=token`).
* [x] &#x20;Use `state` parameter with a random hash to prevent CSRF on the OAuth authentication process.
* [x] &#x20;Define the default scope, and validate scope parameters for each application.

#### Access

* [x] &#x20;Limit requests (Throttling) to avoid DDoS / brute-force attacks.
* [x] &#x20;Use HTTPS on the server side to avoid MITM (Man in the Middle Attack).
* [x] &#x20;Use `HSTS` header with SSL to avoid SSL Strip attacks.
* [x] &#x20;For private APIs, only allow access from whitelisted IPs/hosts.
* [x] Use an API Gateway service to enable caching, Rate Limit policies (e.g. Quota, Spike Arrest, or Concurrent Rate Limit) and deploy APIs resources dynamically

#### Input

* [x] Text areas and input fields for PII (name, email, address, phone number) and login credentials (username, password) should be prevented from being stored in the browser.&#x20;
* [x] Use the proper HTTP method according to the operation: `GET (read)`, `POST (create)`, `PUT/PATCH (replace/update)`, and `DELETE (to delete a record)`, and respond with `405 Method Not Allowed` if the requested method isn't appropriate for the requested resource.
* [x] &#x20;Validate `content-type` on request Accept header (Content Negotiation) to allow only your supported format (e.g. `application/xml`, `application/json`, etc.) and respond with `406 Not Acceptable` response if not matched.
* [x] &#x20;Validate user input to avoid common vulnerabilities (e.g. `XSS`, `SQL-Injection`, `Remote Code Execution`, etc.).
* [x] &#x20;Don't use any sensitive data (`credentials`, `Passwords`, `security tokens`, or `API keys`) in the URL, but use the standard Authorization header.
* [x] &#x20;Use an API Gateway service to enable caching, Rate Limit policies (e.g. `Quota`, `Spike Arrest`, or `Concurrent Rate Limit`) and deploy APIs resources dynamically.
* [x] All the data exchanged with the REST API must be validated by the API.

#### Processing

* [x] &#x20;Check if all the endpoints are protected behind authentication to avoid a broken authentication process.
* [x] Serialize your JSON (to avoid arbitrary JavaScript remote code execution)
* [x] &#x20;User own resource ID should be avoided. Use `/me/orders` instead of `/user/654321/orders`.
* [x] &#x20;Don't auto-increment IDs. Use `UUID` instead.
* [x] &#x20;If you are parsing XML files, make sure entity parsing is not enabled to avoid `XXE` (XML external entity attack).
* [x] &#x20;If you are parsing XML files, make sure entity expansion is not enabled to avoid `Billion Laughs/XML bomb` via exponential entity expansion attack.
* [x] &#x20;Use a CDN for file uploads.
* [x] &#x20;If you are dealing with a huge amount of data, use Workers and Queues to process as much as possible in the background and return a response fast to avoid HTTP Blocking.
* [x] &#x20;Do not forget to turn the DEBUG mode OFF.

#### Output

* [x] &#x20;Send `X-Content-Type-Options: nosniff` header.
* [x] &#x20;Send `X-Frame-Options: deny` header.
* [x] &#x20;Send `Content-Security-Policy: default-src 'none'` header.
* [x] &#x20;Remove fingerprinting headers - `X-Powered-By`, `Server`, `X-AspNet-Version`, etc.
* [x] &#x20;Force `content-type` for your response. If you return `application/json`, then your `content-type` response is `application/json`.
* [x] &#x20;Don't return sensitive data like `credentials`, `Passwords`, or `security tokens`.
* [x] &#x20;Return the proper status code according to the operation completed. (e.g. `200 OK`, `400 Bad Request`, `401 Unauthorized`, `405 Method Not Allowed`, etc.).

Logging

* [x] Do not forget to turn the DEBUG mode OFF in production builds.

## 3. CI/CD Considerations

* [x] Compile and build checks, ensuring the vulnerabilities are identified in third-party components, Libraries.
* [x] Dashboard the findings and Generating Alerts on high-risk code.
* [x] Automate the fixes by integrating the efficient tools that gates the security thresholds and raises possible fixes/suggestions.
* [x] Automation of unit testing of security functions, with full coverage of code analysis.
* [x] Audit your design and implementation with unit/integration tests coverage.
* [x] &#x20;Use a code review process and disregard self-approval.
* [x] &#x20;Ensure that all components of your services are statically scanned by AV software before pushing to production, including vendor libraries and other dependencies.
* [x] &#x20;Design a rollback solution for deployments.

## 4. Testing Considerations

#### Information Gathering

A successful web application security strategy fundamentally begins with an understanding of the interactions between the **web server**, **users**, and **applications**. While application deployment platforms vary, key vulnerabilities in infrastructure configuration act as a common weak link for threat actors to initiate an attack.

Some key application security information-gathering activities include:

* Identify technologies used
* Identify user roles
* Identify application entry points
* Identify client-side code
* Identify multiple versions/channels (e.g. web, mobile web, mobile app, web services)
* Identify co-hosted and related applications
* Identify all hostnames and ports
* Identify third-party hosted content

#### Configuration Management

A web server ecosystem is intrinsically complex with highly connected, heterogeneous services and components working together. Reviewing and managing the configuration of the server is, as a result, a very crucial aspect for maintaining robust security across multiple layers of an application.

Securing various configuration items of an application involves:

* Check for commonly used application and administrative URLs
* Check for old, backup and unreferenced files
* Check HTTP methods supported and Cross Site Tracing (XST)
* Test file extensions handling
* Test for security HTTP headers (e.g. CSP, X-Frame-Options, HSTS)
* Test for policies (e.g. Flash, Silverlight, robots)
* Test for non-production data in live environment, and vice-versa
* Check for sensitive data in client-side code (e.g. API keys, credentials)

#### Secure Transmission

* Check SSL Version, Algorithms, Key length
* Check for Digital Certificate Validity (Duration, Signature and CN)
* Check credentials only delivered over HTTPS
* Check that the login form is delivered over HTTPS
* Check session tokens only delivered over HTTPS
* Check if HTTP Strict Transport Security (HSTS) in use

#### Authentication

* Test for user enumeration
* Test for authentication bypass
* Test for bruteforce protection
* Test password quality rules
* Test remember me functionality
* Test for autocomplete on password forms/input
* Test password reset and/or recovery
* Test password change process
* Test CAPTCHA
* Test multi-factor authentication
* Test for logout functionality presence
* Test for cache management on HTTP (eg Pragma, Expires, Max-age)
* Test for default logins
* Test for user-accessible authentication history
* Test for out-of-channel notification of account lockouts and successful password changes
* Test for consistent authentication across applications with shared authentication schema / SSO

#### Session Management

Once a user is authenticated, their interaction with the server is managed within a **session**. Improperly managed sessions open doors for attackers to compromise access mechanisms by assuming those to be identities of legitimate users. More so, such compromised accesses are often taken advantage of by attack vectors that escalate privileges and penetrate deeper into the system. To avoid vulnerabilities within a session, the following processes are recommended to be tested as a best practice:

* Establish how session management is handled in the application (eg, tokens in cookies, token in URL)
* Check session tokens for cookie flags (httpOnly and secure)
* Check session cookie scope (path and domain)
* Check session cookie duration (expires and max-age)
* Check session termination after a maximum lifetime
* Check session termination after a relative timeout
* Check session termination after logout
* Test to see if users can have multiple simultaneous sessions
* Test session cookies for randomness
* Confirm that new session tokens are issued on login, role change and logout
* Test for consistent session management across applications with shared session management
* Test for session puzzling
* Test for CSRF and clickjacking

#### Authorization

* Test for path traversal
* Test for bypassing authorization schema
* Test for vertical Access control problems (a.k.a. Privilege Escalation)
* Test for horizontal Access control problems (between two users at the same privilege level)
* Test for missing authorization

#### Data Validation

* Test for Reflected Cross Site Scripting
* Test for Stored Cross Site Scripting
* Test for DOM based Cross Site Scripting
* Test for Cross Site Flashing
* Test for HTML Injection
* Test for SQL Injection
* Test for LDAP Injection
* Test for ORM Injection
* Test for XML Injection
* Test for XXE Injection
* Test for SSI Injection
* Test for XPath Injection
* Test for XQuery Injection
* Test for IMAP/SMTP Injection
* Test for Code Injection
* Test for Expression Language Injection
* Test for Command Injection
* Test for Overflow (Stack, Heap and Integer)
* Test for Format String
* Test for incubated vulnerabilities
* Test for HTTP Splitting/Smuggling
* Test for HTTP Verb Tampering
* Test for Open Redirection
* Test for Local File Inclusion
* Test for Remote File Inclusion
* Compare client-side and server-side validation rules
* Test for NoSQL injection
* Test for HTTP parameter pollution
* Test for auto-binding
* Test for Mass Assignment
* Test for NULL/Invalid Session Cookie

#### Denial of Service

* Test for anti-automation
* Test for account lockout
* Test for HTTP protocol DoS
* Test for SQL wildcard DoS

#### Business Logic

Hackers mostly leverage an application’s original programmed flow to orchestrate breaches and penetration attacks. As a result, it is recommended to assess the business and application’s configuration to identify vulnerabilities in code or business logic that could be used for potential exploits.

* Test for feature misuse
* Test for lack of non-repudiation
* Test for trust relationships
* Test for integrity of data
* Test segregation of duties

#### Cryptography

Cryptography ensures the secure exchange of information by using algorithms that transform human-readable data into a **ciphertext-encrypted** output. While doing so, the process establishes trust between the web server and network entities using security keys, making it an important mechanism for maintaining application security. Testing cryptography for maintaining application security involves:

* Check if the data which should be encrypted is not
* Check for wrong algorithms usage depending on the context
* Check for weak algorithms usage
* Check for proper use of salting
* Check for randomness functions

#### Risky Functionality - File Uploads

* Test that acceptable file types are whitelisted
* Test that file size limits, upload frequency and total file counts are defined and are enforced
* Test that file contents match the defined file type
* Test that all file uploads have Anti-Virus scanning in-place.
* Test that unsafe filenames are sanitised
* Test that uploaded files are not directly accessible within the web root
* Test that uploaded files are not served on the same hostname/port
* Test that files and other media are integrated with the authentication and authorisation schemas

#### Risky Functionality - Card Payment

* Test for known vulnerabilities and configuration issues on the Web Server and Web Application
* Test for default or guessable password
* Test for non-production data in a live environment, and vice-versa
* Test for Injection vulnerabilities
* Test for Buffer Overflows
* Test for Insecure Cryptographic Storage
* Test for Insufficient Transport Layer Protection
* Test for Improper Error Handling
* Test for all vulnerabilities with a CVSS v2 score > 4.0
* Test for Authentication and Authorization issues
* Test for CSRF

#### HTML 5

* Test Web Messaging
* Test for Web Storage SQL injection
* Check CORS implementation
* Check Offline Web Application

## 5. Infra-Security Considerations

#### Kubernetes Cluster/Infra Security

* [x] Practice the principle of least privilege. (PoLP)
  * SSO and Identity Access Management to the Cloud Infrastructure
  * Role-Based Access Control (RBAC) through ‘Role Binding’
  * Grant only the necessary privileges.
  * Revoke unnecessary privileges from the PUBLIC user group.
  * Restrict permissions on run-time facilities.
* [x] Pod Security – an admission control plugin to ensure that pods are admitted only when certain security guidelines are met.
* [x] Network Security
  * Use a firewall.
  * Never poke a hole through a firewall.
  * Monitor who accesses your systems.
  * Check network IP addresses.
* [x] Multi-tenancy
* [x] Data Encryption and Secrets Management
* [x] Regulatory Compliance
* [x] Incident Response and Forensics
* [x] Image Security and Vulnerability Scanning Enabled
* [x] Security Groups - allow inbound traffic only on TCP port 443 (HTTPS).
* [x] Logging Enabled
* [x] Running Recent Version - Ensure that the clusters are using the latest stable version with the latest features, design updates and bug fixes, and benefit from better security and performance.
* [x] Non-public Endpoints - ensure the server endpoints are accessible within VPCs

**Application Access**

* [x] **TLS for Kubernetes Ingress** – external access to the ingress controller should be over TLS, and interaction between the ingress controller and application containers must utilize TLS too, despite the fact that there are situations where that isn’t required.
* [x] **Encrypt everything in Transit** – the default behaviour ought to encrypt everything in transit. It is prudent to encrypt network traffic between containers.

## 6. Deployment Considerations

* [x] **OWASP A2: Broken Authentication**
  * Require MFA/2FA for important services and accounts
  * Rotate passwords and access keys frequently, including SSH keys
  * Apply strong password policies, both for ops and in-application user management.
  * Do not ship or deploy the application with any default credentials, particularly for admin users or external services you depend on
  * Use only standard authentication methods like OAuth, OpenID, etc.  avoid basic authentication
  * Auth rate-limiting: Disallow more than X login attempts (including password recovery, etc.) in a period of Y
  * On login failure, don't let the user know whether the username or password verification failed, just return a common-auth error
  * Consider using a centralized user management system to avoid managing multiple accounts per employee (e.g. GitHub, AWS, Jenkins, etc) and to benefit from a battle-tested user management system
* [x] **OWASP A3: Sensitive Data Exposure**
  * Only accept SSL/TLS connections, enforce Strict-Transport-Security using headers
  * Separate the network into segments (i.e. subnets) and ensure each node has the least necessary networking access permissions
  * Group all services/instances that need no internet access and explicitly disallow any outgoing connection (a.k.a private subnet)
  * Store all secrets in vault products like AWS KMS, HashiCorp Vault or Google Cloud KMS
  * Lockdown sensitive instance metadata using metadata
  * Encrypt data in transit when it leaves a physical boundary
  * Don't include secrets in log statements
  * Avoid showing plain passwords in the frontend, take necessary measures in the backend and never store sensitive information in plaintext
* [x] **OWASP A5:  Broken access control**
  * Respect the principle of least privilege  -  every component and DevOps person should only have access to the necessary information and resources
  * Never work with the console/root (full-privilege) account except for account management
  * Run all instances/containers on behalf of a role/service account
  * Assign permissions to groups and not to users. This should make permission management easier and more transparent for most cases
* [x] **OWASP A6: Security Misconfiguration**
  * Access to production environment internals is done through the internal network only, use SSH or other ways, but never expose internal services
  * Restrict internal network access  - explicitly set which resource can access other resources (e.g. network policy or subnets)
  * If using cookies, configure it to "secured" mode where it's being sent over SSL only
  * If using cookies, configure it for "same-site" only so only requests from same domain will get back the designated cookies
  * If using cookies, prefer "HttpOnly" configuration that prevents client-side JavaScript code from accessing the cookies
  * Protect each VPC with strict and restrictive access rules
  * Prioritize threats using any standard security threat modelling like STRIDE or DREAD
  * Protect against DDoS attacks using HTTP(S) and TCP load balancers
  * Perform periodic penetration tests by specialized agencies
* [x] **OWASP A7: Cross-Site-Scripting (XSS)**
  * Use templating engines or frameworks that automatically escape XSS by design, such as EJS, Pug, React, or Angular. - - Learn the limitations of each mechanism XSS protection and appropriately handle the use cases which are not covered
  * Escaping untrusted HTTP request data based on the context in the HTML output (body, attribute, JavaScript, CSS, or URL) will resolve Reflected and Stored XSS vulnerabilities
  * Applying context-sensitive encoding when modifying the browser document on the client-side acts against DOM XSS
  * Enabling a Content-Security Policy (CSP) as a defence-in-depth mitigating control against XSS
* [x] **OWASP A9: Using Components With Known Security Vulnerabilities**
  * Scan docker images for known vulnerabilities (using Docker's and other vendors' scanning services)
  * Enable automatic instance (machine) patching and upgrades to avoid running old OS versions that lack security patches
  * Provide the user with both 'id', 'access' and 'refresh' token so the access token is short-lived and renewed with the refresh token
  * Log and audit each API call to cloud and management services (e.g who deleted the S3 bucket?) using services like AWS CloudTrail
  * Run the security checker of your cloud provider (e.g. AWS security trust advisor)
* [x] **OWASP A10: Insufficient Logging & Monitoring**
  * Alert on remarkable or suspicious auditing events like user login, new user creation, permission change, etc
  * Alert on irregular amount of login failures (or equivalent actions like forgot password)
  * Include the time and username that initiated the update in each DB record
