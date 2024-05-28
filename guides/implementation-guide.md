# Implementation Guide

### Reimagining & building for new domains on the DIGIT platform

1. Install DIGIT core using the [Installation Guide](../get-started/installation-guide/). It is not recommended to customize DIGIT core platform components. Please raise issues or PRs for bug fixes. Raise questions in the DIGIT discussion board.&#x20;
2. Deploy the DIGIT UI build from the published [service build updates.](../accelerators/ui-frameworks/service-build-updates.md)
3. Verify the deployment by setting up the Public Grievances Redressal (PGR) (optional). Or ensure that all services are in running state in the Kubernetes cluster.&#x20;
4. Verify that the Citizen portal is available at `<hostname>/digit-ui/citizen`.&#x20;
5. Verify that the Employee portal is available at `<hostname>/digit-ui/employee`.
6. For further customisations of existing DIGIT UI modules or to build new modules, please fork the latest [release tag](https://github.com/egovernments/DIGIT-Frontend/tags) from the [DIGIT-Frontend](https://github.com/egovernments/DIGIT-Frontend) repository. Check the [service build updates](../accelerators/ui-frameworks/service-build-updates.md) page for a description of the UI releases to pick the appropriate release.
7. If you are building a new domain on the DIGIT platform, start with a clean slate with only basic UI modules. Please fork the [quick start tag](https://github.com/egovernments/DIGIT-Frontend/releases/tag/quick-start-v1.0) from [DIGIT-Frontend](https://github.com/egovernments/DIGIT-Frontend). Start to add new UI modules as folders within the [micro-ui-internals folder](https://github.com/egovernments/DIGIT-Frontend/tree/master/micro-ui/web/micro-ui-internals).&#x20;

