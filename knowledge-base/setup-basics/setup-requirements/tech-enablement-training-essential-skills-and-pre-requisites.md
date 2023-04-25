# Tech Enablement Training - Essential Skills and Pre-requisites

## Introduction <a href="#introduction" id="introduction"></a>

This document aims to put together all the items which will enable us to come up with a proper training plan for a partner team that will be working on the DIGIT platform.

## Technical Pre-requisites <a href="#technical-prerequisites" id="technical-prerequisites"></a>

Below listed are the technical skill sets that are required to work on the DIGIT stack. It is expected the team planning on attending training is well versed with the mentioned technologies before they attend eGov training sessions.

## Development Team Skillset <a href="#skillset-for-the-development-team" id="skillset-for-the-development-team"></a>

* Open API Contract - Swagger2.0
* YAML/JSON
* Postman
* Postgres
* Java and REST APIS
* Basics of Elasticsearch
* Maven
* Springboot
* Kafka
* Zuul
* NodeJS, ReactJS
* WordPress
* PHP

### DevOps Team Skillset <a href="#skill-set-for-the-devops-team" id="skill-set-for-the-devops-team"></a>

* Understanding of the microservice architecture.
* Experience with AWS, Azure, GCP, and NIC Cloud.
* Strong working knowledge of Linux, command, VM Instances, networking, and storage.
* To create Kubernetes cluster on AWS, Azure, and GCP on NIC Cloud.
* Kubectl installation & commands (apply, get, edit, describe k8s objects)
* Terraform for infra-as-code for cluster or VM provisioning.
* Understanding of VM types, Linux OS types, LoadBalancer, VPC, Subnets, Security Groups, Firewall, Routing, DNS)
* Experience setting up CI like Jenkins and creating pipelines.
* Deployment strategies - Rolling updates, Canary, Blue/Green.
* Scripting - Shell, Groovy, Python and GoLang.
* Experience in Baking Containers and Dockers.
* Artifactory - Nexus, Verdaccio, DockerHub, etc.
* Experience with Kubernetes ingress, setting up SSL certificates and renewal
* Understanding of Zuul gateway
* Gitops, Git branching, PR review process. Rules, Hooks, etc.
* Experience in Helm, packaging and deploying.
* JBoss Wildfly, Apache, Nginx, Redis and Postgres.

## Hardware Pre-requisites <a href="#hardware-prerequisites" id="hardware-prerequisites"></a>

Trainees are expected to have laptops/ desktops configured as mentioned below with all the software required to run the DIGIT application

* Laptop for hands-on training with 16GB RAM and OS preferably Ubuntu
* All developers need to have Git ids
* Install VSCode/IntelliJ/Eclipse
* Install [Git](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or higher](http://www.oracle.com/technetwork/java/javase/downloads)
* Install [maven v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL v9.](http://www.postgresql.org/download/)6
* Install [Elastic Search v2.4.x](https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-2.4.1.zip)
* Postman

## Software Assets <a href="#software-assets" id="software-assets"></a>

There are knowledge assets available in the Net for general items and eGov assets for DIGIT services. Here you can find references to each of the topics of importance. It is mandated the trainees do a self-study of all the software mentioned in the prerequisites using the reference materials shared.

| Topic                     | Reference                                                                                                                                                                                                                                                                                                                                                          | Preparedness Check                                                                                                                                                                               |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Git                       | ​[https://www.atlassian.com/git](https://www.atlassian.com/git)​​[https://www.tutorialspoint.com/git/index.htm](https://www.tutorialspoint.com/git/index.htm)​​[https://www.udemy.com/course/git-complete/](https://www.udemy.com/course/git-complete/)​                                                                                                           | Do you have a Git account?Do you know how to clone a repository, pull updates, push updates?Do you know how to give a pull request and merge the pull request?                                   |
| Microservice Architecture | ​[https://www.tutorialspoint.com/microservice\_architecture/index.htm](https://www.tutorialspoint.com/microservice\_architecture/index.htm)​​[https://www.udemy.com/course/microservices-with-spring-boot-and-spring-cloud/](https://www.udemy.com/course/microservices-with-spring-boot-and-spring-cloud/)​                                                       | Do you know when to create a new service?How to access other services?                                                                                                                           |
| ReactJS                   | ​[https://reactjs.org/tutorial/tutorial.html](https://reactjs.org/tutorial/tutorial.html)​​[https://www.udemy.com/course/react-the-complete-guide-incl-redux](https://www.udemy.com/course/react-the-complete-guide-incl-redux)​​[https://www.tutorialspoint.com/reactjs/reactjs\_overview.htm](https://www.tutorialspoint.com/reactjs/reactjs\_overview.htm)​     | How to create react app?How to create a Stateful and Stateless Component?How to use HOC as a wrapper?Validations at form level using React.js and Redux                                          |
| Postgres                  | ​[https://www.postgresqltutorial.com/](https://www.postgresqltutorial.com/)​​[https://www.udemy.com/course/the-complete-python-postgresql-developer-course/](https://www.udemy.com/course/the-complete-python-postgresql-developer-course/)​​[https://www.tutorialspoint.com/postgresql/index.htm](https://www.tutorialspoint.com/postgresql/index.htm)​           | How to create a database and set up privileges?How to add an index on a table?How to use aggregation functions in psql?                                                                          |
| Postman                   | ​[https://www.postman.com/resources/videos-tutorials/](https://www.postman.com/resources/videos-tutorials/)​​[https://www.udemy.com/course/postman-the-complete-guide/](https://www.udemy.com/course/postman-the-complete-guide/)​                                                                                                                                 | Call a REST API from Postman with proper payload and show the responseSetup any service locally(MDMS or user service has least dependencies) and check the API’s using postman                   |
| REST APIs                 | ​[https://www.tutorialspoint.com/rest\_api/index.asp](https://www.tutorialspoint.com/rest\_api/index.asp)​​[https://www.youtube.com/watch?v=rtWH70\_MMHM](https://www.youtube.com/watch?v=rtWH70\_MMHM)​                                                                                                                                                           | What are the principles to be followed when making a REST API?When to use POST and GET?How to define the request and response parameters?                                                        |
| Kafka                     | ​[https://www.udemy.com/course/apache-kafka/](https://www.udemy.com/course/apache-kafka/)​​[https://kafka.apache.org/intro](https://kafka.apache.org/intro)​​[https://www.tutorialspoint.com/apache\_kafka/apache\_kafka\_introduction.htm](https://www.tutorialspoint.com/apache\_kafka/apache\_kafka\_introduction.htm)​                                         | How to push messages on Kafka topic?How does the consumer group work?What are partitions?                                                                                                        |
| Docker and Kubernetes     | ​[https://www.tutorialspoint.com/kubernetes/index.htm](https://www.tutorialspoint.com/kubernetes/index.htm)​​[https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)​​[https://www.tutorialspoint.com/docker/index.htm](https://www.tutorialspoint.com/docker/index.htm)​ | How to edit deployment configuration?How to read logs?How to go inside a Kubernetes pod?How to create a docker file using a base image?How to port-forward the pod to the local port?            |
| JSON                      | ​[https://www.tutorialspoint.com/json/index.htm](https://www.tutorialspoint.com/json/index.htm) [json-path/JsonPath](https://github.com/json-path/JsonPath)​                                                                                                                                                                                                       | How to write filters to extract specific data using jsonPaths?                                                                                                                                   |
| YAML                      | ​[https://www.udemy.com/course/yaml-essentials/](https://www.udemy.com/course/yaml-essentials/)​                                                                                                                                                                                                                                                                   | How to read an API contract using swagger?                                                                                                                                                       |
| Zuul                      | ​[https://www.javatpoint.com/zuul-api-gateway](https://www.javatpoint.com/zuul-api-gateway)s                                                                                                                                                                                                                                                                       | What does Zuul do?                                                                                                                                                                               |
| Maven                     | ​[https://www.udemy.com/course/maven-quick-start/](https://www.udemy.com/course/maven-quick-start/)​​[https://www.tutorialspoint.com/maven/index.htm](https://www.tutorialspoint.com/maven/index.htm)​                                                                                                                                                             | What is POM?What is the purpose of maven clean install and how to do it?What is the difference between the version and SNAPSHOT?                                                                 |
| Springboot                | ​[https://www.tutorialspoint.com/spring\_boot/index.htm](https://www.tutorialspoint.com/spring\_boot/index.htm)​​[https://www.udemy.com/course/spring-hibernate-tutorial/](https://www.udemy.com/course/spring-hibernate-tutorial/)​                                                                                                                               | How does Autowiring work in spring?How to write a consumer/producer using spring Kafka?How to make an API call to another service using restTemplate?How to execute queries using JDBC Template? |
| Elastic search            | ​[https://www.udemy.com/course/elasticsearch-complete-guide/](https://www.udemy.com/course/elasticsearch-complete-guide/)​​[https://www.tutorialspoint.com/elasticsearch/index.htm](https://www.tutorialspoint.com/elasticsearch/index.htm)​                                                                                                                       | How to write basic queries to fetch data from elastic search index?                                                                                                                              |
| Wordpress                 | ​[https://www.tutorialspoint.com/wordpress/index.htm](https://www.tutorialspoint.com/wordpress/index.htm)​​[https://www.udemy.com/course/wordpress-for-beginners-course/](https://www.udemy.com/course/wordpress-for-beginners-course/)​                                                                                                                           | ​                                                                                                                                                                                                |
| DIGIT Architecture        | ​[Orientation - Platform Overview](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/85557250/Orientation+-+Platform+Overview)​​[DIGIT Architecture and Technical overview](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/112721941/DIGIT+Architecture+and+Technical+overview)​                                                               | What comes as part of core service, business service and municipal services?How to calls APIs from one service in another service?                                                               |
| DIGIT Core Services       | ​[Product requirements](https://digit-discuss.atlassian.net/l/c/DYNz7y84)​                                                                                                                                                                                                                                                                                         | Which are the core services in the DIGIT framework?                                                                                                                                              |
| DIGIT DevOps              | ​[DevOps Partners - KT Content](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/113705013/DevOps+Partners+-+KT+Content)​​[DIGIT Deployment](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/27459718/DIGIT+Deployment)​                                                                                                                      | ​                                                                                                                                                                                                |
| DIGIT MDMS                | ​[MDMS Configuration:](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/110952456)​                                                                                                                                                                                                                                                                      | How to read a master date from MDMS?How to add new data in an existing Master?Where is the MDMS data stored?                                                                                     |
| DIGIT UI Framework        | ​[Getting started](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/53051775/Egov+UI+framework)​                                                                                                                                                                                                                                                          | How to add a new component to the framework?How to use an existing component?                                                                                                                    |
| DSS                       | ​[Product - DSS](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/118554635/Product+-+DSS)​                                                                                                                                                                                                                                                               | ​                                                                                                                                                                                                |

​
