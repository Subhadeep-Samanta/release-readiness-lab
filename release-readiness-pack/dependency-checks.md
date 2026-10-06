# Dependency Checks

## Release Candidate

- Release candidate: `v2.4`
- Dependency file: `app/requirements.txt`

## Dependency Pinning

The application dependencies are explicitly pinned:

| Dependency | Required Version |
|---|---|
| Flask | `3.0.2` |
| Gunicorn | `22.0.0` |
| pytest | `8.0.2` |

**Pinning status: PASS**

The versions are fixed in `app/requirements.txt`.

## Vulnerability Scan

Command:

`pip-audit -r requirements.txt`

Result:

**FAILED — known vulnerabilities detected**

`pip-audit` reported 4 findings affecting 2 packages.

| Package | Current Version | Vulnerability | Fixed Version |
|---|---:|---|---:|
| Flask | `3.0.2` | `PYSEC-2026-2151` | `3.1.3` |
| pytest | `8.0.2` | `PYSEC-2026-1845` | `9.0.3` |

The duplicate findings reported by the scanner are retained in the evidence count.

## Risk Assessment

### Flask

Flask is a runtime application dependency. The detected vulnerability therefore represents a release-blocking dependency risk until the fixed version is evaluated and adopted.

**Severity for release readiness: HIGH**

### pytest

pytest is a development/test dependency rather than a runtime application dependency. Its vulnerability should still be remediated, but it presents a lower production-runtime risk than the Flask finding.

**Severity for release readiness: MEDIUM**

## Required Remediation

1. Evaluate and upgrade Flask from `3.0.2` to the fixed version `3.1.3` or a later supported secure version.
2. Evaluate and upgrade pytest from `8.0.2` to `9.0.3` or a later supported secure version.
3. Run the complete test suite after dependency changes.
4. Re-run `pip-audit -r requirements.txt`.
5. Record the new scan result before production approval.

## Dependency Readiness

**Status: NOT READY**

The current release candidate has known dependency vulnerabilities and requires remediation before production release.
