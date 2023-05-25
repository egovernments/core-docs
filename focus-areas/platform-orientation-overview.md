# Platform Orientation - Overview

## Introduction <a href="#introduction" id="introduction"></a>

This document serves as a briefing and overview of the core architecture and components of the platform for a new or unfamiliar developer. It seeks to address the what, why, and how of the platform at the time of writing. It is also meant to be a collaborative exercise, written by newbies for newbies, with future developers adding their own insights and learnings to this resource to have it grow with the platform over time.

This is **NOT** a technical reference or documentation. It is intended for orientation and will be written in natural language wherever possible. It is also limited in its scope to the general architecture of the back end, with little regard to how the systems necessarily converge to provide product solutions.

## Architecture Components

### The Goal <a href="#the-goal" id="the-goal"></a>

By the end of this document, you will be able to completely comprehend the following paragraph. It will equip you to understand the terminology, the tools, the features, and the implicit assumptions therein as well as provide you with solid grounded reasoning on why the architecture is the way that it is. The paragraph is an elevator pitch of the platform architecture, and it looks something like this:

In brief, the platform stack uses nginx servers with Zuul gateways to host Spring Boot microservices stored in Docker containers managed using Kubernetes. The servers rely on Kafka data streams to provide them with data that is indexed in ElasticSearch, and persisted in PostgreSQL databases.

Here’s what you need to know.

## The Components & Why <a href="#the-components-and-why" id="the-components-and-why"></a>

### nginx <a href="#nginx" id="nginx"></a>

**Definition:** nginx (pronounced “Engine X”) is a web server designed to serve dynamic HTTP content fast. It serves 32% of all active websites on the internet as of 2019, making it the world’s most popular web server.

A server in this context is a computer on a network that holds some form of content and provides it when needed i.e. “serves” it.

**Functionality:** Nginx uses a modular event-driven architecture to handle requests asynchronously, rather than through threads. “Event-driven” means it performs actions as a reaction to things happening in its environment (such as requests for information, or changes in values), as opposed to constantly staying in action to function (which is what threading does).

**Why nginx:** Nginx is substantially faster than Apache at a fraction of the processor cost because the narrow scope of a microservice server means that the configuration is highly specialized making it more efficient than a feature-rich server which would do more but run slower.

Because the platform microservices are all HTTP driven, a server that is optimized for fast dynamic HTTP processing makes logical sense.

### Zuul <a href="#zuul" id="zuul"></a>

**Definition:** Zuul is an open-source API gateway service developed and provided by Netflix. An API Gateway is a service that manages access control to a server that is hosting an API, which means that it can handle things like service requests that involve sending and receiving program operation-specific data and parameters and is custom-built for that purpose.

**Functionality:** Zuul acts as a proxy, accepting all incoming API requests and authenticating them before delegating them to the microservice in question. This means that whenever an app or a product is requesting or calling a microservice, it is actually connecting to Zuul first, rather than directly to the server. Once Zuul okays the request, it hands off to the server.

**Why Zuul:** Zuul provides two benefits: it acts as a wrapper on the internal mechanics of the microservices, meaning that any internal functionality concerns are irrelevant to any external clients. It also simplifies the server gateway and access system, allowing for a single configuration of authentication protocols to suffice for every deployed microservice. In the absence of a common gateway, authentication would have to be individually defined on every server access point, which would be tedious and redundant.

### Spring Boot <a href="#spring-boot" id="spring-boot"></a>

**Definition:** Spring is an application framework for Java, or the environment in which a java application runs. Spring Boot is an opinionated instance of the Spring framework, which means that it is automatically preconfigured in the way most Java application frameworks tend to be configured on average.

**Functionality:** The opinionated configuration of Spring Boot means that a developer does not need to be spending time and resources to install the libraries and dependencies required for a specific Java application. They are all present at the time of deployment and only highly specialized dependencies need to be installed after the fact.

**Why Spring:** Because the platform consists of a large number of microservices where the individual functionalities of a given service are defined very simply, it is unlikely that highly specialized dependencies will be required for a non-opinionated configuration to be required or viable. Therefore, an opinionated instance that includes all the commonly required dependencies by design is an ideal match for the framework requirements for a project such as this.

### Kafka <a href="#kafka" id="kafka"></a>

**Definition:** Kafka is a real-time data streaming service. It allows other systems to subscribe or publish to a data stream (a sequence of data that updates asynchronously in real-time).

**Functionality:** Kafka acts as the backbone of the server architecture, handling data transfer between the databases and the microservices, as well as other platform entities that require access to data and functionality elements. It creates streams of information that services and network entities can either publish or subscribe to.

**Why Kafka (or why Data Streaming):** Data streaming in general, and Kafka in particular, address an important aspect of microservice architecture design. Inter-service communication plays a larger role in the functionality of such architecture over traditional service architectures, and being able to reliably and efficiently provide data to all the microservices active at a given time during runtime is essential to the platform working as intended.

With streaming, services that need data can request it independent of each other without affecting the functionality of others (a key advantage of a pub/sub model) and the data can be reliably expected to be up-to-date. With distributed streaming infrastructures like Kafka, scaling up to accommodate larger and more complex microservice deployments also becomes easier.

## ElasticSearch

**Definition:** ElasticSearch is a search engine. It provides text-based search functionality across an indexed database.

**Functionality:** ElasticSearch allows for searching across all kinds of documents, including specifically schema-less JSON objects. It is quasi-real time, allows its database indices to be sharded (horizontally partitioned) with shard-level replication as well as distributed computation and storage.

ElasticSearch is complemented by Logstash, a data collection and logging system and Kibana, an analytics and visualization dashboard. These three tools, combined with Beats, a lightweight data shipper (not being used in the architecture) are collectively named the Elastic Stack.

**Why the Elastic Stack:** The Elastic stack is self-contained and highly functional, ideal for the “just works” configuration that is needed for scalable systems. Specifically, ElasticSearch is a more efficient method of searching the database since the query runtime is faster on indexed Elastic than on indexed relational databases. It works in tandem with the slower but more robust relational database to provide faster data access.

## PostgreSQL

**Definition:** PostgreSQL is an open-source relational database management system developed by the Ingres team at the University of California, Berkeley.

**Functionality:** PostgreSQL is a fully functional RDBMS that is market competitive with other open source and proprietary database management tools. A full list of the features it offers would be slightly redundant to add to this document, but it could be introduced at a later date.

**Why PostgreSQL:** PostgreSQL has one real advantage over other forms of open source RDBMS in that it is slightly faster. MySQL will run slower on average on certain specific query cases and corner cases. Furthermore, there is a consensus in the platform development community that a move to PostgreSQL is inevitable in all but the most legacy of systems. Non-Postgres systems at large scale are only really being maintained because migration would be too resource-intensive to be worthwhile.

### Docker <a href="#docker" id="docker"></a>

**Definition:** Docker is virtualization software that creates lightweight virtual environments called containers in which programs can be run with their own unique configuration of libraries, dependencies, and setups. Because all Docker containers run on one OS kernel, they are less resource intensive than virtual machines (which instantiate a new OS for every virtualization).

**Functionality:** Docker uses Linux functionality like cgroups (which allows for compartmentalizing hardware resources) and namespaces to isolate the containers without having to create a new instance of the kernel for every virtualization.

Docker containers are also ephemeral, in that they only exist for as long as it is needed for the app or service running within the container to perform the necessary task, after which it is cleaned up.

**Why Docker:** Virtualization and containers are advantageous for a distributed scaled system because of the ease of configuration for individual microservice functionality. This in turn lowers the size of the resultant code base, as well as allows for constant delivery (since the entire stack does not need to be taken down to instantiate a new container for a new microservice).

### Kubernetes <a href="#kubernetes" id="kubernetes"></a>

**Definition:** Kubernetes is an open-source container orchestration platform that allows for automating the container deployment, maintenance, and scaling process.

**Functionality:** Kubernetes consolidates containers into pods, which are groups of containers guaranteed to be hosted in a single location and can share resources. These pods are then organized into services, where the containers are all intended to interact with each other. These are deployed in Kubernetes Nodes on the API server architecture, which are accessed by clients via the Kube-proxy interface.

**Why Kubernetes:** By design, Kubernetes and by extension the container architecture it facilitates, meet a lot of the concerns and requirements of microservice architectures. Over time, as the system complexity increases, the automation of container management means that the service can be scaled and managed without hindering functionality, provided the core design is consistent with the problem it is attempting to solve.

### Putting it All Together <a href="#putting-it-all-together" id="putting-it-all-together"></a>

#### Revisiting the Elevator Pitch <a href="#revisiting-the-elevator-pitch" id="revisiting-the-elevator-pitch"></a>

> In brief, the platform stack uses nginx servers with Zuul gateways to host Spring Boot microservices stored in Docker containers managed using Kubernetes. The servers rely on Kafka data streams to provide them with data that is stored indexed in ElasticSearch, and persisted in PostgreSQL databases.

Now that you have read the document, you should be better equipped to understand what that means, as well as the raison d’être for its current state. You should also be cognizant of the context in which the platform functions, and the nature of the solutions it is capable of providing.

Most importantly, you are now ready to jump into the technical documentation and be able to put it in perspective with the system at large, while being able to focus on the specific aspect with which you are concerned.

#### What Now? <a href="#what-now" id="what-now"></a>

Still doesn’t make sense? Feels like something is missing. Is everything in this document wrong and bad and you can’t believe someone actually wrote this stuff out? Don’t worry! This is a collaborative effort, and your contribution will be most welcome. Ping the author(s), leave a comment, or better yet, edit the document yourself and keep improving it. The more the better.

Over time, this document is intended to help any new team members become familiar and capable with the platform and anything you design worthy of adding to their knowledge should be added here.

If you’re good to go, however, then get in touch with your team and they will let you know what is next.\
