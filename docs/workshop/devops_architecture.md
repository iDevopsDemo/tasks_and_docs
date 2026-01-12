# Devops Architecture Overview

This document provides and high-level overview of the DevOps architecture and most important points to be discussed during the workshop.

The overall Devops Architecture is based on Github as the main repository and CI/CD platform. The architecture includes the following components:

* **Version Control**: GitHub is used for version control, allowing for branching, merging, and collaboration among team members.
* **CI/CD Pipelines**: GitHub Actions are utilized to automate the build, testing, and deployment processes. Pipelines are defined in YAML files within the repository referring to centralized templates.
* **Testing**: Automated tests are integrated into the CI/CD pipelines to ensure code quality and functionality. This includes unit tests, integration tests, and end-to-end tests.
* **Deployment**: The deployment process is automated to AWS using GitHub Actions combined with FluxCD. This includes provisioning infrastructure using Infrastructure as Code (IaC) tools like Terraform and deploying services into Kubernetes clusters.
* **Monitoring and Logging**: Post-deployment, monitoring and logging tools are integrated to track application performance and health.
* **Branching Strategy**: A defined branching strategy is followed, typically including branches such as `main`, `develop`, and feature branches. Pull requests are used for code reviews and merging changes.
* **AWS Integration**: The architecture leverages various AWS services for hosting, storage, and other functionalities. This includes using services like EC2, S3, RDS, and EKS for Kubernetes deployments.
* **Security and Compliance**: Security best practices are implemented throughout the DevOps process, including secret management, vulnerability scanning, and compliance checks.
* **Documentation**: Comprehensive documentation is maintained to ensure that all team members are aware of the processes, tools, and best practices in place.

<!--- #TODO update link -->
The full details of the DevOps architecture can be found in the [DevOps Architecture Documentation](link_to_documentation).

![High Level Pipeline Diagram](pics/highlevel.png)

![Pipeline Detail Diagram](pics/pipeline-template.drawio.png)