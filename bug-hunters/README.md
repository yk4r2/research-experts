# Bug Hunters

Systematic bug hunting with spec reconstruction, adversarial validation, and confidence-ranked reports. Hunt bugs, don't fix them.

## Philosophy

- **Spec-first** - can't find bugs without knowing intended behavior
- **Adversarial validation** - every finding challenged before reported
- **Confidence over severity** - certainty matters more than impact
- **Hunt, don't fix** - job ends at confirmed bug report
- **User decides** - present findings, never auto-remediate

## Agents

### orchestrator - Central Brain
The meta-agent coordinating systematic bug discovery. Reconstructs specs, spawns hunters, challenges findings, filters false positives.

**Workflow**:
1. Spec Reconstruction → 2. Hotspot Scan → 3. Hunter Deployment → 4. Adversarial Challenge → 5. Confidence Scoring → 6. Report

**Invokes**: All hunters + dev-experts coding agents (as challengers)

---

### logic-hunter - Spec Detective
Language-agnostic logic bug hunter. Finds spec-vs-implementation gaps, cross-component data flow issues, algorithm correctness failures.

**Focus**:
- Does code do what it's SUPPOSED to do?
- Contract violations, state machine errors
- Data/control flow bugs, invariant breaks

**Modes**:
- Scan: Bird's eye hotspot detection
- Hunt: Deep trace with evidence chain

**Invoked by**: orchestrator, user

---

### cpp-hunter - C++ Bug Hunter
C++ specific bug hunting. Memory corruption, UB, concurrency issues.

**Focus**:
- Use-after-free, double-free, buffer overflow
- Data races, deadlocks, memory ordering
- Signed overflow, strict aliasing, ODR violations

**Invoked by**: orchestrator (for C++ targets), user

---

### python-hunter - Python Bug Hunter
Python specific bug hunting. Async pitfalls, None propagation, type violations.

**Focus**:
- Mutable defaults, None propagation
- Async/await pitfalls, GIL issues
- Type hint violations, import cycles

**Invoked by**: orchestrator (for Python targets), user

---

## Flow

```
                         USER
                           │
                           ▼
                     ┌─────────────┐
                     │ orchestrator │ ◄─── Spec Reconstruction
                     └──────┬──────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        logic-hunter   cpp-hunter   python-hunter
              │             │             │
              └─────────────┴─────────────┘
                            │
                            ▼
                   ┌────────────────┐
                   │  CHALLENGE     │ ◄─── dev-experts agents
                   │  (adversarial) │      (cpp-dev, python-dev)
                   └────────┬───────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        FALSE_POSITIVE   CONFIRMED   NEEDS_CONTEXT
           (discard)         │         (re-hunt)
                            ▼
                   ┌────────────────┐
                   │  Confidence    │
                   │  Scoring       │
                   └────────┬───────┘
                            │
                            ▼
                      FINAL REPORT
                   (MEDIUM+ confidence)
```

## Confidence Levels

| Level | Criteria |
|-------|----------|
| `CERTAIN` | Spec violation + reproducible + challenger confirmed |
| `HIGH` | Strong evidence + challenger failed to disprove |
| `MEDIUM` | Circumstantial evidence + known pattern |
| `LOW` | Suspicious but weak evidence (filtered from report) |

## Evidence Weights

| Evidence | Weight |
|----------|--------|
| Explicit spec violation | +3 |
| Type system violation | +2 |
| Test failure proves it | +2 |
| Challenger failed | +2 |
| Naming contradiction | +1 |
| Comment/code mismatch | +1 |
| Plausible alternative | -1 |
| Valid counterargument | -2 |
| Intentional per user | -3 |

## Key Rules

1. **Spec first** - no hunting without reconstructed specification
2. **Challenge everything** - every finding faces adversarial validation
3. **Hunt only** - no fixes, no remediation, just reports
4. **User decides** - present options at every decision point
5. **Filter low confidence** - only MEDIUM+ makes the report

## Collaboration with dev-experts

Bug hunters **invoke** dev-experts agents as challengers:
- `cpp-dev` challenges `cpp-hunter` findings
- `python-dev` challenges `python-hunter` findings
- `rust-dev` acts as both hunter and challenger for Rust

This creates adversarial tension that filters false positives.

---

## Color Scheme

❤️ RED = orchestrator (decider, coordinator)
💛 YELLOW = hunters (checkers, bug finders)

---

## Installation

```bash
/plugin marketplace add git@github.com:DeevsDeevs/agent-system.git
/plugin install bug-hunters@deevs-agent-system
```
