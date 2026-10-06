# Rollback Plan

## Release

- Release candidate: `v2.4`
- Known-good version: `v2.3`
- Target namespace: `checkout-system`
- Deployment: `checkout-api`

## Rollback Trigger

Rollback should be initiated if v2.4 causes:

- Application health degradation
- Database or Redis connectivity failures
- Significant checkout failures
- Pod readiness or liveness failures
- Unexpected production errors
- Release-blocking regressions

## Known-Good Version

The repository documentation identifies `v2.3` as **Prod - STABLE** and `v2.4` as the release candidate.

Therefore, `v2.3` is the documented rollback target.

## Rollback Procedure

Check the deployment:

    kubectl get deployment checkout-api -n checkout-system
    kubectl get pods -n checkout-system

Set the deployment back to v2.3:

    kubectl set image deployment/checkout-api checkout-api=kalvium/checkout-api:v2.3 -n checkout-system

Wait for the rollback:

    kubectl rollout status deployment/checkout-api -n checkout-system

Verify the pods:

    kubectl get pods -n checkout-system

Verify application health and PostgreSQL/Redis connectivity through the normal service access path.

## Rollback Verification

The rollback procedure was **NOT EXECUTED LOCALLY** because `kubectl` is not installed on the validation machine.

The rollback target is based on the documented production history.

## Rollback Limitation

The repository has no Git tags.

The command:

    git tag -l

returned no tags.

Therefore, `v2.3` is documented as the known-good release, but there is no formal Git tag identifying that release.

## Rollback Readiness

**Status: PARTIAL**

The rollback target and procedure are documented, but the procedure has not been executed locally and v2.3 has no Git release tag.
