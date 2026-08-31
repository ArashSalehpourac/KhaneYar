# KhaneYar Git Workflow

**Control:** P0-12  
**Status:** Active  
**Scope:** Repository branches, commits, pull requests, merge policy, and `main` protection for `ArashSalehpourac/KhaneYar`.

## 1. Source of truth

- `main` is the only integration branch and represents the latest reviewed repository state.
- Production implementation is not authorized merely because a branch or PR exists; lifecycle-gate authorization still applies.
- Every material repository change must trace to an Asana task ID such as `P0-12`, `P5-03`, or `P10-15`.

## 2. Branch naming

Create one short-lived branch per controlled task or tightly coupled change.

Canonical pattern:

`p<phase>-<task-number>-<short-kebab-slug>`

Examples:

- `p0-12-git-workflow`
- `p3-11-recurrence-semantics`
- `p5-03-local-db-schema`
- `p10-15-secret-scan`

Rules:

1. Lowercase branch names only.
2. Use hyphens, not spaces or underscores.
3. The branch prefix must match the Asana task ID.
4. Do not create personal branches such as `arash-work`, `temp`, `new`, or `final`.
5. Delete task branches after successful merge unless retention is required for a documented reason.

## 3. Commit convention

Canonical commit subject:

`<TASK-ID>: <imperative summary>`

Examples:

- `P0-12: document Git workflow and main protection policy`
- `P4-06: refine onboarding permission copy`
- `P10-03: add recurrence boundary tests`

Commit rules:

- Keep the subject concise and outcome-oriented.
- One commit should represent one coherent change.
- Never include secrets, credentials, personal data, generated binaries, or environment-specific files that belong outside Git.
- Do not use meaningless subjects such as `update`, `fix`, `changes`, `final`, or `work`.
- During development, intermediate commits are allowed on the task branch; the final merge to `main` should normally use squash merge so `main` receives one controlled commit per PR.

## 4. Pull-request policy

All material changes target `main` through a pull request.

PR title pattern:

`<TASK-ID>: <controlled outcome>`

Each PR must contain:

- related Asana task ID and link when available;
- purpose and scope;
- summary of changes;
- evidence/tests/checks performed;
- risks or trade-offs;
- links to new/updated decision, ADR, risk, requirement, or evidence records when applicable;
- explicit confirmation that no secrets are included;
- explicit lifecycle authorization check if production implementation is present.

A PR must not be merged when:

- the task Definition of Done is not met;
- required evidence is missing;
- a blocking review comment remains unresolved;
- required tests/checks fail;
- the change introduces an undocumented architecture decision or material risk;
- production code is included before the lifecycle gates authorize it.

## 5. Review and merge rules

- Default merge method: **squash merge**.
- The squash commit subject must follow `<TASK-ID>: <imperative summary>`.
- Self-review is acceptable only while the project has a single active maintainer; the PR must still provide objective evidence/checks.
- Once another qualified maintainer/reviewer is active, require at least one approval for protected changes.
- Resolve review conversations before merge.
- Do not force-push `main` or rewrite published `main` history.
- Do not delete `main`.

## 6. `main` protection policy

Target protection for `main`:

1. Require a pull request before merging.
2. Require review conversation resolution.
3. Require at least one approving review once a second qualified reviewer exists.
4. Dismiss stale approvals when new commits materially change a reviewed PR, when supported by repository settings.
5. Require status checks after CI checks are established under P6-10.
6. Block force pushes.
7. Block branch deletion.
8. Apply the rule to administrators/maintainers where the account/repository plan supports it.

### Current verified state

As of 2026-08-31, GitHub reports `main` as **not protected** (`protected: false`, protection enforcement off). Therefore the controls above are the governing project policy, but GitHub does not yet technically enforce them.

Until technical protection is enabled:

- do not push directly to `main`;
- use a task branch and PR for every material change;
- use squash merge;
- record any emergency exception in the decision log and evidence register.

Technical protection should be enabled in GitHub settings as soon as the repository/account configuration permits it. P6-10 will later add CI checks that can become required status checks.

## 7. Emergency changes

Emergency direct-to-`main` changes are prohibited by default. If an exceptional recovery event makes the normal PR path impossible:

1. document the reason and affected scope;
2. record the exception in the Decision Log;
3. create evidence of the exact commit/change;
4. run the required checks immediately afterward;
5. restore normal PR-only operation.

## 8. Traceability

For every merged PR, maintain this chain where applicable:

`Asana task -> branch -> commits -> PR -> tests/evidence -> merge commit -> decision/ADR/risk/requirement records`

The Asana task should not move to DONE until its Definition of Done is satisfied and the relevant repository evidence is stable.

## 9. Examples

### Documentation/control task

- Asana: `P0-12`
- Branch: `p0-12-git-workflow`
- Commit: `P0-12: document Git workflow and main protection policy`
- PR: `P0-12: define Git branching and commit convention`
- Merge: squash

### Future implementation task

- Asana: `P8-04`
- Branch: `p8-04-recurrence-engine`
- Commits may be iterative on the branch.
- PR cannot merge until required tests, evidence, reviews, and lifecycle authorization are satisfied.

## 10. Definition of Done for P0-12

P0-12 is complete when:

- branch naming is documented;
- commit naming is documented;
- PR content/review/merge rules are documented;
- `main` protection requirements and current enforcement state are documented;
- the repository PR template points to Asana rather than the retired ClickUp workflow;
- the policy is merged into `main` through a controlled PR.
