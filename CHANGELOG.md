# Changelog

All notable changes to this repository should be documented in this file.

## Update Policy

- Update this file for every structural code change, new feature, bug fix, or documentation/process change that affects contributors.
- Keep entries concise and grouped under: `Added`, `Changed`, `Fixed`, `Docs`.
- Use reverse chronological order (newest date first).

## [2026-03-02]

### Added
- Added Distribution Engineer agent role in [`.agents/agents/distribution-engineer.md`](.agents/agents/distribution-engineer.md).
- Added distribution workflow skill in [`.agents/skills/distribute/SKILL.md`](.agents/skills/distribute/SKILL.md).
- Added UI/UX Designer Specialist agent role in [`.agents/agents/ui-ux-designer.md`](.agents/agents/ui-ux-designer.md).
- Added design workflow skill in [`.agents/skills/design/SKILL.md`](.agents/skills/design/SKILL.md).

### Changed
- Updated [`.agents/skills/help/SKILL.md`](.agents/skills/help/SKILL.md) to reflect 9 available skills and include design-stage guidance.
- Updated [`.agents/skills/architecture/SKILL.md`](.agents/skills/architecture/SKILL.md) to hand off to `/design` before `/frontend`.
- Updated [`.agents/skills/frontend/SKILL.md`](.agents/skills/frontend/SKILL.md) to require `Design Spec (UI/UX Designer)` before implementation.
- Updated [`.agents/skills/qa/SKILL.md`](.agents/skills/qa/SKILL.md) to include design conformance validation.
- Updated [`AGENTS.md`](AGENTS.md) and [`README.md`](README.md) to include the mandatory `/design` phase in the development workflow.

### Docs
- Added repository onboarding guide for coding agents in [`.github/copilot-instructions.md`](.github/copilot-instructions.md).
- Enhanced [`AGENTS.md`](AGENTS.md) to require reading copilot instructions first and to align validation/changelog policies.
- Added this changelog to track structural, feature, fix, and documentation updates.