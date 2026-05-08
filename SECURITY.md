
# SECURITY — Forge-Theory-Labs

## 1. Reporting Vulnerabilities
Report privately to:
security@forge-theory-labs.local

Include:
- description
- reproduction steps
- affected repos
- impact assessment

Do NOT:
- open public issues
- disclose on social media
- publish exploit details
- create public forks showing the issue

## 2. Scope
Security applies to all Wave A–E repositories:
- cognitive systems
- trading intelligence
- robotics
- infrastructure
- emergence & simulation engines

## 3. Contributor Security Expectations
- preserve deterministic behaviour
- no global mutable state
- no untyped or ambiguous interfaces
- no unnecessary dependencies
- no hidden network calls
- no uncontrolled filesystem side effects

## 4. Dependency Policy
Allowed:
- zero-dependency implementations
- standard library
- necessary cryptographic primitives

Not allowed:
- unreviewed third-party libraries
- unclear licensing
- ambiguous behaviour
- telemetry or analytics

## 5. Secrets & Credentials
Never commit:
- API keys
- tokens
- passwords
- private keys
- environment secrets

If leaked:
1. rotate immediately
2. purge from Git history
3. notify maintainers

## 6. Robotics Safety (Wave C)
- no unsafe defaults
- no unbounded motor commands
- no unverified sensor loops
- kill-switch logic required
- hardware assumptions must be validated

## 7. Trading Safety (Wave B)
- no unbounded order placement
- no silent fallback to real funds
- no ambiguous strategy behaviour
- deterministic, auditable logic only

## 8. Simulation Safety (Wave E)
- no unbounded memory growth
- no infinite loops without break conditions
- no runaway GPU/CPU behaviour
- simulators must remain stable under load

## 9. Disclosure Timeline
0–24h: acknowledge  
1–7d: reproduce & classify  
7–30d: patch & validate  
30+d: public disclosure (if applicable)

## 10. Governance
Security decisions follow:
- semantic correctness
- ecosystem coherence
- long-term stability
- minimal attack surface
- deterministic behaviour

