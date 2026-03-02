# Copilot Instructions for `ai-coding-starter-kit`

Use this file as the primary operating guide for this repository. Follow it first, then read [`AGENTS.md`](../AGENTS.md).

## 1) Repository Summary

- **What this repo is:** A Next.js 16 + TypeScript starter for AI-assisted product development workflows (requirements → architecture → frontend/backend → QA → deploy).
- **Primary runtime:** Node.js (project pins Node via [`.nvmrc`](../.nvmrc), currently `v25.6.1`).
- **Frontend stack:** Next.js App Router, React 19, Tailwind CSS, shadcn/ui components.
- **Optional backend:** Supabase client scaffold is present but intentionally stubbed in [`src/lib/supabase.ts`](../src/lib/supabase.ts).
- **Repository size/shape:** Small-to-medium template repo with most code concentrated in [`src/`](../src/), workflow docs in [`docs/`](../docs/), and agent workflow metadata in [`.agents/`](../.agents/).

## 2) Fast Start (Always Use This Order)

From repo root:

1. **Use pinned Node version**
   - `nvm use` (reads [`.nvmrc`](../.nvmrc)).
2. **Install dependencies first**
   - `npm install`
3. **Run production build as primary validation**
   - `npm run build`
4. **Run dev server only when interactive verification is needed**
   - `npm run dev`
5. **Run prod server only after successful build**
   - `npm run start`

## 3) Verified Command Matrix (Observed in this repo)

### Bootstrap
- ✅ `npm install`
  - Works and is idempotent.
  - Observed: one high-severity vulnerability warning from `npm audit` (not a build blocker).

### Build
- ✅ `npm run build`
  - Works successfully.
  - Performs compile + TypeScript + static generation checks.
  - This is the most reliable gate in current repository state.

### Run (Dev)
- ✅ `npm run dev`
  - Starts quickly (observed ~626ms to ready).
  - Serves at `http://localhost:3000`.

### Run (Production)
- ✅ `npm run start`
  - Works after build.
  - Serves at `http://localhost:3000`.

### Lint
- ⚠️ `npm run lint` currently fails in this repo.
  - Error observed:
    - `Invalid project directory provided, no such directory: .../lint`
- ⚠️ `npx eslint .` also fails due ESLint v9 flat-config expectation while repo uses [`.eslintrc.json`](../.eslintrc.json).
- **Agent guidance:** Until lint config/scripts are updated, do **not** treat lint as a reliable gate. Use `npm run build` + targeted file review as validation.

### Test
- ⚠️ No test script is defined in [`package.json`](../package.json).
  - `npm run test` fails with `Missing script: "test"`.
- **Agent guidance:** For now, rely on build success + manual/feature-level checks.

## 4) Preconditions and Postconditions

### Preconditions before changes
- Always install deps with `npm install` before validation.
- Confirm expected scripts with `npm run` if unsure.
- Read existing rules in [`.agents/rules/`](../.agents/rules/) before making structural changes.

### Postconditions before submitting work
- `npm run build` passes.
- If UI changed, sanity-check with `npm run dev`.
- Update feature tracking when relevant in [`features/INDEX.md`](../features/INDEX.md).
- Add changelog entry in [`CHANGELOG.md`](../CHANGELOG.md) for feature/bugfix/structural changes.

## 5) Project Layout (Where to Change What)

### Core application code
- [`src/app/layout.tsx`](../src/app/layout.tsx): global layout and metadata.
- [`src/app/page.tsx`](../src/app/page.tsx): default landing page entry.
- [`src/app/globals.css`](../src/app/globals.css): global Tailwind/css variable theme tokens.

### UI system
- [`src/components/ui/`](../src/components/ui/): shadcn/ui primitives (do not recreate existing primitives).
- shadcn config in [`components.json`](../components.json).

### Utilities and hooks
- [`src/lib/utils.ts`](../src/lib/utils.ts): shared utility (`cn`).
- [`src/lib/supabase.ts`](../src/lib/supabase.ts): optional Supabase client scaffold.
- [`src/hooks/`](../src/hooks/): reusable hooks.

### Product and workflow documentation
- [`docs/PRD.md`](../docs/PRD.md): product requirements baseline.
- [`features/INDEX.md`](../features/INDEX.md): feature registry/status.
- [`features/README.md`](../features/README.md): feature spec format.
- [`docs/production/`](../docs/production/): production hardening guides.

### Agent operating system (important)
- [`AGENTS.md`](../AGENTS.md): high-level operating conventions.
- [`.agents/rules/general.md`](../.agents/rules/general.md): file handling, feature tracking, handoff conventions.
- [`.agents/rules/frontend.md`](../.agents/rules/frontend.md): shadcn-first frontend constraints.
- [`.agents/rules/backend.md`](../.agents/rules/backend.md): API, DB, and validation expectations.
- [`.agents/rules/security.md`](../.agents/rules/security.md): secrets/auth/security requirements.

## 6) CI / Automation Notes

- No GitHub workflow files were found under [`.github/workflows/`](../.github/workflows/).
- In absence of CI pipelines, locally replicate quality checks with:
  1. `npm install`
  2. `npm run build`
  3. `npm run dev` (if UI behavior changed)

## 7) Root File Inventory (Quick Reference)

Top-level files currently include:
- [`.env.local.example`](../.env.local.example)
- [`.eslintrc.json`](../.eslintrc.json)
- [`.gitignore`](../.gitignore)
- [`.nvmrc`](../.nvmrc)
- [`AGENTS.md`](../AGENTS.md)
- [`CHANGELOG.md`](../CHANGELOG.md)
- [`components.json`](../components.json)
- [`next.config.ts`](../next.config.ts)
- [`package.json`](../package.json)
- [`package-lock.json`](../package-lock.json)
- [`postcss.config.mjs`](../postcss.config.mjs)
- [`README.md`](../README.md)
- [`tailwind.config.ts`](../tailwind.config.ts)
- [`tsconfig.json`](../tsconfig.json)

## 8) Known Friction + Workarounds

1. **Lint command mismatch in current toolchain**
   - Symptom: `npm run lint` fails.
   - Workaround: use `npm run build` as primary gate until lint config migration is implemented.

2. **No automated tests configured**
   - Symptom: `npm run test` missing.
   - Workaround: build + focused manual validation in dev server.

3. **Optional backend can confuse first-time agents**
   - [`src/lib/supabase.ts`](../src/lib/supabase.ts) is intentionally stubbed.
   - Only enable Supabase after env vars are configured in [`.env.local.example`](../.env.local.example) → local `.env.local`.

## 9) Decision Policy for Agents

- Trust this instruction file as source-of-truth for command order and validation.
- Only perform broad repository search when:
  1. Information here is missing for your task, or
  2. You observe behavior that contradicts these instructions.
- Prefer minimal, targeted edits and avoid introducing new frameworks or structural patterns unless explicitly requested.