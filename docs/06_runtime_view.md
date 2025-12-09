# Runtime View

## Developer creates a PR (fast feedback)

1. Dev opens PR on feature branch in GitHub.
2. GitHub Actions CI triggers:
    - Run unit tests (parallel).
    - Lint + format check.
    - SonarQube analysis (PR scan).
    - Build Docker image tagged with pr-<pr-number>-<sha> and push to Artifactory (optional for PR workflow).
    - Create ephemeral k8s namespace pr-<id> in dev EKS, deploy helm chart referencing the PR image (image: digest).
    - Run integration tests using the deployed environment (tests run as job pods).
    - Run lightweight E2E smoke tests (optional).

3. Post-status updates on PR; SonarQube/coverage or failing tests mark PR as failed.
4. On PR close/merge, ephemeral namespace is deleted.

## Merge to main — release pipeline

1. Merge triggers ci-release:
    - Run full test suite (unit + integration + E2E).
    - Build release image: tag vX.Y.Z (SemVer) and latest-digest.
    - Push image to Artifactory.
    - Create a GitHub release (automated changelog).
    - Deploy to staging cluster with canary.
    - Run full E2E test suite against staging.
    - If successful, promote same image digest to production with controlled rollout (canary/blue-green + automated health checks).
    - Update version metadata in Artifactory.

## Rollback scenario

- Since deployments are by image digest and Helm releases, rollback is: helm rollback <release> <revision> or redeploy previous image digest.
- Automate rollback on metrics breach (via GitHub Action/Argo Rollouts or custom operator).

## Arc42 Note (to be removed in final version)

**Contents**

The runtime view describes concrete behavior and interactions of the
system’s building blocks in form of scenarios from the following areas:

- important use cases or features: how do building blocks execute
  them?

- interactions at critical external interfaces: how do building blocks
  cooperate with users and neighboring systems?

- operation and administration: launch, start-up, stop

- error and exception scenarios

Remark: The main criterion for the choice of possible scenarios
(sequences, workflows) is their **architectural relevance**. It is
**not** important to describe a large number of scenarios. You should
rather document a representative selection.

**Motivation**

You should understand how (instances of) building blocks of your system
perform their job and communicate at runtime. You will mainly capture
scenarios in your documentation to communicate your architecture to
stakeholders that are less willing or able to read and understand the
static models (building block view, deployment view).

**Form**

There are many notations for describing scenarios, e.g.

- numbered list of steps (in natural language)

- activity diagrams or flow charts

- sequence diagrams

- BPMN or EPCs (event process chains)

- state machines

- …

See [Runtime View](https://docs.arc42.org/section-6/) in the arc42
documentation.

## Runtime Scenario Remote Connect

<https://code.siemens.com/common-device-management/remote-access/remote-access-service/-/blob/main/README.md?ref_type=heads>

This is the interaction between different components for remote connection and disconnection.

## Runtime Scenario Context Hierarchy

<https://code.siemens.com/common-device-management/inventory/context-hierarchy-service/-/blob/main/README.md>

This is the interaction between different components for creating context based hierarchy.

## &lt;Runtime Scenario 2>

## …

## &lt;Runtime Scenario n>
