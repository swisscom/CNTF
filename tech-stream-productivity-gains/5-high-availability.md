# 5 - High Availability

## 5 - 1 Definition

Availability in the context of cloud nativeness typically refers to fault tolerance, resiliency and self-healing. These attributes may allow an application to stay operational even when facing errors or failures. By dynamically and swiftly addressing these issues without causing downtime, applications can maintain high availability. This is often achieved through the implementation of microservice architectures, redundancies, failover mechanisms, monitoring, and container orchestration.

A microservice architecture can facilitate resilience by allowing individual components of an application to fail without necessarily affecting others. Additionally, reduced start-up times of microservices would keep downtimes short, should they occur.

Redundancy and failover mechanisms are a key component to maintain availability during the restart of components. They allow to reroute traffic to a different instance of the same component while the failing one restarts. This can be done on application, microservice or infrastructure level.

Self-healing mechanisms allow a container to handle failures without manual intervention by utilizing health checks and other observability features to identify issues and trigger the according action.

## 5 - 2 External References

## 5 - 3 Pain Points

The current traditional approaches create some problems when aiming to achieve high availability.

Monolithic architectures for example inherently have a single point of failure. When a problem occurs in any part of the application, it will most likely cause the entire system to fail. Due to its size the restart of this application will be time consuming.

Implementing an effective failover mechanism may also be problematic. Since component isolation is most likely not supported in a general way, a failure will lead to a loss of all data related to the current transaction. This will impact the application’s ability to reroute traffic to an unaffected instance of the same application.

Additionally, many applications nowadays manage state. This means that a potential failure not only risks the current transaction’s data, but also the data of all previous transactions. This will impact the applications ability to return to normal operations and severely complicates the recovery mechanisms.

## 5 - 4 Harmonized Productivity Gains Quantified

## 5 - 5 CNTF’s ask to ISV or F/OSS

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A5-1.001 | Generally, applications and their micro-services must be either stateless or externalize their state. |
| AREQ A5-1.002 | If the applications are using databases, these must support backup recovery and be deployed distributed and fully redundant |
| AREQ A5-1.003 | The application and their micro-services must be self-healing |
| AREQ A5-1.004 | The application and its micro-services must support a dynamic service discovery and load balancing mechanisms |
| AREQ A5-1.005 | The application must be deployed in Kubernetes and support its dynamic orchestration |
| AREQ A5-1.006 | The application and its micro-services must as much as possible hardware independent. |

## 5 - 6 CNTF’s ask to CSP readiness

## 5 - 7 Testimonies
