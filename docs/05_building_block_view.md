# Building Block View

Components and responsibilities:

- **GitHub Repositories**
  - app-services (code + Dockerfile + k8s/helm chart)
  - infra (Terraform for EKS, VPC, IAM)
  - platform (shared charts, k8s operators)

- **CI/CD (GitHub Actions)**
  - ci-build — run unit tests, lint, SonarQube analysis, build container, push to Artifactory (image: myapp:${version}).
  - ci-integration — deploy to ephemeral namespace, run integration tests.
  - ci-e2e — run E2E against staging cluster (or ephemeral PR environment).
  - cd-promote — on release tag, promote image to prod cluster (or create PR for deployment).
  - cd-canary — perform canary/blue-green deployments via Helm and metrics checks.

- **Artifact Repository**
  - Artifactory (Docker registry, generic package repos). Images use immutable digests and semantic tags.

- **SonarQube**
  - Quality gates: code coverage threshold, security hotspots, duplication, critical bugs fail build.

- **Kubernetes (EKS)**
  - Helm charts for deployments.
  - Namespaces: infra, shared, app-{name}, pr-<id> (ephemeral).
  - CI-created ephemeral namespaces for PRs.

- **Infrastructure**
  - Terraform modules for VPC, EKS, node groups, IAM roles, ALB, RDS (if needed).
  - S3 backend for Terraform state with locking via DynamoDB.

- **Security**
  - GitHub OIDC to assume AWS roles (short-lived).
  - IAM roles for service accounts (IRSA).
  - Image scanning during CI (Snyk/Trivy — optional).

