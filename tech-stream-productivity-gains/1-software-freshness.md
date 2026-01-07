# 1 - Software Freshness

## 1 - 1 Definition

Software freshness refers to the extent to which software is kept up-to-date, secure, and in line with current standards, technologies, and requirements. It is essential to maintain optimal performance, compatibility, and safety.

To illustrate this, we can use the analogy of the cold chain, which is a temperature-controlled supply chain for perishable goods, ensuring their effectiveness and safety. Similarly, software freshness ensures that the perishable aspects of software, such as security, performance, and relevance, are preserved through continuous maintenance and updates.

It is crucial to regularly update software with patches, updates, and dependency versions to avoid any degradation in performance or (regulatory pushed) security. Neglecting these updates can pose significant risks, including security breaches, bugs, or becoming obsolete.

By adopting a continuous improvement approach with smaller and incremental changes across development, delivery, deployment and operations, it becomes easier to identify and fix issues in the early stages of development. This approach ensures that the software remains stable and of high quality over time. When updates are small and frequent, any introduced bugs are more likely to affect only a limited part of the system, minimizing the potential impact on the overall system. Consequently, it becomes easier to isolate and resolve issues without causing widespread disruption.

Software Freshness encompasses several key elements:

### 1. Always on Latest Software

The goal to be always on Latest Software and avoid touching software and/or configuration by hand. This applies to CSP taking that latest software from ISV, as well as for ISV to provide the latest stable version of supplied open-source software components.

### 2. Separation of Software Life-cycle Management and Functional Life-cycle Management

The ability to manage the software realization of a network function independent of the functionality it provides to the network. This means that a software package can be upgraded without impacting the function of the CNF in the network. Vice versa, it should be possible to turn on a functionality available in the software without changing the realization in software.

### 3. Continuous Software Flow

Developing small and lightweight software artifacts with a simple structure that enables fast and stable CI/CD pipelines. By incorporating widely used Cloud Native standards and best practices, such as OCI and Semantic Versioning, it ensures smooth operations and reduces operational expenses. Vendors should also support the integration of selected lifecycle automation tools to streamline processes.

### 4. In-service Software Update (ISSU)

Effective and seamless software lifecycle management is crucial for maintaining software freshness, security, and performance. Supporting in-service software and configuration upgrades allows for seamless updates without disrupting ongoing sessions. Changes should be as small and incremental as possible to help keep ISSU simpler and more robust. To this end, the recommendation for CSPs who are not yet ready to always run on the Latest Software, to resort to other upgrade mechanisms than ISSU, e.g. utilizing network level redundancy to maintain services during the upgrade procedure.

### 5. In-service Software Roll Forward / Rollback (ISSR)

As part of the software flow, the ability to seamlessly revert changes, whilst maintaining the NFs service is essential. The underlying strategies may vary including a roll forward to a fixed version or a roll back to apply a known-to-work software version or configuration. As for ISSU, the smaller the changes are the more robust this procedure is.

### 6. In-service Software Downgrade (ISSD)

In certain operational scenarios, the ability to downgrade software in-service is required to ensure continued network availability and adherence to service level expectations. An ISSD approach enables CSPs to revert to a previous software baseline while maintaining active sessions and without forcing a full service disruption. Similar to in-service upgrades and rollbacks, downgrade operations are most effective when changes between releases are kept minimal, reducing incompatibility risks and operational complexity. ISSD procedures may be triggered due to functional regressions, performance degradation, security vulnerabilities, or unforeseen behavioural changes introduced in newer releases. To ensure robustness, CSPs should verify backward compatibility across data models, configuration schemas, and state persistence. Where this cannot be guaranteed, network-level redundancy mechanisms may be leveraged to safeguard service continuity during the downgrade process.

### 7. Release Strategies

With the microservice architecture, a canary upgrade can be implemented to test new features/versionson a limited set of subscribers. This accelerates the deployment of changes into production in a more stable manner with a smaller blast radius. Testing will then happen either in staging/canary/labs or production. This means to accept failures in the release and having robust recovery mechanisms (as in A/B, canary…). Canary can happen on node (NF) level or CNF internal. We expect to align which strategy is being used in the industry to avoid double implementations and to understand the upsides and downsides of each option. There is the potential to roll-update whole NF sets.

Another key point is the separate “Functional” and “Realisation” levels.

\- Functional means to enable and expose a new feature/function to a limited or selected set of users (e.g. for 5G Core Network Platform: by UE types or IMSI range or Network Slice NSSAI).

\- Realisation means to bring in new software to the system only doing regression verification.

### 8. Continuous Feedback Flow to ISV or F/OSS community

Cloud Native brings increased focus on fast delivery and deployment of updated software components. There is an expectation of fast turn-around times and to facilitate that it is of highest importance to have an established feedback process to close to loop. An automatic continuous feedback flow from CSP to ISV is essential to achieve high quality software and fast turn-around when errors occur or security vulnerabilities need to be remedied.

Different types of data need to be collected and made available to ISV for different purposes:

- Software Pipeline Status and Health

- Artefact Pipeline Progress

- Cloud Infrastructure Configuration

- Software Configuration

- Application Configuration

- Application Feature Usage Information

- Test Result Information

- Traffic and Load Information

- Metrics and KPIs for Trend Detection

- Troubleshooting Information (e.g. logs, traces)

Source of feedback information can be CSP lab, staging and production environments. This enables the possibility to establish a lean pre-production automatic early feedback channel back to the Independent Software Vendor.

Agreements between information source owners and information receivers must be established. To adhere to regulatory requirements and privacy principles some information may have to be anonymized before transferring from CSP to ISV.

### 9. Division of Responsibility - Optimal Verification and Integration

Quality is assured as joint effort between ISV and CSP. Automated quality assurance activities will be conducted both in ISV and CSP environments, selecting the most appropriate environment for the task at hand. Generally applicable verification shall be shifted towards ISV, while CSP specific verification shall be shifted towards CSP. An aligned staging process and an established feedback loop is essential for this to be efficient.

The ISV defines the versions of opensource projects verified and supported in a product to ensure coherent integration and quality assurance. The cloud-native SW architecture can allow for replacement of opensource components by upstream versions, which in turn requires a modified responsibility split (e.g. SLA) between supplier and operator for the product, in which case E2E responsibilities will shift from the supplier to the operator.

### 10. Aligned Staging Process

To streamline the software flow from supplier to operations, staging environments are an essential asset. Staging environments exist both on the supplier side for testing and integration as well as on the operations side for integration into the local operations environment. We aim for an alignment of essential steps in the staging process to ensure consistent quality assurance and verification in an end-to-end process whilst avoiding duplicate activities.

### 11. Aligned Test Automation

An aligned test scope between supplier and operator is critical for an efficient feedback flow in which e.g. reference tests can be used to detect anomalies. Implementing automated testing after each software drop is essential. It should be integrated into the continuous integration/continuous deployment pipelines, providing a fully autonomous testing experience.

### 12. Regulatory Push for Security 30/60/90

This typically implies a staged plan or timeline to improve its cybersecurity posture . This might issue a 30/60/90-day remediation plan:
 By Day 30: Patch all high CVSS-score vulnerabilities.
 By Day 60: Implement MFA and logging for critical systems.
 By Day 90: Conduct a full risk assessment and train all staff.

### 13. Built for Automation

An efficient low-friction software flow requires all components and processes along the way to be built for automation. The software is provided with APIs for configuration alongside machine readable assets. The processes for ingesting, testing and deploying software in production defined by the operator do not include any manual steps and are fully automated and integrated with the automation provided by the Network Functions.

### 14. Non-Technical aspects

A lot of time is spent for assessing network impacts for a change, approvals in the process, scheduling maintenance activities, project planning and documentation. This will also define the delivery and ingestion process as such and how to first align, then streamline, and finally automate the process.

### 15. Bringing ISV Dev to CSP DevOps in a scalable manner

There are many examples of the successful use of cloud native principles and technologies in the IT industry, when Dev and Ops cooperate and optimize their activities for a single deployment environment accessible by both parties. This is different from a Telco setting with an N:M relation between ISVs and CSPs and intermediate delivery steps of complex software. This calls for a high level of alignment in terms of technology and WoW across the N and M, else the introduction of cloud native principles may not scale well and turn out counterproductive.

### 16. Accessibility of CSP stage (labs/tenants/slices) from ISV Dev side

To facilitate efficient troubleshooting and to streamline the feedback loop, the ability for an ISV developer to gather information on a CSP deployment is crucial. In addition to providing information about a deployment (see item 7) the ability to securely access CSP staging environments from ISV side in a controlled manner to gather more detailed data is needed for certain cases.

By embracing these practices, the software can maintain its freshness, ensuring it remains up-to-date, secure, and aligned with current standards and requirements.

## 1 - 2 External References

- <https://github.com/lfn-cnti/bestpractices/blob/main/doc/whitepaper/Accelerating_Cloud_Native_in_Telco.md>
- <https://www.ngmn.org/highlight/ngmn-publishes-cloud-native-manifesto.html>

## 1 - 3 Pain Points

We feel very limited to embrace Software Freshness because the delivery is still designed in a way that people “touch it”. The reality is the many traditional support and commissioning methods of the ISV are still needed. Software drops are too heavy, too long (low cadence) due to low CSP adoption of new software and industry requirements on robustness on CSP and vendor alike. The above definition is not realizable and CSPs must in-house develop tools and processes that would be best placed at vendor side for reusability and scale.

## 1 - 4 Harmonized Productivity Gains Quantified

Swisscom has demonstrated a remarkable reduction in the time required for manual deployment, reducing the process from 2.5 weeks to just 10 minutes. The significant progress made in this area highlights the potential to save approximately 8,000 hours of DevOps work within the DMC context in 2025. This accomplishment reinforces the existing pain points and emphasizes the scope for further productivity improvements. Our focus on addressing these challenges empowers us to enhance our overall efficiency and cultivate even greater productivity gains.

## 1 - 5 CNTF’s ask to ISV or F/OSS

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A1-1.001 | As expressed later in Area 2 the transition from an imperative to a declarative intent driven methodology where the desired state of the system is defined in a simple and abstract intent in Git repositories. Simplify LLDs to expose to engineers/service-mgmt tools, abstracted intent to reduce manual interventions and complex dependencies. Artifacts should be machine readable (MOPs or NIR) |
| AREQ A1-1.002 | Software images should be delivered via OCI |
| AREQ A1-1.003 | Software releases should follow Semantic Versioning |
| AREQ A1-1.004 | Software should be delivered with testing tools that allows easy automation of integration testing in the Operator’s environment |
| AREQ A1-1.005 | Canary rollouts should be supported by the Software |
| AREQ A1-1.006 | Vendor to show the granularity and timing of SW deliverables |
| AREQ A1-1.xxx | Availability of machine-readable delivery assets e.g. release notes |
| AREQ A1-1.xxx | Strive to deliver the latest stable version of supplied open-source software. |
| AREQ A1-1.xxx | Define relevant KPIs and data sets that are suitable to receive as feedback from CSP. |
| AREQ A1-1.xxx | Provide means to anonymize sensitive or personal information collected from the system. |
| AREQ A1-1.xxx | Develop tools and processes to handle information received from CSP in a safe manner. |

## 1 - 6 CNTF’s ask to CSP readiness

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A1-2.001 | Ability to run automatic regression testing |
| AREQ A1-2.002 | Pipeline capabilities |
| AREQ A1-2.003 | Availability of “testing” nodes: lab or canary |
| AREQ A1-2.004 | Availability of staging process and zone |
| AREQ A1-2.005 | Fully automated SW ingestion process / Software ingestion and update flow without manual steps defined |
| AREQ A1-2.006 | Approval flow via Git |
| AREQ A1-2.xxx | Ability to automatically process and act on machine readable delivery assets e.g. release notes |
| AREQ A1-2.xxx | Willingness to share relevant feedback information. |
| AREQ A1-2.xxx | Strive to deploy the latest stable version of ISV supplied software. |
| AREQ A1-2.xxx | Automatically collect feedback data and make it available to ISV. |
| AREQ A1-2.xxx | Provide necessary correlation information for ISV to be able to interpret feedback data. |

## 1 - 7 Testimonies

Lukas Leuthold, Swisscom:

> Swisscom has undergone a remarkable transformation, transitioning from productized CI/CD pipelines to a GitOps-centric approach. This shift has resulted in substantial improvements, with manual deployment time reduced from 2.5 weeks to a mere 10 minutes. However, the telco software industry still heavily relies on traditional manual practices. In the current process, software is delivered to a specific endpoint, requiring an engineer to manually copy it to an internal software repository. Furthermore, highly specialized ISV engineers must prepare and modify the Day0 and DayX configurations to facilitate software deployment to a DEV staging instance. One significant challenge is that the software delivery process is still designed in a way that an expert must "**touch it**," representing a bottleneck in the process. This reliance on expertise hinders the efficiency of software delivery and does not align with our Go-To-Market targets due to its time-consuming nature. In embracing the concept of Software Freshness, Swisscom acknowledges that fully tested software from the ISV might not be expected. Instead, we aim to enable basic local testing, even at the level of an engineer's laptop. Our Continuous Testing/Verification tools automate the testing of each software drop. By adopting this approach, the ISV can deliver preliminary software versions to be tested in a production-like environment, expediting the overall software delivery process.
