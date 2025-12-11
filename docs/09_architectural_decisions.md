# Architectural Decisions

- Use Trunk-based development for rapid CI/CD.
- Use SemVer automated by CI or release tooling.
- Use GitHub Actions with OIDC to access AWS.
- Use Artifactory for immutable artifact storage.
- Use EKS per AWS account (dev/stage/prod) for isolation.
- Use ephemeral namespaces to support integration tests & PR previews.
- Use SonarQube as mandatory quality gate.

## Arc42 Note (to be removed in final version)

**Contents**

Important, expensive, large scale or risky architecture decisions
including rationales. With "decisions" we mean selecting one alternative
based on given criteria.

Please use your judgement to decide whether an architectural decision
should be documented here in this central section or whether you better
document it locally (e.g. within the white box template of one building
block).

Avoid redundancy. Refer to section 4, where you already captured the
most important decisions of your architecture.

**Motivation**

Stakeholders of your system should be able to comprehend and retrace
your decisions.

**Form**

Various options:

- ADR ([Documenting Architecture
  Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions))
  for every important decision
- List or table, ordered by importance and consequences or:
- more detailed in form of separate sections per decision

**Further Information**

See [Architecture Decisions](https://docs.arc42.org/section-9/) in the
arc42 documentation. There you will find links and examples about ADR.
