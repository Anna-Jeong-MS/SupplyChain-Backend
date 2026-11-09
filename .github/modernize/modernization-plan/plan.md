# Modernization Plan: SupplyChain Backend Modernization

**Project**: SupplyChain Backend

---

## Technical Framework

- **Language**: Java 8
- **Framework**: Spring Boot 2.7.18
- **Build Tool**: Maven
- **Database**: MySQL 8.0.33
- **Key Dependencies**: Spring Data JPA, Spring AMQP, RabbitMQ,
  Hibernate, Lombok

---

## Overview

> This modernization prepares the SupplyChain Backend API for the documented
> enterprise and Azure targets. The application currently uses an end-of-life
> Java runtime, legacy framework and platform libraries, local credentials,
> MySQL, and RabbitMQ. The modernized application will:
>
> - Move to the documented Java 17 and Spring Boot 3.2 runtime.
> - Align external service calls, logging, business validation, and messaging
>   with the platform APIs documented for this project.
> - Replace MySQL and local credentials with Azure SQL Database and Azure Key
>   Vault, and define the requested Azure resources as Bicep.
> - Update the existing container image for the Java 17 runtime.
>
> The work is phased: establish the existing behavior, modernize the runtime
> and application integrations, verify the result, then update the container
> and complete dependency security remediation. Infrastructure code is
> generated without provisioning resources.

---

## Migration Impact Summary

| App | Original | Azure target | Auth | Notes |
|-----|----------|--------------|------|-------|
| API | MySQL | Azure SQL DB | Managed identity | Roadmap target |
| API | RabbitMQ | Azure Service Bus | MI | Custom API |
| API | Local credentials | Azure Key Vault | MI | Remove plaintext |
| API | Java 8 / Boot 2.7 | Java 17 / Boot 3.2 | N/A | Documented target |
| API | Docker Java 8 image | Java 17 distroless | N/A | Update Dockerfile |

---

## Open Questions & Questionnaire

- [ ] Q: Should the framework target move to Spring Boot 4.x? The repository
  roadmap specifies Spring Boot 3.2; this plan retains that requested target.
- [x] Q: Should the plan include environment provisioning? → A: No resource
  provisioning; generate the Bicep requested in the roadmap.
- [x] Q: Should the plan include integration testing? → A: Yes, use mock mode
  because no Azure test environment is specified.
- [x] Q: Should the plan include security/CVE remediation? → A: Yes.
- [x] Q: Which deployment target should be used? → A: No deployment task;
  deployment was not requested.
- [x] Q: Should containerization be included? → A: Update the existing
  Dockerfile as specified in the roadmap.
