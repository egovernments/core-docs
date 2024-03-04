---
description: >-
  DIGIT Quickstart is recommended to jump-start with minimal DIGIT services to
  get a sense of the various installation steps and system requirements.
---

# Quick Setup

#### Topics Covered:

* [Quickstart basics](./#overview)
* [Hardware pre-requisites](./#hardware-pre-requisites)
* [Required checks](./#required-checks)
* [Quickstart steps](./#quickstart-setup)

## Overview

DIGIT Quickstart setup helps in installing the DIGIT Infra on a local machine/VM. This installation is not meant for production use. However, this quick setup flow familiarizes users with the key production-grade setup processes.

Quickstart is recommended for basic infra types like a local machine, setting up on a single VM, etc. This setup creates a lightweight Kubernetes ([k3d](https://github.com/rancher/k3d) ) cluster which does not require a full-fledged cloud setup or multiple VMs. Refer to the open-source project [k3d](https://github.com/rancher/k3d) to learn more. Install the k3d on a local or on a VM once all the pre-requisites and hardware requirements specified below are met.

## Hardware Pre-requisites

To install k3d, ensure the instance meets the following hardware requirements to ensure sufficient CPU and memory in default systems and meets the DIGIT setup requirement.

Apart from the regular system usage, DIGIT requires the following dedicated CPU/Memory specs:

* An admin/[sudoer](https://medium.com/kernel-space/linux-fundamentals-a-to-z-of-a-sudoers-file-a5da99a30e7f) access to proceed
* OS: Ubuntu 18.04 or Debian 10 or Windows 10 or Mac OSX
* Local machine or VM or bare metal
* 16 GiB of RAM (recommend 20+)
* 30 GiB of HDD (recommend 40+)
* NAT or Bridged networking with access to the internet

## Required Checks

Before proceeding with DIGIT quick setup - Check the machine's remaining CPU/Memory capacity. Use the following commands to fetch the memory details. The commands vary from OS to OS. Click on the specific OS option below to view the instructions.

<details>

<summary>Windows - On Command Prompt</summary>

`systeminfo |find "Physical Memory"`

</details>

<details>

<summary>Linux - On Terminal</summary>

`free -m`

</details>

<details>

<summary>Mac - On terminal</summary>

**To Check Memory**: `top -l 1 -s 0 | grep PhysMe`

`Sample Output:` PhysMem: 16G used (3855M wired), 273M unused. &#x20;

(Here memory is not sufficient, it should at least be 8GB)



**To Check CPU:** `top -l 2 | grep -E "^CPU"`

`Sample Output:` \
CPU usage: 8.46% user, 12.86% sys, 78.66% idle \
CPU usage: 10.94% user, 8.11% sys, 80.93% idle

Here the CPU is sufficient where >30% is left over for the DIGIT setup to be done.

</details>

<mark style="color:red;">**Note: The output of the commands in the above links provides the total memory/CPU and unused/free/available memory/CPU details. Make sure the unused/free/available memory matches the following specs:**</mark>

* <mark style="color:red;">**Memory: 8GB**</mark>
* <mark style="color:red;">**CPU: >30%**</mark>

## Quickstart Setup

Once the above prerequisites are met, proceed with the following steps -&#x20;

{% content-ref url="1.-choose-infra.md" %}
[1.-choose-infra.md](1.-choose-infra.md)
{% endcontent-ref %}

{% content-ref url="2.-deployment.md" %}
[2.-deployment.md](2.-deployment.md)
{% endcontent-ref %}

{% content-ref url="faq.md" %}
[faq.md](faq.md)
{% endcontent-ref %}

## Useful Links <a href="#quickstart-setup" id="quickstart-setup"></a>

{% embed url="https://urban.digit.org/products/training-and-demo/training-videos#quickstart" %}
Quickstart walkthrough videos
{% endembed %}

