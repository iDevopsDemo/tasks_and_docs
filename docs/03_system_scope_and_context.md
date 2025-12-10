# System Scope and Context

Actors & external systems:

- Developers (push PRs to GitHub).
- GitHub (repo, Actions, OIDC).
- SonarQube (static analysis server).
- Artifactory (docker registry / maven / npm repo). <!--- #TODO which packages? -->
- AWS (Accounts: dev / staging / prod). <!--- #TODO multi or single account? -->
- EKS clusters (one per environment). <!--- #TODO multi or single cluster? -->
- Terraform state backend (S3 + DynamoDB). <!--- #TODO terraform required? Where to store state? -->
- Monitoring stack (Prometheus/Grafana, optionally AWS CloudWatch).
- Secrets manager (AWS Secrets Manager or HashiCorp Vault).

## High-Level System Context Diagram

```text
Developer -> GitHub repo (code + CI) -> GitHub Actions CI -> SonarQube
                                           -> Build Docker -> Artifactory
                                           -> Deploy to EKS (dev/stage/prod)
AWS Accounts: dev, stage, prod
EKS per account -> Kubernetes namespaces per app / ephemeral namespace for PRs
```

TODO: Add drawio diagram here.

## Arc42 Note (to be removed in final version)

**Contents**

System scope and context - as the name suggests - delimits your system
(i.e. your scope) from all its communication partners (neighboring
systems and users, i.e. the context of your system). It thereby
specifies the external interfaces.

If necessary, differentiate the business context (domain specific inputs
and outputs) from the technical context (channels, protocols, hardware).

**Motivation**

The domain interfaces and technical interfaces to communication partners
are among your system’s most critical aspects. Make sure that you
completely understand them.

**Form**

Various options:

- Context diagrams

- Lists of communication partners and their interfaces.

See [Context and Scope](https://docs.arc42.org/section-3/) in the arc42
documentation.

## Business Context

**Contents**

Specification of **all** communication partners (users, IT-systems, …)
with explanations of domain specific inputs and outputs or interfaces.
Optionally you can add domain specific formats or communication
protocols.

**Motivation**

All stakeholders should understand which data are exchanged with the
environment of the system.

**Form**

All kinds of diagrams that show the system as a black box and specify
the domain interfaces to communication partners.

Alternatively (or additionally) you can use a table. The title of the
table is the name of your system, the three columns contain the name of
the communication partner, the inputs, and the outputs.

**&lt;Diagram or Table>**

**&lt;optionally: Explanation of external domain interfaces>**

## Technical Context

**Contents**

Technical interfaces (channels and transmission media) linking your
system to its environment. In addition a mapping of domain specific
input/output to the channels, i.e. an explanation which I/O uses which
channel.

**Motivation**

Many stakeholders make architectural decision based on the technical
interfaces between the system and its context. Especially infrastructure
or hardware designers decide these technical interfaces.

**Form**

E.g. UML deployment diagram describing channels to neighboring systems,
together with a mapping table showing the relationships between channels
and input/output.

**&lt;Diagram or Table>**

**&lt;optionally: Explanation of technical interfaces>**

**&lt;Mapping Input/Output to Channels>**
