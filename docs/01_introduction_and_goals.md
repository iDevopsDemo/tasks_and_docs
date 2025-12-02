# Introduction and Goals

This document describes the DevOps architecture of **mysite360** project and outlines the strategic decisions, architectural approaches, and technological choices made during the transformation of the **mysite360** software platform into a "Next Generation" architecture.

The main goal of this document is to provide a comprehensive overview of the DevOps architecture, meaning  the development, setup, deployment, and Continuous Integration/Continuous Deployment (CI/CD) aspects of this transition. It aims to align the development and operations teams towards a common vision and set of objectives.

The main objectives of this document are:

- To define the key components of the DevOps architecture, including tools, technologies, and processes.
- To outline the roles and responsibilities of team members involved in the DevOps practices.
- To establish best practices for continuous integration, continuous delivery, and infrastructure as code.
- To provide guidelines for monitoring, logging, and incident management.

## Requirements Overview

### Pain Points vs Remediation Objectives

The DevOps approach is governed by the currenty pain points within the development and operations of **mysite360** and some centrally defined remediation strategies.

|                                             | Business-oriented microservices | Container orchestration | Shift-left testing approach | API governance through API contracts | Data-driven architecture (Data collectors, mesh & subscription, coordinated data models) | DevSecOps          | Release mgmt.      |
|---------------------------------------------|---------------------------------|-------------------------|-----------------------------|--------------------------------------|----------------------------------------------------------|--------------------|--------------------|
| High maintenance costs                      |        :white_check_mark:       |                         |      :white_check_mark:     |                                      |                                                          |                    |                    |
| High defect rate                            |        :white_check_mark:       |                         |      :white_check_mark:     |          :white_check_mark:          |                                                          |                    |                    |
| Low development velocity                    |        :white_check_mark:       |                         |      :white_check_mark:     |                                      |                                                          | :white_check_mark: |                    |
| Deployment challenges                       |        :white_check_mark:       |    :white_check_mark:   |                             |                                      |                                                          | :white_check_mark: | :white_check_mark: |
| Lack of downwards scalability (sites scale) |        :white_check_mark:       |                         |                             |                                      |                                                          |                    |                    |
| End-of-life of components                   |                                 |                         |                             |                                      |                                                          |                    |                    |
| Lack of standardization                     |                                 |                         |                             |          :white_check_mark:          |                    :white_check_mark:                    |                    |                    |
| Missing licensing and toggling capabilities |                                 |                         |                             |                                      |                                                          |                    |                    |
| Problematic ownership between teams         |        :white_check_mark:       |                         |                             |          :white_check_mark:          |                            :x:                           |                    | :white_check_mark: |
| Lack of data centric architecture           |                                 |                         |                             |                                      |                    :white_check_mark:                    |                    |                    |


**Business-oriented microservices**

Decomposing the monolithic application into smaller, independently deployable services aligned with business capabilities. Each microservice owns its own data and business logic, enabling teams to develop, deploy, and scale services independently. This reduces coupling between components, improves maintainability, and allows teams to take clear ownership of specific business domains.

**Container orchestration**

Using platforms like Kubernetes to automate the deployment, scaling, and management of containerized applications. Container orchestration handles service discovery, load balancing, self-healing, and resource allocation, making deployments more reliable and consistent across different environments while reducing manual intervention.

**Shift-left testing approach**

Moving testing activities earlier in the software development lifecycle, closer to the development phase. This includes implementing automated unit tests, integration tests, and quality checks that run during development and in CI/CD pipelines, rather than relying on manual testing at the end. Early detection of defects reduces costs and accelerates feedback cycles.

**API governance through API contracts**

Establishing formal API specifications (e.g., OpenAPI/Swagger) that define the interface contracts between services before implementation. This ensures consistent API design, enables parallel development of dependent services, facilitates automated validation and testing, and reduces integration issues by enforcing clear communication boundaries between teams and components.

**Data-driven architecture (Data collectors, mesh & subscription, coordinated data models)**

Implementing a standardized approach to data management where data collectors gather information from various sources, a data mesh architecture enables decentralized data ownership with federated governance, subscription mechanisms provide event-driven data distribution, and coordinated data models ensure consistency across services. This creates a coherent data strategy that improves data quality, accessibility, and interoperability.

**DevSecOps**

Integrating security practices throughout the entire DevOps lifecycle, from development to deployment and operations. This includes automated security scanning, vulnerability assessments, compliance checks, and security testing in CI/CD pipelines, ensuring that security is built into the application rather than being an afterthought. DevSecOps enables faster releases while maintaining or improving security posture.

**Release mgmt.**

Establishing structured processes and automation for planning, scheduling, and controlling software releases across environments. This includes versioning strategies, deployment orchestration, rollback capabilities, feature flagging, and coordination between teams to ensure predictable, low-risk releases that can be executed reliably and frequently.

**Not understood**

- Reduced server stack complexity by using immutable and harden hyperconverged platform
- Increase usage of commercial ready SW and focus on value-adding development activities
- Establish key software partnerships including with hyperscalers
- Disconnect architecture from HW and operating systems
- Open model and flexible architecture
- End-to-end testing of full solution
- Pre-validation of third-party components

More details on the drives behind a new DevOps architecture can be read in the [MySite Next Gen Technology options](./advanda/MySite%20Next%20Gen_Technology%20options.pdf)

### DevOps Architecture Goals

The overarching devops architecture vision for **mysite360** 2.0, derived from the forces outlined above, focuses on the following key aspects:

- **Containerization and Orchestration**: Leveraging containerization technologies like Docker and orchestration tools like Kubernetes to ensure scalability, flexibility, and efficient resource utilization.
- **Test Automation**: Implementing automated testing frameworks to ensure code quality, reduce manual effort, and accelerate the development lifecycle.
- **Continuous Integration and Continuous Deployment (CI/CD)**: Implementing robust CI/CD pipelines to automate the build, test, and deployment processes, enabling faster and more reliable software delivery.
- **Infrastructure as Code (IaC)**: Adopting IaC practices using tools like Terraform and Ansible to manage infrastructure in a version-controlled and automated manner.
- **Monitoring and Logging**: Establishing comprehensive monitoring and logging solutions to ensure system reliability, performance, and proactive issue resolution.

## Quality Goals

## Stakeholders