# GitHub vs. GitLab: Advanced Differences

This document explores the key differences between GitHub and GitLab, focusing on advanced features and enterprise-level considerations. Assuming familiarity with basic Git operations and version control concepts, we'll dive into organizational structures and CI/CD capabilities.

## Organizational Structure and Enterprise Features

### GitHub Organizations

GitHub's organizational model centers around **Organizations** as the primary unit for enterprise collaboration. Organizations provide:

- Centralized billing and resource management
- Team-based access controls with granular permissions
- Integration with enterprise identity providers (SAML SSO)
- Organization-wide settings for security policies

However, GitHub lacks support for **hierarchical structures** beyond organizations. There's no concept of sub-organizations or nested teams, requiring careful naming conventions and project level settings.

### GitLab Groups

GitLab offers a more flexible hierarchical structure through **Groups**:

- Nested groups allow for multi-level organization (e.g., Poduct > Micro-Service > Component)
- Inherited permissions and settings cascade down the hierarchy
- Group-level CI/CD variables and runners

This hierarchical approach is particularly advantageous for complex organizational setups.

## CI/CD: GitLab CI vs. GitHub Actions

### GitLab CI Pipeline Architecture

GitLab CI employs a powerful but complex templating system, e.g. featuring the **include statement**, **extends keyword**, **multi-project pipeline** and **child pipelines**.

```yaml
# .gitlab-ci.yml
include:
  - project: 'my-group/my-project'
    ref: main
    file: '/templates/.gitlab-ci-template.yml'
  - template: 'Auto-DevOps.gitlab-ci.yml'
  - local: '.gitlab-ci-local.yml'

stages:
  - build
  - test
  - deploy
```

=> **Complexity**: Deep include chains, extends hierarchies, and multi-project setups can make final pipeline understanding and debugging error-prone & difficult

### GitHub Actions Workflow Architecture

GitHub Actions provides a more straightforward approach with **reusable actions**:

```yaml
# .github/workflows/main.yml
name: CI

on:
  push:
    branches: [ main ]

jobs:
  build:
    uses: ./.github/workflows/build.yml
    with:
      node-version: '18'

  test:
    needs: build
    uses: ./.github/workflows/test.yml
```

### Feature Comparison

**Key Features:**

| Aspect                  | GitLab CI                                                               | GitHub Actions                                                                                                      |
| ----------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Templating              | Includes Statement (local files, remote URLs, and **versioning**)       |                                                                                                                     |
|                         | Extends Keyword (reuse entire or **partially extend** on existing jobs) | Composite Actions (reusable actions composed of multiple steps)                                                     |
|                         | YAML anchors (Ability to resuse configuration snippets)                 | YAML anchors                                                                                                        |
|                         |                                                                         | Oranganizational workflow templates (standardized CI/CD starting points)                                            |
|                         |                                                                         | Actions Marketplace (community-contributed, vetted actions )                                                        |
| Multi-Project Pipelines | Downstream pipelines (Parent-child/Multi-project)                       | Workflow Calls/Repository Dispatch/Workflow Dispatch (triggering workflows in other repositories or "reusing" them) |

> **Note:** More complex and powerful templating in GitLab vs. more community collaboration in GitHub.

## Deployment

GitHub Actions provides deployment capabilities through Environments, which describe general deployment targets such as production, staging, or development.

Environments can be secured with deployment **protection rules**, ensuring that jobs referencing them must pass all protection rules before running or accessing environment-specific secrets. For environments requiring reviewers, jobs wait for approval with a "Waiting" status.

Custom protection rules can integrate with third-party services like Datadog for advanced gating. Environments also support **notifications through Microsoft Teams** deployment events (pending approval, approval, status changes).

Deployment status can be visualized using **status badges** in repositories.

*Reference: [GitHub Docs - Controlling deployments with environments](https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/control-deployments)*

## Security

### Artifact Attestations and Kubernetes Integration

Artifact attestations enable you to increase the supply chain security of your builds by establishing where and how your software was built. You can use GitHub Actions to generate artifact attestations that establish build provenance for artifacts such as binaries and container images.

Artifact attestations can be enforced using a Kubernetes admission controller. The trust-policies Helm chart installs a policy that verifies attestations for all images before admission into the cluster, providing runtime security for containerized deployments.

For air-gapped or secure environments, offline verification of artifacts is supported, allowing validation without external network access.

### OIDC Integration with AWS

OpenID Connect (OIDC) enables secure, token-based authentication with AWS services without storing long-lived credentials. This approach follows the principle of least privilege and reduces credential exposure risks.

### Secure Usage Practices

GitHub provides comprehensive guidance for secure workflow implementation, including best practices for secrets management, dependency & vulnerability scanning, and access controls.

*References:*

- [Enforcing artifact attestations with Kubernetes](https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/enforce-artifact-attestations-kubernetes)
- [OIDC in AWS](https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-aws)
- [Security hardening for GitHub Actions](https://docs.github.com/en/actions/reference/security/secure-use)

## Recommendations

### General recommendations

- **Utilize Organization capabilities**: Make use of Githubs organization capabilities wherever possible. Deployment environments and associated secrets, access control, workflow templates ...
- **Plan for security**: Thoroughly work through the security best practices and apply techniques from the very beginning wby templating
- **Provided extendable templating**: Support development teams by providing and attesting simple resusable actions and templates rather than offering DevOpsaaS capabilities. Make use of the community mindset, that GitHub supports.
