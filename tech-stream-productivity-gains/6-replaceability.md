# 6 - Replaceability

## 6 - 1 Definition

Replaceability is the capability of a delivered cloud‑native application to operate correctly when its non‑functional components—such as monitoring, logging, data services, messaging, or caching—are substituted with CSP‑provided platform services. It requires that applications rely on open standards, externalized configuration, and portable interfaces, ensuring that vendor‑bundled components are optional rather than mandatory. Replaceability enables CSPs to avoid duplicated operational stacks, reduce footprint, and integrate applications seamlessly into their existing cloud‑native ecosystem

## 6 - 2 External References



## 6 - 3 Pain Points

To minimize operational overhead and avoid duplicating functionality, cloud‑native applications must allow to replace vendor‑provided non‑functional components. Such as monitoring, logging, and data services, with their own standardized platform services. This ensures architectural consistency, reduces the footprint of newly onboarded applications, and enables seamless integration into the existing operational ecosystem.

## 6 - 4 Harmonized Productivity Gains Quantified

## 6 - 5 CNTF’s ask to ISV or F/OSS

| Requirement     | Description |
|-----------------|-------------|
| AREQ A6‑1.001   | Delivered applications must not require the use of vendor‑provided monitoring, logging, or database components. All such components must be replaceable by provided equivalents without modifying application code. |
| AREQ A6‑1.002   | Applications must expose standardized interfaces for observability (e.g., OpenTelemetry, Fluent/FluentBit‑compatible logs) so that provided monitoring and logging stacks can be used as drop‑in replacements. |
| AREQ A6‑1.003   | Any monitoring, logging, or tracing stack included with the application must be optional. The application must operate correctly when these components are removed and replaced with provided services. |
| AREQ A6‑1.004   | Applications must write logs to stdout/stderr in a structured format to ensure compatibility with CSP logging pipelines and avoid the need for vendor‑specific log collectors. |
| AREQ A6‑1.005   | Applications must remain compatible with standards‑compliant implementations of any data service they consume, ensuring that vendor‑bundled databases or storage components can be fully replaced by provided equivalents without impacting application functionality. |
| AREQ A6‑1.006   | Connection parameters for all external services (e.g., databases, message brokers, caches, telemetry endpoints) must be fully externalized and configurable at deployment time, enabling seamless substitution with provided services. |
| AREQ A6‑1.007   | All replaceable components must be configured through declarative artifacts (e.g., Helm values, Kubernetes manifests, GitOps‑managed configuration), allowing substitution of own services without vendor intervention. |
| AREQ A6‑1.008   | ISV must provide clear documentation describing how to disable or remove bundled components and how to integrate provided alternatives, including supported protocols, configuration variables, and expected data formats. |
| AREQ A6‑1.009   | Applications must be validated to run with at least one alternative implementation of each replaceable component (e.g., alternative OTEL collector, alternative data service, alternative message broker) to demonstrate practical replaceability. |
| AREQ A6‑1.010   | No vendor‑provided operational component may be required for application correctness. Only core business logic components may be mandatory, all operational services must be replaceable by managed equivalents. |

## 6 - 6 CNTF’s ask to CSP readiness

## 6 - 7 Testimonies

Hans Rudolf Steiger, Swisscom: 

> Swisscom achieves clear business benefits from replacing vendor‑bundled monitoring and logging components with our standardized observability platform. This capability strengthens our compliance posture by ensuring that service health can be measured through SLIs generated with our approved tooling, fully aligned with BCM expectations. At the same time, integrating logs and telemetry into our central security and regulatory systems ensures consistent adherence to Swisscom’s security controls and country‑specific requirements. Replaceability therefore reduces operational risk, improves governance, and enables a uniform compliance baseline across all onboarded applications.

