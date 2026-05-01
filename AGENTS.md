# AGENTS.md

## Project

This is the long-term working context for the pet emergency triage and pre-arrival coordination platform.

The product is not an AI veterinarian. It is a pet emergency triage, hospital contact, navigation, and case-summary platform.

## Current Source Of Truth

When a new Codex window starts, read these files first:

1. `AGENTS.md`
2. `docs/项目进度.md`
3. `docs/项目规则.md`
4. `/Users/jack/Desktop/pet.md`

The previous prototype directory `/Users/jack/Desktop/项目/wod` was intentionally discarded. Do not continue from that prototype.

## Current Product Direction

MVP positioning:

- Help pet owners start an emergency flow within 60 seconds.
- The first screen should emphasize a large SOS emergency button.
- The user should answer as few questions as possible after tapping SOS.
- The system sends key information to the hospital side, and the doctor guides emergency measures by phone.
- The user side should not show red/yellow/green risk levels.
- The backend may keep red-flag markers for hospital prioritization and safety fallback.
- Generate structured records for later authorized, anonymized AI training.

The MVP starts with WeChat Mini Program first. H5, hospital admin, and operations admin follow the same monorepo architecture later.

## Current Technical Direction

Use one TypeScript monorepo when the project enters engineering implementation:

- Mini Program / H5: Taro + React + TypeScript
- Hospital admin: Next.js + React + TypeScript
- Operations admin: Next.js + React + TypeScript
- Backend API: NestJS + TypeScript
- Database: PostgreSQL
- ORM: Prisma
- Map provider: Gaode Map
- AI integration: backend abstraction only, disabled by default in MVP

Do not introduce Python, Java, Go, Rust, native iOS, or native Android during MVP unless the user explicitly approves a new plan.

## Current Stage

The current stage is document planning only.

Do not write implementation code, scaffold apps, install dependencies, or initialize WeChat Developer Tools project until the user explicitly says to enter the coding/build stage.

## Medical Safety Boundary

The system must not:

- diagnose disease
- prescribe medication
- provide medication dosage
- promise safety
- promise cure
- tell users to delay care when red-flag symptoms exist
- let AI downgrade a red emergency to yellow or green

The system may:

- collect structured emergency information
- identify backend-only red-flag risks for hospital prioritization
- recommend contacting a pet hospital
- send SOS information to a hospital queue
- support one-tap callback and navigation
- generate case summaries
- prepare owner-to-hospital communication text

## Development Rules

- Keep medical rules explicit in code and docs, not hidden only in prompts.
- Add tests for triage, SOS, permission, and anonymization logic when coding begins.
- Do not commit secrets, API keys, real user data, or unverified real hospital phone numbers.
- New dependencies require approval.
- Keep `main` stable. Do not do experimental scaffolding or large feature work directly on `main`.
- Keep changes scoped to the current task.

## Git Branch And Rollback Rules

Before any engineering implementation, scaffolding, dependency installation, or large document rewrite, create a dedicated branch first.

Recommended flow:

```bash
git switch main
git pull
git switch -c feature/<short-task-name>
```

Examples:

```bash
git switch -c feature/wechat-miniapp-skeleton
git switch -c feature/sos-flow-docs
git switch -c feature/hospital-admin-skeleton
```

Review rule:

- Keep `main` as the stable baseline.
- Implement new work on a feature branch.
- The owner reviews the result before merging.
- If the owner is not satisfied, do not merge the branch.
- If the work is satisfactory, merge it back to `main` and push.

Rollback patterns:

```bash
# If the work is on a feature branch and should be discarded:
git switch main
git branch -D feature/<short-task-name>

# If files were modified but not committed:
git restore .
git clean -fd

# If a commit was already made and pushed/shared:
git revert <commit-sha>
```

Avoid using destructive history rewrite commands such as `git reset --hard` on shared or pushed work unless the owner explicitly approves it and understands the risk.

## Handoff Rule

At the end of every meaningful work session, update `docs/项目进度.md` with:

- what changed
- current status
- next action
- blockers or risks
- files touched
