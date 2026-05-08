
# CONTRIBUTING — Forge-Theory-Labs

## 1. Semantic Principles
- Determinism only
- Typed semantics
- Meaning-preserving changes
- Strict invariants
- Zero ambiguity
- Zero hallucination

## 2. Repository Structure
- README.md
- SCP Capsule
- Badges (wave, domain, type)
- Deterministic behaviour
- Clear directory layout

## 3. SCP Capsule Requirements
- Semantic Identity
- Purpose
- Core Behaviour
- Interpretation Rules
- Semantic Lineage
- Internal Invariants
- Mutation Rules
- Failure Modes
- Recovery Modes
- Integration Rules
- Affordances
- Boundaries
- External Interfaces
- Summary

## 4. Code Standards
- No global mutable state
- No hidden side effects
- No silent failure
- No ambiguous return types
- Explicit function purpose and output

### Commit Format
[TYPE] Short description

Longer explanation (optional)
Affected modules: X, Y, Z

Types: feat, fix, refactor, docs, capsule, infra

## 5. Branching Strategy
- main (stable)
- dev (active)
- feature/<name>
- capsule/<repo>

## 6. Pull Requests
- Purpose of change
- Wave/domain/type alignment
- Updated SCP Capsule if behaviour changed
- Deterministic validation
- No breaking changes unless justified

## 7. Testing
- Deterministic tests
- Reproducible behaviour
- No randomness unless seeded
- Rule-based validation for emergent systems

## 8. New Repositories
- Wave assignment
- Domain assignment
- Type assignment
- SCP Capsule
- README
- Badges
- Deterministic behaviour

## 9. Communication Style
- Clear
- Direct
- Technical
- Non-emotional
- Meaning-preserving

## 10. Governance
Maintained by the ecosystem architect. Decisions follow semantic correctness, coherence, and long-term maintainability.

