# Status Model

## Start Date

Choose the earliest defensible project activity and record the basis:

1. First meaningful commit when commit history is available.
2. Repository creation date when no earlier meaningful evidence is available.
3. Explicit project start date in a trusted project document when it clearly identifies the project.

Do not silently present a repository creation date as the development start date. Format as `YYYY-MM-DD (first meaningful commit)` or equivalent.

## Stage

Use one primary stage:

- `Planning`: requirements or design exist, but no executable slice is verified.
- `Prototype`: executable experiment exists; architecture or core behaviour is still being explored.
- `MVP`: core user journey works end to end with intentionally limited scope.
- `Beta`: MVP is available to testers and is receiving stabilization or launch work.
- `Production`: released for normal users and actively maintained.
- `Paused`: intentionally inactive with possible continuation.
- `Closed`: explicitly ended or archived.
- `Unknown`: evidence is insufficient or contradictory.

## Progress Estimate

Report a conservative 0–100 estimate only when the project has a stated scope. Base it on evidence across these dimensions:

- Core functionality: 35%
- Verification and reliability: 20%
- User experience and accessibility: 15%
- Deployment or distribution readiness: 15%
- Documentation and operations: 10%
- Validation with intended users: 5%

Reweight unavailable dimensions explicitly. Do not compare percentages across projects with materially different scopes. For unclear scope, use `Not estimable` instead of inventing a number.

## Activity

Classify activity from the most recent meaningful evidence:

- `Active`: meaningful activity within 14 days.
- `Quiet`: last meaningful activity 15–30 days ago.
- `Stale`: last meaningful activity more than 30 days ago without a pause decision.
- `Paused` or `Closed`: use the explicit project decision regardless of recency.

Ignore automated dependency noise unless it changes delivery status.

## Confidence

- `High`: default-branch code, tests, release or deployment evidence supports the conclusion.
- `Medium`: multiple consistent documents or development branches support the conclusion, but production evidence is missing.
- `Low`: sparse, conflicting, inaccessible or plan-only evidence.

## Risk Categories

Use only relevant categories:

- Product scope
- Technical correctness
- Testing and reliability
- Deployment or operational cost
- External API or data dependency
- Distribution and user acquisition
- Content or art production
- Legal, licensing or privacy
- Maintenance capacity

