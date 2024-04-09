---
description: Infrastructure resources required to deploy DIGIT
---

# Infrastructure Architecture

Various infrastructure resources required for DIGIT deployment can be provisioned from the AWS cloud manually. However, the best practice is to maintain consistency, automation, audit, reusability, and cost forecast. The use of infra-as-code using tools like [terraform](https://medium.com/tech-guides/terraform-zero-to-hero-733f6860bb9a) templates works well to this end.

![](<../../../.gitbook/assets/image (185).png>)

## **Infrastructure Resources**

{% content-ref url="../../../reference/devops/1.-how-dns-works.md" %}
[1.-how-dns-works.md](../../../reference/devops/1.-how-dns-works.md)
{% endcontent-ref %}

{% content-ref url="../../../reference/devops/2.-load-balancer.md" %}
[2.-load-balancer.md](../../../reference/devops/2.-load-balancer.md)
{% endcontent-ref %}

{% content-ref url="../../../reference/devops/3.-ssl-cert-manager.md" %}
[3.-ssl-cert-manager.md](../../../reference/devops/3.-ssl-cert-manager.md)
{% endcontent-ref %}

1. [**Ingress Rules, WAF, SSL Termination**](../../../reference/devops/4.ingress-waf.md)
2. [**VPC**](../../../reference/devops/5.vpc.md)
3. [**Subnets (Private/Public, CIDR, Security Groups)**](../../../reference/devops/6.subnets.md)
4. [**EKS (Managed Kubernetes Service)**](../../../reference/devops/7.eks.md)
5. [**Worker Node Group (Autoscaling)**](../../../reference/devops/8.worker-node-group.md)
6. [**RDS (Managed Database Service)**](../../../reference/devops/9.rds.md)
7. [**NAT Gateway**](../../../reference/devops/10.nat.md)
8. [**Internet Gateway**](../../../reference/devops/11.internet-gateway.md)
9. [**Block Storage (EBS Volumes)**](../../../reference/devops/12.block-storage-ebs-volumes.md)
10. [**Object Storage (S3)**](../../../reference/devops/13.object-storage-s3.md)



