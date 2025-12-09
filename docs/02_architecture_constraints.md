# Architecture Constraints

This document lists the architecture constraints for the project. These
constraints must be followed by all architects and developers working on
the project.

- Cloud provider: AWS (must use EKS).
- CI platform: GitHub Actions (CI & CD).
- Artifact repo: JFrog Artifactory for container images and artifacts.
- Static code quality: SonarQube (integrated in CI).
- Container orchestration: Kubernetes (EKS).
- IaC: Terraform for AWS infra, Helm for app deployment.
- Branching model: Trunk-based with short-lived feature branches (see section Branching).
- Versioning: Semantic Versioning (SemVer) with automated tagging.

## Arc42 Note (to be removed in final version)

**Contents**

Any requirement that constraints software architects in their freedom of
design and implementation decisions or decision about the development
process. These constraints sometimes go beyond individual systems and
are valid for whole organizations and companies.

**Motivation**

Architects should know exactly where they are free in their design
decisions and where they must adhere to constraints. Constraints must
always be dealt with; they may be negotiable, though.

**Form**

Simple tables of constraints with explanations. If needed you can
subdivide them into technical constraints, organizational and political
constraints and conventions (e.g. programming or versioning guidelines,
documentation or naming conventions)

See [Architecture Constraints](https://docs.arc42.org/section-2/) in the
arc42 documentation.
