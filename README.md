# Augment Code Rules & Instructions

This repository contains custom rules and instructions for [Augment Code](https://www.augmentcode.com/) AI assistant, configured to enhance development workflows with best practices and safety guardrails.

It integrates the [bgizdov/superpowers](https://github.com/bgizdov/superpowers) skill system (a fork of [obra/superpowers](https://github.com/obra/superpowers)) to provide advanced workflow automation.

## Overview

This configuration extends Augment with:
- **Custom Rules**: Project-specific guidelines for deployment safety, documentation, and test-driven development
- **Superpowers Skills**: Advanced workflow automation from [bgizdov/superpowers](https://github.com/bgizdov/superpowers)

## Structure

```
.
├── instructions.md          # Main instruction file that references all rules
├── rules/                   # Custom rules directory
│   ├── deploy.md           # Deployment safety rules
│   ├── docs.md             # Documentation guidelines
│   └── tdd.md              # Test-driven development rules
└── superpowers-instructions.md  # Superpowers workflow guide (local)
```

## Rules

### Deployment Safety (`rules/deploy.md`)
Prevents accidental production deployments by requiring explicit permission before running:
- Deployment scripts
- Package publishing commands
- Database migrations
- Infrastructure provisioning

### Documentation (`rules/docs.md`)
Enforces minimal, purposeful documentation:
- Keep README.md concise and essential
- Avoid over-documentation
- Only create docs when explicitly requested
- Organize additional docs in `docs/` directory

### Test-Driven Development (`rules/tdd.md`)
Enforces TDD principles:
- Write tests first
- Follow RED-GREEN-REFACTOR cycle
- Maintain test coverage
- Update existing tests with code changes

## Superpowers Integration

This configuration uses the [Superpowers](https://github.com/bgizdov/superpowers) skill system, which provides:

- **brainstorming** - Design refinement before coding
- **test-driven-development** - RED-GREEN-REFACTOR enforcement
- **systematic-debugging** - Root cause analysis
- **writing-plans** - Detailed implementation planning
- **executing-plans** - Batch execution with checkpoints
- **requesting-code-review** - Pre-review checklist
- **using-git-worktrees** - Parallel development branches
- And more...

See `superpowers-instructions.md` for the complete workflow guide.

## Usage

This repository is designed to be used as Augment's configuration directory (`~/.augment`). The `instructions.md` file references all rules and the superpowers system, which Augment loads automatically.

