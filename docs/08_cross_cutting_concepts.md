# Cross-Cutting Concepts

## Branching Model (Trunk-based / short-lived)

- main (always releasable; protected).
- Feature branches feature/<short-desc> or hotfix/<id>.
- PRs created for merging to main.
- Release flow: tagging on main as vX.Y.Z (SemVer).
- Optional: release/* branches if release coordination needed, but keep short-lived.

**Branch protection rules**

- Require passing CI.
- Require SonarQube quality gate.
- Require code review (1-2 approvers).
- Enforce signed commits if desired.

## Versioning (SemVer + metadata) TODO

- Use Semantic Versioning: MAJOR.MINOR.PATCH.
- CI automates version bump via one of:
  - Conventional Commits → auto versioning (semantic-release).
  - Manual bump via release PR that triggers tag vX.Y.Z.
- Artifact tagging:
  - myapp:${commit_sha} (immutable for tracing).
  - myapp:vX.Y.Z (release tag referencing digest).
  - myapp:latest optional (not used for prod deployments).
- Store version metadata in Artifactory and in Git tags.

## Testing Strategy & Pipeline Stages

- Unit Tests — fastest; executed on every push / PR. Goal < 1-3 min via parallelization.
- Integration Tests — run against ephemeral namespace with mocked/real dependencies, slower; run on PR merge, or PR if budget allows.
- Contract Tests — between services (Pact or similar) executed in CI.
- E2E Tests — run in staging environment, triggered on merge or scheduled nightly. Use stable staging environment with representative data.
- Performance/Load Tests — scheduled or pre-release.
- Security Scans — SAST (SonarQube), dependency checks, container scan (Trivy), optionally DAST in staging.

**Test parallelization**

- Split tests into workers in GitHub Actions matrix.
- Use test selection by changed files for faster feedback.

**Ephemeral Test Environments**

- For each PR:
  - Create pr-<id> k8s namespace.
  - Deploy the commit-built image.
  - Run integration & smoke tests.
  - Delete namespace on close/merge.

## Quality Gates with SonarQube

- Execute SonarQube scanner on PR and main.
- Block merges if quality gate fails (critical issues, coverage below threshold).
- Keep SonarQube credentials secret (access tokens stored in GitHub Secrets or retrieved from secret manager).

## Artifactory usage

- Docker registry for images: artifactory.example.com/docker-local/<repo>/myapp.
- Use promotion model: build once, promote artifact between repos/environments (dev → stage → prod) to guarantee binary equivalence.

## Security & Secrets

- Store secrets in AWS Secrets Manager / SSM Parameter Store or Vault.
- GitHub Actions uses short-lived OIDC to assume role; do not store long-lived AWS keys.
- Kubernetes secrets via sealed-secrets or external secrets operator backed by Secrets Manager.
- Image scanning in CI; block on critical CVEs.

## Arc42 Note (to be removed in final version)

**Content**

The deployment view describes:

1. technical infrastructure used to execute your system, with
   infrastructure elements like geographical locations, environments,
   computers, processors, channels and net topologies as well as other
   infrastructure elements and

2. mapping of (software) building blocks to that infrastructure
   elements.

Often systems are executed in different environments, e.g. development
environment, test environment, production environment. In such cases you
should document all relevant environments.

Especially document a deployment view if your software is executed as
distributed system with more than one computer, processor, server or
container or when you design and construct your own hardware processors
and chips.

From a software perspective it is sufficient to capture only those
elements of an infrastructure that are needed to show a deployment of
your building blocks. Hardware architects can go beyond that and
describe an infrastructure to any level of detail they need to capture.

**Motivation**

Software does not run without hardware. This underlying infrastructure
can and will influence a system and/or some cross-cutting concepts.
Therefore, there is a need to know the infrastructure.

Maybe a highest level deployment diagram is already contained in section
3.2. as technical context with your own infrastructure as ONE black box.
In this section one can zoom into this black box using additional
deployment diagrams:

- UML offers deployment diagrams to express that view. Use it,
  probably with nested diagrams, when your infrastructure is more
  complex.

- When your (hardware) stakeholders prefer other kinds of diagrams
  rather than a deployment diagram, let them use any kind that is able
  to show nodes and channels of the infrastructure.

See [Deployment View](https://docs.arc42.org/section-7/) in the arc42
documentation.

## Infrastructure Level 1

Describe (usually in a combination of diagrams, tables, and text):

- distribution of a system to multiple locations, environments,
  computers, processors, .., as well as physical connections between
  them

- important justifications or motivations for this deployment
  structure

- quality and/or performance features of this infrastructure

- mapping of software artifacts to elements of this infrastructure

For multiple environments or alternative deployments please copy and
adapt this section of arc42 for all relevant environments.

**_&lt;Overview Diagram>_**

Motivation
_&lt;explanation in text form>_

Quality and/or Performance Features
_&lt;explanation in text form>_

Mapping of Building Blocks to Infrastructure
_&lt;description of the mapping>_

## Infrastructure Level 2

Here you can include the internal structure of (some) infrastructure
elements from level 1.

Please copy the structure from level 1 for each selected element.

### _&lt;Infrastructure Element 1>_

_&lt;diagram + explanation>_

### _&lt;Infrastructure Element 2>_

_&lt;diagram + explanation>_

…

### _&lt;Infrastructure Element n>_

_&lt;diagram + explanation>_
