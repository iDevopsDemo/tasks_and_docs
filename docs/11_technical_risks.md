# Risks and Technical Debts

- **Risk**: Long CI runtime slows developer feedback.
  **Mitigation**: aggressive test splitting, test selection, caching, and running heavy tests only on merge.

- **Risk**: Secrets leakage.
  **Mitigation**: OIDC + IAM + Secrets Manager and RBAC.

- **Risk**: Different behavior across environments.
  **Mitigation**: Infrastructure parity; use same Helm charts/values with environment overrides; use infra as code.

- **Risk**: Artifactory single point-of-failure.
  **Mitigation**: High availability for Artifactory, or mirror critical artifacts to S3/ECR.

## Arc42 Note (to be removed in final version)

**Contents**

A list of identified technical risks or technical debts, ordered by
priority

**Motivation**

“Risk management is project management for grown-ups” (Tim Lister,
Atlantic Systems Guild.)

This should be your motto for systematic detection and evaluation of
risks and technical debts in the architecture, which will be needed by
management stakeholders (e.g. project managers, product owners) as part
of the overall risk analysis and measurement planning.

**Form**

List of risks and/or technical debts, probably including suggested
measures to minimize, mitigate or avoid risks or reduce technical debts.

See [Risks and Technical Debt](https://docs.arc42.org/section-11/) in
the arc42 documentation.
