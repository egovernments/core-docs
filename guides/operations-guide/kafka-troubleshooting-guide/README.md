---
description: This doc is about a Kafka troubleshooting guide
---

# Kafka Troubleshooting Guide

## Pre-reads

[https://kafka.apache.org/intro](https://kafka.apache.org/intro)\
[https://zookeeper.apache.org/](https://zookeeper.apache.org/)

### Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
* [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
* Git

### Status check of Kafka Broker's&#x20;

Using the below command you can able list down the Kafka brokers and their status

`kubectl get pods -n kafka-cluster`

*   If Kafka brokers are in crashloopbackoff or Error status

    *   Describe the brokers and look for error

        `kubectl describe kafka-v2-0 -n kafka-cluster`

    &#x20;  `kubectl describe kafka-v2-1 -n kafka-cluster`

    &#x20;  `kubectl describe kafka-v2-2 -n kafka-cluster`
*   &#x20;Check Kafka broker's logs for error

    `kubectl logs -f kafka-v2-0 -n kafka-cluster`&#x20;

    `kubectl logs -f kafka-v2-1 -n kafka-cluster`&#x20;

    `kubectl logs -f kafka-v2-2 -n kafka-cluster`
*   If brokers are in crashloopbackoff due to disk space issues, follow the below document for the cleanup of the logs

    * [Cleanup of Kafka logs](https://core.digit.org/guides/operations-guide/cleanup-kafka-logs)



### Status check of Zookeeper

Ensure Zookeeper pods are running without any errors in order to run Kafka brokers without a hitch

* If Zookeeper pods are in crashloopbackoff or Error status, Use the below commands to check the error
  *   Describe the Zookeeper and look for error

      `kubectl describe zookeeper-v2-0 -n zookeeper-cluster`

      `kubectl describe zookeeper-v2-1   -n zookeeper-cluster`

      `kubectl describe zookeeper-v2-2 -n zookeeper-cluster`
  *   &#x20;Check Kafka broker's logs for error

      `kubectl logs -f zookeeper-v2-0 -n zookeeper-cluster`&#x20;

      `kubectl logs -f zookeeper-v2-1 -n zookeeper-cluster`&#x20;

      `kubectl logs -f zookeeper-v2-2 -n zookeeper-cluster`

