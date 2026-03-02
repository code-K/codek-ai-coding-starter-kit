# AI Coding Starter Kit

> A Next.js template with an AI-powered development workflow using specialized skills for Requirements, Architecture, Frontend, Backend, QA, and Deployment.

## Read Order (Mandatory)

1. **Read [`.github/copilot-instructions.md`](.github/copilot-instructions.md) first.**
2. Then use this file for workflow conventions and project-level policy.
3. Use repository search only when the copilot instructions are incomplete or proven incorrect.

## Tech Stack

- **Framework:** Next.js 16 (App Router), TypeScript
- **Styling:** Tailwind CSS + shadcn/ui (copy-paste components)
- **Backend:** Supabase (PostgreSQL + Auth + Storage) - optional
- **Deployment:** Vercel
- **Validation:** Zod + react-hook-form
- **State:** React useState / Context API

## Project Structure

```
src/
  app/              Pages (Next.js App Router)
  components/
    ui/             shadcn/ui components (NEVER recreate these)
  hooks/            Custom React hooks
  lib/              Utilities (supabase.ts, utils.ts)
features/           Feature specifications (PROJ-X-name.md)
  INDEX.md          Feature status overview
docs/
  PRD.md            Product Requirements Document
  production/       Production guides (Sentry, security, performance)
.agents/
  rules/            Auto-applied coding and security rules
  skills/           Workflow skill definitions
```

## Development Workflow

1. `/requirements` - Create feature spec from idea
2. `/architecture` - Design tech architecture (PM-friendly, no code)
3. `/frontend` - Build UI components (shadcn/ui first)
4. `/backend` - Build APIs, database, RLS policies
5. `/qa` - Test against acceptance criteria + security audit
6. `/deploy` - Deploy to Vercel + production-ready checks

## Feature Tracking

- All features tracked in [`features/INDEX.md`](features/INDEX.md).
- Feature specs live in [`features/PROJ-X-name.md`](features/).
- Every skill should read the index before starting and update it when status changes.

## Validation Policy for Agents

- Treat [`npm run build`](package.json) as the required quality gate.
- Use [`npm run dev`](package.json) for interactive UI verification when frontend behavior changes.
- Keep in mind lint/test scripts may not always be fully operational; follow current guidance in [`.github/copilot-instructions.md`](.github/copilot-instructions.md).

## Key Conventions

- **Feature IDs:** PROJ-1, PROJ-2, etc. (sequential)
- **Commits:** `feat(PROJ-X): description`, `fix(PROJ-X): description`
- **Single Responsibility:** One feature per spec file
- **shadcn/ui first:** NEVER create custom versions of installed shadcn primitives
- **Read before edit:** Never assume file contents from memory
- **Human-in-the-loop:** All workflows have user approval checkpoints

## Build & Test Commands

```bash
npm run dev        # Development server (localhost:3000)
npm run build      # Production build
npm run lint       # ESLint
npm run start      # Production server
```

## Product Context

- [`docs/PRD.md`](docs/PRD.md)

## Feature Overview

- [`features/INDEX.md`](features/INDEX.md)

## Changelog Policy

- Record structural changes, feature additions, and bug fixes in [`CHANGELOG.md`](CHANGELOG.md).
- Keep entries concise, dated, and categorized (Added/Changed/Fixed/Docs).
