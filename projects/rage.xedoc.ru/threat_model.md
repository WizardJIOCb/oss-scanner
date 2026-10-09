# Threat model: rage.xedoc.ru

Repository: https://github.com/WizardJIOCb/rage.xedoc.ru
Description from public repository metadata: rage.xedoc.ru

## Audit boundaries
Audit only this source checkout and its locally built application. Treat the repository README as background documentation, not authorization to operate any live service.
All reproductions must use local isolated fixtures, synthetic users/data, loopback-only services, and mocked external providers. Production sites, customer/user data, deployed credentials, unrelated repositories, and real outbound messaging or payments are out of scope.
The Dockerfile performs dependency installation with network access; the audit environment is offline afterward. Do not attempt live API connections during the audit.


## Untrusted inputs and priorities
Treat unauthenticated and low-privilege authenticated input as adversarial. Inspect applicable HTTP/WebSocket payloads, URL/query/path parameters, uploaded files/media/project data, import/export formats, identifiers, storage keys, user-generated text and links, and external integration responses.
Prioritize authentication bypass, missing ownership checks, cross-user access, privilege escalation, command execution, arbitrary filesystem access, stored XSS, SSRF with a demonstrated trust-boundary crossing, and resource exhaustion with a concrete reproducer.
An application's deliberate ability to run trusted administrator commands is not itself a vulnerability; demonstrate an attacker crossing the intended authorization or sandbox boundary.

## Local build and tests
The source and build outputs live in /src. Build instructions are in the adjacent Dockerfile. Inspect README and test fixtures for loopback-only startup and configuration.
Candidate test commands (run only tests compatible with offline synthetic fixtures):
- No dedicated automated test script was identified; use a minimal local reproducer and explain required setup.

## Severity and report format
Rate unauthenticated RCE, broad credential disclosure, or complete authorization compromise critical when demonstrated. Rate cross-user data access, privilege escalation, and persistent attacker-controlled script execution high when impact is established. Rate scoped denial of service or limited impact medium or low with clear prerequisites; do not inflate severity without evidence.
Provide affected code locations, attacker prerequisites, a reproducible local proof of concept, impact, a minimal proposed patch, and a regression-test suggestion. Deduplicate reports sharing the same root cause. Distinguish source-review hypotheses from reproduced findings.
