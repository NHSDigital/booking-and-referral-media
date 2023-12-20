---
topic: core-NFR
---

## {{page-title}}

The following non functional requirements apply to all APIs designed to receive requests from BaRS. This includes sender systems receiving asynchronous responses and feedback, as well as receiving systems. All items listed below will be adhered to.

| Name                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Conformance                  | The solution conforms with the BaRS standards where applicable, within any Application                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Safety                       | The solution complies with NHS Digital [Clinical Risk Management Standards](https://digital.nhs.uk/services/clinical-safety/clinical-risk-management-standards), in particular 0129 (IT Supplier) and 0160 (Trust/Provider)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Security                     | The solution resists unauthorised, accidental or unintended usage and provides access only to legitimate requests                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Scalable and capacity        | The solution is designed to accommodate increased volumes, workloads and users                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Availability and reliability | The solution meets a service level agreement that includes a 99.9% uptime guarantee and a high Mean Time Between Failures (MTBF) The solution has adequate disaster recovery and fault tolerance enabling continued operation in the event of a failure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Auditability                 | All of the solutions interactions are fully auditable for both sending and receiving                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Data retention               | The Solution audits all API access attempts and actions, retaining all pertinent data therein                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Deployment                   | Solution providers release a new major version of their Booking and Referral APIs alongside a previous major version, until such time as consumers have migrated to the new major version. Alternatively, there is support for backward compatibility of requests to support consumers. Solution providers release a new minor or patch version, replacing the previous minor or patch version The Booking and Referral endpoints are independently deployable against unique Fully Qualified Domain Names (FDQN). This ensures support for limitations around sending and receiving messages between path-to-live and production environments. To increase availability, during upgrades and maintenance, the Booking and Referral APIs are load balanced across multiple servers In multi tenanted deployments, the activity of individual tenants are readily distinguishable |



The following Processing time SLAs describe the need for APIs to respond to a request within an acceptable time frame. This time frame should be measured from when a request is received and does not include the transport time.
These times are guide for average response time.

| item | Requirement.                                                                                                                                                   |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | 90% of requests SHOULD take less than 2100ms to process. (Allowing for response time depending on measurement point). $process-message independently measured. |
| 2    | All requests MUST take less than 5000ms to process.                                                                                                            |
| 3    | Any requests not processed within 5000ms should be timed out with "408 - REC_TIMEOUT - timeout"                                                                |





<hr>