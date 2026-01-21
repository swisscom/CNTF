# 3 - Observability

## 3 - 1 Definition

Observability is the ability to understand the state and behaviour of a system based on the outputs it produces. An observable software system provides enough information about its performance and internal state to enable users or automation to derive insights and take corrective action when needed. In the context of cloud-nativeness, observability becomes critical due to the highly distributed nature of the cloud, the complexity of modern applications, and the interactions across multiple layers of infrastructure. It is therefore essential to have an observable architecture that can pinpoint problems before they occur and support rapid remediation.

In the telecom domain, the traditional integrated node design served as the aggregated source of hardware, software, configuration, network function service delivery, and telemetry. With cloudification, this changes: the lifecycle of a network function service is decoupled from the underlying hardware and platform services. The separation of shared infrastructure, shared platform services, and dedicated application software results in telemetry being emitted independently from each disaggregated aspect of the system. There is no longer a single telecommunications node that aggregates these signals automatically, which has major consequences for observability.

According to the Cloud Native Computing Foundation (CNCF), "Observability is a system property that defines the degree to which the system can generate actionable insights. It allows users to understand a system's state from these external outputs and take (corrective) action. […]” Consequently, how observable a system is will significantly impact its operating and development costs." Translating this into the telco domain implies that telemetry data must be collected across all layers of a distributed and disaggregated application stack, processed, and made available-both to human operators and to automation systems-to fulfil multiple operational needs, such as service assurance, monitoring, closed-loop automation, and root-cause analysis. All telemetry data must also carry contextual metadata to enable meaningful interpretation.

A common cloud-native approach relies on three raw telemetry data types, often referred to as the three pillars of observability:

1. Metrics: Quantitative measures of system or application performance, or business-defined indicators, typically stored in time-series databases.
2. Logs: Structured or unstructured textual records that provide insight into runtime behaviour and context across applications and infrastructure.
3. Traces: Information about the path of a request across different services in a distributed architecture, enabling visibility into distributed transactions.

From these raw data types, additional insights-such as alerts and fault indications-can be derived through correlation and analysis. To implement observability at scale, it is common practice to combine appropriate tools and frameworks into an "observability stack."

A cloud-native observability approach typically includes the following concepts:

- Scraping and externalizing raw telemetry from data sources across the cloud stack.
- Providing a control plane for dynamic configuration of telemetry type and granularity.
- Storing telemetry data in a centralized, persistent data store so it can be collected once and shared across multiple consumers.
- Exposing telemetry and its schemas via interfaces that support flexible queries.
- Post-processing telemetry data (aggregation, correlation, analysis) by dedicated data consumption components to support the desired observability use cases.

## 3 - 2 External References

- [CNCF Observability definition](https://glossary.cncf.io/observability/)
- [Cloud-Native Observability of Telco Apps, Ericsson](https://www.ericsson.com/en/reports-and-papers/ericsson-technology-review/articles/cloud-native-observability-of-telco-apps)
- [Observability Whitepaper, v1.0 - CNCF TAG Observability, 2023](https://github.com/cncf/tag-observability/blob/whitepaper-v1.0.0/whitepaper.md)
- [Cloud Native Observability: Hurdles remain to understanding the health of systems](https://www.cncf.io/wp-content/uploads/2022/03/CNCF_Observability_MicroSurvey_030222.pdf)

## 3 - 3 Pain Points

The main challenge in observability is to properly define what outputs of the system or software need to be observed. Teams need to define the right metrics to monitor, generate meaningful logs and tracings. To achieve this, several teams and profiles need to collaborate such as (but not limited to): developers, DevOps engineers and product managers.

Furthermore, the significantly large and diversified landscape of observability tools result in an additional burden for organizations to handle their observability stack, with some tools lacking proper documentation or being hard to install and operate, this tendency has been reported by a micro-survey from CNCF in 2022.

### Disaggregated and distributed applications

As the cloud-native telco applications are deployed in a disaggregated and distributed manner, there is no possibility to expose a network function service view from within the applications. The realizing SW components do not, and should not, have the full visibility of all layers of the cloud stack. In a similar manner, the shared cloud platforms and infrastructure are agnostic to the service functions provided by the SW components deployed on them. That leads to telemetry data streams from the independent data sources of the layers of the cloud stack which need to be aggregated and correlated to create the desired network function service view. Despite this, the requirement is still the same as pre-cloud native applications, to provide a network function service view, and the most common requirement is to do so from the application.

### Ephemeral data sources

The SW components of the cloud-native telco applications are containerized and deployed on supporting container platforms. The container instances are ephemeral objects which are terminated and re-instantiated in an arbitrary way by the scheduling container control plane. The SW components which act as telemetry data sources therefore have a different lifetime than the required availability of the telemetry data itself.

### Unstructured data

Many of the SW components realizing the applications and the underlying cloud stack emit telemetry data, especially logs and event information, in an unstructured format. Even though that information might be human readable, for automated machine processing of that data it is difficult to aggregate and correlate unstructured data from different sources, potentially even with different semantics behind the data.

### Data volume

The sheer amount of data sources, especially when considering a complete network, leads to an immense potential volume of telemetry data which then needs to be collected and stored. The full amount of that data cannot be transported and persisted, as it will exceed the available bandwidth of the management network and the available storage capacity. Telemetry data generation and collection need to be configured and controlled to limit the volume.

### Data traceability

The telemetry data scraped from the multiple data sources of the different layers of the cloud stack often lacks consistent identifiers of its sources. Even if the data objects are tagged with meta-data from their origin, the values cannot be correlated externally from their source domain. The semantics of the meta-data structure are not aligned in between the data sources.

## 3 - 4 Harmonized Productivity Gains Quantified

## 3 - 5 CNTF’s ask to ISV or F/OSS

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A3-1.001 | Telemetry data should be structured: To enable consistent post-processing, all observability data should be structured according to well defined and versioned schemas. |
| AREQ A3-1.002 | Telemetry data should be traceable to its source: Each record and metric of the generated data should be traceable in at least two dimensions: time & place. Consistent source IDs are required. |
| AREQ A3-1.003 | Telemetry data life cycle shall be de-coupled from its source: The data needs to be available after the lifetime of its ephemeral data source. |
| AREQ A3-1.005 | Telemetry data persistency: Observability data shall be persistently stored separately of the data source, while local caching is permitted. |
| AREQ A3-1.006 | Telemetry data access and control: The access to the observability data to authorized users needs to be preserved. The collection and exposure of the observability data can be controlled and configured. |

## 3 - 6 CNTF’s ask to CSP readiness

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A3-2.001 | Ability to consume new types of telemetry data |
| AREQ A3-2.002 | Mindset change to understand concepts and consequences of cloud-native deployments on observability and adapt or swap out southbound interfaces of today’s tooling and management systems |
| AREQ A3-2.003 | Ability to integrate new telemetry interfaces from cloud platforms and interfaces. |

## 3 - 7 Testimonies
