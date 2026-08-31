# Architecture Decision Records (ADRs)

This directory stores Architecture Decision Records for KhaneYar.

## Purpose

ADRs capture significant technical and architectural decisions once the underlying question is real and evidence is available. Phase 0 establishes the mechanism only; it does not prematurely baseline product architecture.

## Numbering and lifecycle

- ADR IDs use four digits: `ADR-0001`, `ADR-0002`, and so on.
- IDs are never reused.
- One file records one significant decision.
- Accepted ADRs are immutable historical records. A later ADR may supersede an earlier ADR; the earlier file is not silently rewritten.
- Status values for real decisions are: `Proposed`, `Accepted`, `Superseded`, or `Deprecated`.
- A reservation file may use `Reserved` only to hold the first decision slot before a real architecture decision exists.

## Required content

Each real ADR must contain:

- ADR ID and title
- Status
- Date
- Owner
- Related Asana task(s)
- Decision scope
- Context
- Decision drivers
- Constraints and assumptions
- Options considered
- Decision
- Rationale
- Consequences and trade-offs
- Risks and mitigations
- Evidence / experiment / benchmark links
- Related requirements, PRs, commits, or Drive artifacts
- Revisit or supersession trigger

Use [`0000-adr-template.md`](./0000-adr-template.md) for new ADRs.

`0001-reserved-first-architecture-decision.md` intentionally reserves the first real architecture-decision slot. It is not an architecture choice and must be replaced by a substantive ADR only when the relevant architecture task is ready and evidence exists.

## Governance rule

Do not create or accept substantive ADRs before the underlying architectural question exists. Architecture decisions must be traceable to the relevant Asana task and supporting evidence. Production feature coding remains governed by the project stage gates and is not authorized merely because an ADR exists.
