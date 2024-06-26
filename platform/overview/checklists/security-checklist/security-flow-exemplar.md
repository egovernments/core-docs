# Security Flow - exemplar

## **PHASE 1: REQUIREMENTS**

* **Call out the security requirements in PRD like a Sample functional requirement:** user needs the ability to verify their contact information before they are able to renew their membership.&#x20;
* **Sample security consideration**: users should be able to see only their own contact information and no one else’s.

## **PHASE 2: DESIGN**

This phase translates in-scope requirements into a plan of what this should look like in the actual application. Here, functional requirements typically describe what should happen, while security requirements usually focus on what shouldn’t.

* **Sample functional design:** page should retrieve the user’s name, email, phone, and address from CUSTOMER\_INFO table in the database and display it on the screen.
* **Sample security concern:** we must verify that the user has a valid session token before retrieving information from the database. If absent, the user should be redirected to the login page.

## **PHASE 3: DEVELOPMENT**

When it’s time to actually implement the design and make it a reality, concerns usually shift to making sure the code is well-written from the security perspective. There are usually established secure coding guidelines as well as code reviews that double-check that these guidelines have been followed correctly. These code reviews can be either manual or automated using technologies such as [static application security testing (SAST)](https://snyk.io/learn/application-security/sast-vs-dast/).

That said, modern application developers can’t be concerned only with the code they write, because the vast majority of modern applications aren’t written from scratch. Instead, developers rely on existing functionality, usually provided by free open-source components to deliver new features and therefore value to the organization as quickly as possible. In fact, 90%+ of modern deployed applications are made of these open-source components. These open-source components are usually checked using [Software Composition Analysis (SCA)](https://snyk.io/blog/what-is-software-composition-analysis-sca-and-does-my-company-need-it/) tools.

**Secure coding guidelines, in this case, may include:**

* Using parameterized, read-only SQL queries to read data from the database and minimize chances that anyone can ever commandeer these queries for nefarious purposes
* Validating user inputs before processing data contained in them
* Sanitizing any data that’s being sent back out to the user from the database
* Checking open source libraries for vulnerabilities before using them

## **PHASE 4: VERIFICATION**

The **Verification** phase is where applications go through a thorough testing cycle to ensure they meet the original design & requirements. This is also a great place to introduce automated security testing using a variety of technologies. The application is not deployed unless these tests pass. This phase often includes automated tools like CI/CD pipelines to control verification and release.

**Verification at this phase may include:**

* Automated tests that express the critical paths of your application
* Automated execution of application unit tests that verify the correctness of the underlying application
* Automated deployment tools that dynamically swap in application secrets to be used in a production environment

## **PHASE 5: MAINTENANCE & EVOLUTION**

The story doesn’t end once the application is released. In fact, vulnerabilities that slipped through the cracks may be found in the application long after it’s been released. These vulnerabilities may be in the code developers wrote but are increasingly found in the underlying open-source components that comprise an application. This leads to an increase in the number of “zero-days”—previously unknown vulnerabilities that are discovered in production by the application’s maintainers.

These vulnerabilities then need to be patched by the development team, a process that may in some cases require significant rewrites of application functionality. Vulnerabilities at this stage may also come from other sources, such as external penetration tests conducted by ethical hackers or submissions from the public through what’s known as “bug bounty” programs. Addressing these types of production issues must be planned for and accommodated in future releases.
