# 2 – Declarative Management

## 2 - 1 Definition

Configuration management for cloud-native systems across multiple layers involves processes, tools, and best practices for managing deployment, configuration and ongoing operations.

The layers are typically distinguished as follows, but may slightly vary in a specific deployment architecture

1. Functional/application layer: configuration of the actual functionality a network function provides to the network
2. Application/CNF software layer: configuration of the software composition and non-functional attributes of the software
3. Infrastructure layer: configuration of the infrastructure hosting the application/CNF including low-level connectivity and compute resources

The application/CNF software layer and infrastructure layer comprise the realization of a specific network function. Each layer, functional, application software and infrastructure, may cycle through different stages of configuration independently i.e. all layers have their own Day 0, 1, 2/n configurations.

In dynamic, distributed environments, there are many parameters that need to be planned, defined and provisioned and managed across versions, generations, change-management integration, validation and reconciled upon the live state to desired state discrepancies.

Note: User data management (HSS/UDM subscriber data provisioning) is using dedicated provisioning interfaces and is out of scope of this analysis

A cloud-native approach to configuration management would be:

- Moving away from direct imperative and sequential configuration in a day 0, 1, 2/n manner based on e.g. NETCONF, CLI, SNMP to a declarative source-of-truth mastered in GitOps and synced and reconciled e.g. with K8s operators.
- Non-repetitive configuration (day 0/1 templating) should be driven using Kubernetes ConfigMaps or Custom Resources with Schema.
- A network function should expose declarative APIs for configuration.
- Kubernetes Operators with specific scopes, e.g. provided by the NF supplier, should be used as an abstraction front-end for configuration. ETSI NFV defined functions such as VNFM/VNFO/EMS is put into many operators and such traditional dedicated systems will disappear.
- Management systems can access the networks via the abstraction layer based on K8s CRD/Operators.
- Instead of managing a flat model of well over 1000 parameters per Node, abstract configuration artifacts e.g. CRDs should be provided that reflect repetitive use cases of the business. Examples from the 5G Core Network Platform of such repetitive configuration tasks are:
  1. APN as a service (E2E incl. HSS/UDM/DNS and Packet Gateway)
  2. Packet inspection and service chaining/logic rules exposed as a service
  3. Service-aware charging rules exposed as a service
  4. Network Slicing (NSSAI/URSP) as a service (E2E)
  5. Radio Resource Partitioning as a service (on MME/AMF)
  6. Routing behaviour for P-GW/UPF contexts used by Private Networks.
  7. Installation of a new data plan (PCF)
  8. Management of Secrets & Certificates (E2E)
  9. Management of telemetry profiles (destination, datapoints, periodicity etc)
  10. IP/FQDN Claims for day 0 instantiation
  11. Primary & Secondary Network configuration incl. L2 provisioning
  12. Deployment of VMs or K8s Cluster as a Service and Namespace as a Service

## 2 - 2 External References

Multi-Intent Service Configuration Vision Whitepaper by L. Leuthold – July 22

## 2 - 3 Pain Points

Imperative protocols (Netconf, SNMP, CLI) instead of declarative cloud-native approaches (configmaps or Custom Resource Descriptions) lead to fire-and-forget operations and higher complexity (e.g. through configuration sequences) in configuration management. There are no APIs provided by the network functions to plan and design service logics and data plans characteristics.

Even having cloud native configuration management, it is still difficult to have an E2E service configuration from a design studio point of view. We believe that creating sections of configuration each having their own operator exposing APIs will help.

### Imperative Methodology

The current infrastructure deployment processes for K8s clusters and Switch Fabric configuration in Bare-Metal solutions are driven by an imperative, fire-and-forget methodology. This approach involves one-time push operations without continuous pull-based reconciliation. The lack of ongoing synchronization between the actual system state and the desired state defined in Git repositories can result in potential drifts and the need for manual corrections.

### Manual Interventions

Despite the integration of automation pipelines, significant manual interventions are still required in the overall process. Manually creating complex Low-Level Designs (LLDs) and pre-defining all the necessary information can be time-consuming and prone to errors. The current systems do not facilitate seamless and efficient changes, as configurations are often spread throughout intricate LLDs and input information is spread throughout the organization, making updates burdensome and slow

### End-to-End Automation Capability

Many deployments lack comprehensive end-to-end automation capabilities and coherent, streamlined processes, from Kubernetes cluster deployment to lifecycle management (LCM). This limitation translates into manual and error-prone efforts and waiting times due to task handovers and scheduling dependencies. Tasks such as cluster management, bootstrapping sidecars, overhead of management nodes, application-directed networking requirements (e.g., L2 isolation, LAG, Active-Passive NICs, SR-IOV vs. OV), and provisioning additional VLANs on L2 fabric in a cloud-native configuration management approach (as detailed in Area 2) add to the complexity and challenges faced.

### Vendor Tooling Landscape

The reliance on forked Open-Source tools within the tooling landscape provided by vendors has two consequences. Firstly, vendors must maintain their own forks and port upstream features into their customized versions, resulting in additional efforts and potential discrepancies. Secondly, telcos face difficulties in leveraging publicly available knowledge of the tools since the vendor-specific forks limit access to widely shared expertise and documentation.

Addressing these pain-points is crucial to streamline deployment processes, reduce manual interventions, and embrace end-to-end automation that aligns with cloud-native principles. By reevaluating the methodology, enhancing tooling landscapes, and focusing on standardization and continuous reconciliation, Swisscom can overcome these challenges and improve operational efficiency.

## 2 - 4 Harmonized Productivity Gains Quantified

Not possible as of now. This transformation has just started – we do not have success testimonies other than showcasing SDC and IaaS automation

## 2 - 5 CNTF’s ask to ISV or F/OSS

| Requirement   | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| AREQ A2-1.001 | IaaS Provisioning should be exposed by API or CRD/KRM based (Cluster API) and not performed by proprietary (somewhat closed) tools. This includes E2E Networking from MetalLB, external Networks (L2 fabrics) and remote order entry to other domains (such as DC networking) |
| AREQ A2-1.002 | Implement Kubernetes Operators to automate the management of infrastructure components, reducing the need for manual pre-definitions. |
| AREQ A2-1.003 | Continuously reconcile the actual system state with the desired state defined in Git repositories |
| AREQ A2-1.004 | Provide cloud native APIs to hydrate and push desired state to running state for supported infrastructure components including testing |
| AREQ A2-1.005 | Provide software enabling CSPs to manage the lifecycle of the clusters, handle updates, and ensure that the desired state is maintained |

## 2 - 6 CNTF’s ask to CSP readiness

| Requirement   | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| AREQ A2-2.001 | Git-based process for configuration management i.e. all configuration is applied via Git and NF-local configuration procedure (CLI) are disabled by default and only used in emergencies |
| AREQ A2-2.002 | Availability of observability systems to secure correct operations of the network functions beyond monitoring of the desired state |
| AREQ A2-2.003 | Input data for LLDs is available via APIs or stored in Git   |
| AREQ A2-2.004 | Harmonization of tooling landscape                           |

## 2 - 7 Testimonies

Lukas Leuthold, Swisscom:

> Swisscom has used SDC (schema driven configuration) to build a bridge from NETCONF to KRM based approach. With that, we can keep the configuration in GitOps and invest in the config management on service orchestration level to carry and provide management facility that are derived from the catalog, inventory or by user administrations. Config generation is done using Jinja2 Templates which allowed Swisscom to improve quality of day0 and day1 configurations and better align across environments (development, staging, production). Swisscom is actively developing automation processes to address limitations in the current vendor-provided solution. The existing approach requires complex static Low-Level Designs (LLDs) upfront for deploying and upgrading Kubernetes (k8s) clusters. However, the initial deployment cannot be seamlessly integrated with the necessary post-deployment steps to prepare the cluster for workloads. This leads to disjointed processes and difficulties in achieving a smooth end-to-end deployment experience. The rolling upgrade process, requiring significant manual intervention, is particularly time-consuming, resulting in delays and extending the process duration to 12-15 hours. This manual intervention hinders efficiency and operational speed. Resiliency tests have indicated that an imperative "Blackbox" approach should not handle the deployment of any add-ons. Instead, specialized software such as FluxCD/ArgoCD should be delegated to manage this task. By leveraging dedicated software, we can ensure the deployment of add-ons is separate and optimized for resilience. To effectively manage infrastructure-related resources, Swisscom aims to delegate these responsibilities to a management cluster equipped with CAPI controllers, aligning with CAPI architecture principles. This approach involves having a management cluster that controls and reconciles workload clusters. However, we currently observe limited capabilities to restore the state of the infrastructure after experiencing issues. The lack of robust reconciliation mechanisms often necessitates full redeployments as the only viable solution in the face of problems. Regarding the tooling landscape, Swisscom strives to prioritize the use of upstream solutions. However, adoption of these upstream solutions is sometimes hindered by compatibility issues with Cloud Native Functions (CNFs) provided by vendors, posing challenges in achieving seamless integration. To overcome these pain-points, Swisscom is actively working towards refining automation processes, streamlining upgrade procedures, improving resiliency strategies, and advocating for standardization and compatibility in the tooling landscape. By addressing these challenges head-on, we aim to enhance the efficiency, reliability, and overall robustness of our infrastructure deployment and management practices.
