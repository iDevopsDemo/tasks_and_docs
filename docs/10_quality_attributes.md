# Quality Attributes

1. **Fast feedback on code changes**
   - Unit tests and Sonar run < 5 minutes. Achieved via parallelization and caching.

2. **PR preview environment**
   - Ephemeral namespace exists within ~3–5 min; integration tests executed automatically.

3. **Reproducible releases**
   - Same image digest that passed staging is promoted to prod; ability to rollback to prior digest.

4. **Zero downtime deploy**
   - Canary/blue-green via Helm and controlled traffic shift using ALB or service mesh.

## Quality Tree

| Top Level | Quality | Priority | Scenario name | Scenario description | Associated test scenario |
| :-------- | :------ | :------- | :------------ | :------------------- | ------------------------ |

## Quality Scenarios

| ID    | Scenario                                                            | Stimulus                                                                                                                                          | Environment and conditions                                                                                                                             | System artefact                          | Response                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :---- | :------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### References
