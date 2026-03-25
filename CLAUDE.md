# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working with this repository.

## Repository Overview

**super-duper-waffle** is a new, minimal repository initialized with a single README. No source code, build system, or tooling has been added yet.

- **Owner:** drymonkey08
- **Remote:** drymonkey08/super-duper-waffle
- **Default branch:** main
- **Current state:** Bootstrapped — awaiting project scaffolding

## Repository Structure

```
super-duper-waffle/
└── README.md       # Project title placeholder
```

## Development Branch

When contributing via Claude Code or automated tooling, use the designated feature branch:

- Branch: `claude/add-claude-documentation-lNhLd`
- Always push to `origin/<branch-name>` with `-u` flag: `git push -u origin <branch-name>`
- Never push directly to `main` without explicit permission

## Git Conventions

- Write clear, descriptive commit messages in imperative mood (e.g., "Add auth module", not "Added auth module")
- Keep commits focused — one logical change per commit
- Do not amend published commits; create new commits instead
- Never skip pre-commit hooks (`--no-verify`)

## Working with This Repo

Since this repository has no established stack yet, follow these principles when adding code:

1. **Discuss before scaffolding** — confirm the intended language/framework with the user before creating files
2. **Prefer editing existing files** over creating new ones when possible
3. **Keep it minimal** — avoid over-engineering or adding abstractions before they are needed
4. **Document as you go** — update this CLAUDE.md whenever significant structure is added

## Future Setup Checklist

When the project stack is decided, update this file with:

- [ ] Language and runtime (Node.js, Python, Go, etc.)
- [ ] Package manager and dependency management
- [ ] Build system and scripts (`npm run build`, `make`, etc.)
- [ ] Test framework and how to run tests
- [ ] Linting and formatting tools and configs
- [ ] Environment variable setup (`.env.example`)
- [ ] CI/CD pipeline details
- [ ] Deployment process

## Security Notes

- Do not commit secrets, API keys, or credentials
- Add a `.gitignore` before adding source code to avoid accidental secret exposure
- Use `.env.example` (not `.env`) to document required environment variables

## Updating This File

Keep CLAUDE.md up to date as the project evolves. Update it when:
- A new tech stack or framework is adopted
- Build, test, or deployment commands change
- New conventions or code style rules are established
- The directory structure changes significantly
