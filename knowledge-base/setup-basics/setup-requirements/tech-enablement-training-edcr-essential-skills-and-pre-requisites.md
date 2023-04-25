# Tech Enablement Training (eDCR) - Essential Skills & Pre-requisites

## Introduction

This document aims to put together all the items which will enable us to come up with a proper training plan for a partner team who will be working on the eDCR service used for the plan scrutiny.

## Technical Pre-requisites

Below listed are the technical skillsets that are required to work on eDCR service. It is expected that the team planning on attending training is well versed with the mentioned technologies before they attend eGov training sessions.

### Development Team Skillset

* Java and REST APIS
* Postgres
* Maven
* Spring framework
* Basics of 2D CAD Drawings
* Git
* Postman
* YAML/JSON

### DevOps Team Skillset

* Strong working knowledge of Linux, command, VM Instances, networking, storage
* The session, cache, and tokens handling (Redis-server)
* Understanding of VM types, Linux OS types, LoadBalancer, VPC, Subnets, Security Groups, Firewall, Routing, DNS
* Experience setting up CI like Jenkins and creating pipelines
* Artifactory - Nexus, verdaccio, DockerHub, etc
* Experience in setting up SSL certificates and renewal
* Gitops, Git branching, PR review process. Rules, Hooks, etc.
* JBoss Wildfly, Apache, Nginx, Redis and Postgres

### Hardware Pre-requisites

Trainees are expected to have laptops/ desktops configured as mentioned below with all the software required to run the eDCR service application

* Laptop for hands-on training with 16GB RAM and OS preferably Ubuntu
* All developers need to have Git ids
* Install VSCode/IntelliJ/Eclipse
* Install [Git](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or higher](http://www.oracle.com/technetwork/java/javase/downloads)
* Install [maven v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL v9.](http://www.postgresql.org/download/)6
* Postman
* Install LibreCAD
* Application Server [JBoss Wildfly v11.x](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip)

### Software Assets

There are knowledge assets available on the Net for general items and eGov assets for DIGIT services. Here you can find references to each of the topics of importance. It is mandated the trainees do a self-study of all the software mentioned in the prerequisites using the reference materials shared.

| Topic               | Reference                                                                                                                                                                                                                                                                                                                                                | Preparedness Check                                                                                                                                                             |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Git                 | ​[https://www.atlassian.com/git](https://www.atlassian.com/git)​​[https://www.tutorialspoint.com/git/index.htm](https://www.tutorialspoint.com/git/index.htm)​​[https://www.udemy.com/course/git-complete/](https://www.udemy.com/course/git-complete/)​                                                                                                 | Do you have a Git account?Do you know how to clone a repository, pull updates, push updates?Do you know how to give a pull request and merge the pull request?                 |
| Postgres            | ​[https://www.postgresqltutorial.com/](https://www.postgresqltutorial.com/)​​[https://www.udemy.com/course/the-complete-python-postgresql-developer-course/](https://www.udemy.com/course/the-complete-python-postgresql-developer-course/)​​[https://www.tutorialspoint.com/postgresql/index.htm](https://www.tutorialspoint.com/postgresql/index.htm)​ | How to create database and set up privileges?How to add index on table?How to use aggregation functions in psql?                                                               |
| Postman             | ​[https://www.postman.com/resources/videos-tutorials/](https://www.postman.com/resources/videos-tutorials/)​​[https://www.udemy.com/course/postman-the-complete-guide/](https://www.udemy.com/course/postman-the-complete-guide/)​                                                                                                                       | Call a REST API from Postman with proper payload and show the responseSetup any service locally(MDMS or user service has least dependencies) and check the API’s using postman |
| REST APIs           | ​[https://www.tutorialspoint.com/rest\_api/index.asp](https://www.tutorialspoint.com/rest\_api/index.asp)​​[https://www.youtube.com/watch?v=rtWH70\_MMHM](https://www.youtube.com/watch?v=rtWH70\_MMHM)​                                                                                                                                                 | What are the principles to be followed when making a REST API?When to use POST and GET?How to define the request and response parameters?                                      |
| JSON                | ​[https://www.tutorialspoint.com/json/index.htm](https://www.tutorialspoint.com/json/index.htm)​​[​<img src="https://github.com/fluidicon.png" alt="" data-size="line">json-path/JsonPath](https://github.com/json-path/JsonPath)​                                                                                                                       | How to write filters to extract specific data using jsonPaths?                                                                                                                 |
| YAML                | ​[https://www.udemy.com/course/yaml-essentials/](https://www.udemy.com/course/yaml-essentials/)​                                                                                                                                                                                                                                                         | How to read an API contract using swagger?                                                                                                                                     |
| Maven               | ​[https://www.udemy.com/course/maven-quick-start/](https://www.udemy.com/course/maven-quick-start/)​​[https://www.tutorialspoint.com/maven/index.htm](https://www.tutorialspoint.com/maven/index.htm)​                                                                                                                                                   | What is POM?What is the purpose of maven clean install and how to do it?What is the difference between version and SNAPSHOT?                                                   |
| eDCR Approach Guide | ​[eDCR Approach Guide](https://digit-discuss.atlassian.net/l/c/Gh0kEwC6)​                                                                                                                                                                                                                                                                                | How to configuring and customizing the eDCR engine as per the state/city rules and regulations.                                                                                |
| eDCR Service setup  | ​[Development Control Rules (Digit-DCR)](https://digit-discuss.atlassian.net/l/c/gLYMCaS7)​​[Setting Up eDCR Service](https://digit-discuss.atlassian.net/l/c/8s5or1tz)​                                                                                                                                                                                 | Overall Flow of eDCr service, design and setup process                                                                                                                         |

​
