# 4 - Scalability

## 4 - 1 Definition

Scalability refers to the dynamic expanding and contracting of resources as the workload fluctuates without a loss of performance or stability. It is crucial to allow the accommodation of vastly differing loads without statically overprovisioning the application. In the context of cloud nativeness this can be achieved through techniques such as auto-scaling, container orchestration, and microservices architecture. Microservice architecture breaks applications down into smaller independent units which allow different parts of the application to be scaled individually. A container orchestration platform allows the dynamic and automated management of the deployed application by performing the necessary operations, potentially across different hosts.

## 4 - 2 External References

## 4 - 3 Pain Points

A lack of scalability often leads to significant issues when applications face highly variable traffic. Applications may struggle to handle high traffic peaks or become severely overprovisioned during low-demand periods, resulting in performance degradation or unnecessary costs.

One major factor contributing to scalability challenges is the monolithic software architecture, which frequently causes operational issues due to its inflexibility. The slow start-up time of monolithic applications hampers the horizontal scaling process, as adding additional instances becomes time-consuming. This limitation often forces applications to resort to vertical scaling, where the computing power of a single machine is increased. Vertical scaling requires downtime, is limited by the physical properties of the server, and introduces a single point of failure.

Another issue with horizontal scaling is state management. Applications needing previous sessions or data for future transactions struggle to reroute requests to different instances of the same application. This difficulty complicates the consideration of necessary prerequisites for current requests.

The same constraints apply to downscaling; it may require downtime and is restricted by the server's physical properties. These limitations make rightsizing challenging, as the required computational capabilities must be estimated upfront and cannot be quickly adjusted, often only with downtime.

Another problem with rightsizing is that only the entire application can be upscaled. This means if only a specific part of the application is overloaded, it is still necessary to scale up even the parts that are not overloaded. These inefficiencies in rightsizing lead to cost disadvantages, as the application is likely sized larger than necessary for extended periods.

## 4 - 4 Harmonized Productivity Gains Quantified

## 4 - 5 CNTF’s ask to ISV or F/OSS

| Requirement | Description |
| ------------- | ------------------------------------------------------------ |
| AREQ A4-1.001 | Generally, applications and their micro-services must be either stateless or externalize their state. |
| AREQ A4-1.002 | The application must be delivered in a micro-service architecture according to CNCF and 12factor app specification |
| AREQ A4-1.003 | The micro-services must start-up and shutdown gracefully. |
| AREQ A4-1.004 | The application and its micro-services must support a dynamic service discovery and load balancing mechanisms |
| AREQ A4-1.005 | The application must be deployed in Kubernetes and support its dynamic orchestration |
| AREQ A4-1.006 | The application and its micro-services must as much as possible hardware independent. |
| AREQ A4-1.007 | The application's micro-services must respond to autoscaling policies tailored to the specific service |

## 4 - 6 CNTF’s ask to CSP readiness

## 4 - 7 Testimonies
