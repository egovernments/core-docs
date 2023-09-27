---
description: Infrastructure resources required to deploy DIGIT
---

# Infrastructure Architecture

Various infrastructure resources required for DIGIT deployment can be provisioned from the AWS cloud manually. However, the best practice is to maintain consistency, automation, audit, reusability, and cost forecast. The use of infra-as-code using tools like [terraform](https://medium.com/tech-guides/terraform-zero-to-hero-733f6860bb9a) templates works well to this end.

![](<../../../.gitbook/assets/image (31) (1).png>)

## **Infrastructure Resources**

{% content-ref url="../../../focus-areas/devops/1.-how-dns-works.md" %}
[1.-how-dns-works.md](../../../focus-areas/devops/1.-how-dns-works.md)
{% endcontent-ref %}

{% content-ref url="../../../focus-areas/devops/2.-load-balancer.md" %}
[2.-load-balancer.md](../../../focus-areas/devops/2.-load-balancer.md)
{% endcontent-ref %}

{% content-ref url="../../../focus-areas/devops/3.-ssl-cert-manager.md" %}
[3.-ssl-cert-manager.md](../../../focus-areas/devops/3.-ssl-cert-manager.md)
{% endcontent-ref %}

1. [**Ingress Rules, WAF, SSL Termination**](../../../focus-areas/devops/4.ingress-waf.md)
2. [**VPC**](../../../focus-areas/devops/5.vpc.md)
3. [**Subnets (Private/Public, CIDR, Security Groups)**](../../../focus-areas/devops/6.subnets.md)
4. [**EKS (Managed Kubernetes Service)**](../../../focus-areas/devops/7.eks.md)
5. [**Worker Node Group (Autoscaling)**](../../../focus-areas/devops/8.worker-node-group.md)
6. [**RDS (Managed Database Service)**](../../../focus-areas/devops/9.rds.md)
7. [**NAT Gateway**](../../../focus-areas/devops/10.nat.md)
8. [**Internet Gateway**](../../../focus-areas/devops/11.internet-gateway.md)
9. [**Block Storage (EBS Volumes)**](../../../focus-areas/devops/12.block-storage-ebs-volumes.md)
10. [**Object Storage (S3)**](../../../focus-areas/devops/13.object-storage-s3.md)



