# CNTF Tech Stream Productivity Gains

## Responsible Officer / Initiator

Lukas Leuthold, Swisscom

## Contributors

### Deutsche Telekom

Daniel Dierich, Kai Steuernagel, Mohamed Annis Souames

### Telefònica

Matthias Sauders, Bas Hendrikx

### Swisscom

Lukas Leuthold, Adrian Kurt, Josua Hiller, Joel Studler, Ashan Senevirathne

### Ericsson

Peter Wörndle, Jonas Falkena, Staffan Bonnier, Anders Fagerlind , Jawwad Rasheed

## CNTF participating Operators

Deutsche Telekom, Vodafone DE, KPN, TNO, Telenor, Vodafone IT/Fastweb, Orange FR, Container Solutions GB

## CNTF participating vendors

Ericsson, Nokia

## Content

- [General Information](0-productivity-gains.md)
- [1 - Software Freshness](1-software-freshness.md)
- [2 - Declarative Management](2-declarative-management.md)
- [3 - Observability](3-observability.md)
- [4 - Scalability](4-scalability.md)
- [5 - High Availability](5-high-availability.md)

## General Information

### Purpose

This document provides a comprehensive exploration of the significant productivity gains resulting from the adoption of cloud-native principles. It specifically highlights the relevance of these gains in the context of 2025. By synthesizing the individual experiences of CNTF associates, a unified narrative is presented, offering a holistic view of the transformative potential.

In embracing cloud-native principles, it is crucial to recognize that this journey extends beyond mere technical considerations into ways of working and processes. While technical aspects are vital, the adoption of cloud-native principles by technology suppliers and CSPs should also be driven by the objective of generating tangible business value. This broader perspective encourages organizations to explore the full spectrum of potential benefits associated with cloud-native transformations.

The productivity gains outlined in this document represent a network of interconnected benefits, reinforcing and complementing one another. Each gain has the potential to facilitate the achievement of other gains, further amplifying the positive impact. By strategically leveraging cloud-native principles, organizations can anticipate substantial productivity improvements in 2025, ensuring they stay at the forefront of innovation and efficiency in a rapidly evolving digital landscape.

CNTF drives solutions and alignment that scales for both vendors and operators. Creating a healthy industry with room for differentiation where it makes sense, while aligning for reduced cost in other areas. Also includes high level alignment of industry pacing/timing where needed.

### Scope

The content applies to the CNTF initiative, started in November 2024 by Swisscom. Being a forum, we aligned the content among all CSP and ISV listed on the title page. The findings shall serve as a guideline and be actively discussed with our ISV, CSPs and Cloud Providers. While the guidelines are applicable for both network functions/platform and software engineering in general, examples and pain-points are coming from network side.

### Goal

The primary goal of this document is to express the common pain-points encountered by the CNTF associates and share and align the expected user experience within the cloud-native context. We realise that CSPs need to amplify direction/goals for WoW and process alignment. The underlying vision of this document remains solution- and product-agnostic, aiming to harmonize a unified experience across different operators. By presenting these pain-points, we intend to provide a focused and condensed articulation of the areas where software suppliers (both vendors and F/OSS) should allocate resources and make improvements. At the same time, we present essential characteristics of cloud-native operations (ways-of-working and processes), applicable to CSPs wanting to make most use out of cloud-native technologies.

The topic of cloud nativeness and its design patterns has a high potential of becoming a trite cliché if not related to its potential to gain the operational productivity significantly. There is also a risk that an uncoordinated introduction of cloud native principles may lead to a high level of industry fragmentation. To counter this perception and these risks, we firmly assert that embracing cloud-native principles has the potential to stimulate significant productivity growth. As such, our objective is to go beyond general statements and explicitly specify the gains in productivity that can be achieved, quantify them where possible, highlight existing challenges, and indicate areas of alignment within the CNTF perspective.

Given the extensive range of aspects and disciplines within cloud-native principles, attempting to cover them all in a single document would exceed its intended purpose. Therefore, for the first edition of this document, we have chosen to focus on three key areas that we consider of utmost importance. By prioritizing these areas, we aim to foster continued dialogue, both within the CNTF community and with vendors, to further enhance our understanding and collaboration in advancing cloud-native practices.

### Document History

| SemVer | Date      | Description                                                  |
| ------ | --------- | ------------------------------------------------------------ |
| 1.0.0  | CW11/2025 | Initial release                                              |
| 2.0.0  | CW15/2025 | Chapters / Area restructured. Always-on-latest-SW Paradigm, “No-touch”/Continuous Flow SW and Feedback Loop, Testing in Production, CNTF proposed foundation services for GitOps, Multi-App-On-Single Cluster, DORA Metrics for CD. |
| 2.1.0  | CW44/2025 | New Areas: Observability - Area 3, Scalability - Area 4, High Availability Area 5 |
| 2.1.0+ |           | Version control tracked in git                               |

### Glossary

| Term  | Description                                            |
| ----- | ------------------------------------------------------ |
| ISV   | Industry Software Vendor, also NF vendors, Supplier    |
| CSP   | Communication Service Provider, also Telcos, Operators |
| F/OSS | Free- and Open Source Software                         |
| CNTF  | Cloud Native Telco Forum                               |
| CNCF  | Cloud Native Computing Foundation                      |

### Definition of Terms

| Term                                      | Description                                                  |
| ----------------------------------------- | ------------------------------------------------------------ |
| Software/Realization lifecycle management | The process of changing software artifacts or software related configuration e.g. security update or Pod replica count. |
| Functional lifecycle management           | The process of changing the functionality a network function provides in the network e.g. creating a new APN/DNN or enabling a new 3GPP interface. |
