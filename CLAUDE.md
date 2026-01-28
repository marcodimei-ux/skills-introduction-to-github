# CLAUDE.md - AI Assistant Guide

This document provides guidance for AI assistants working with this repository.

## Repository Overview

This is a **GitHub Skills** course repository for "Introduction to GitHub". It is an interactive learning experience that teaches new users fundamental GitHub concepts including:

- Creating branches
- Making commits
- Opening pull requests
- Merging pull requests

The course is designed as a template repository that learners copy to their own account and progress through step-by-step.

## Repository Structure

```
skills-introduction-to-github/
├── .github/
│   ├── dependabot.yml          # Dependabot config for GitHub Actions updates
│   ├── steps/                  # Step content (markdown instructions)
│   │   ├── -step.txt           # Current step tracker (contains step number)
│   │   ├── 0-welcome.md        # Welcome/initial step
│   │   ├── 1-create-a-branch.md
│   │   ├── 2-commit-a-file.md
│   │   ├── 3-open-a-pull-request.md
│   │   ├── 4-merge-your-pull-request.md
│   │   └── X-finish.md         # Completion/congratulations step
│   └── workflows/              # GitHub Actions workflows
│       ├── 0-welcome.yml       # Triggers on template clone
│       ├── 1-create-a-branch.yml
│       ├── 2-commit-a-file.yml
│       ├── 3-open-a-pull-request.yml
│       └── 4-merge-your-pull-request.yml
├── images/                     # Tutorial screenshots (PNG files)
├── .gitignore                  # Standard gitignore for compiled/OS files
├── LICENSE                     # MIT License (Copyright GitHub, Inc.)
└── README.md                   # Dynamic readme showing current step
```

## Key Concepts

### Step Tracking System

The course tracks learner progress via:

1. **`.github/steps/-step.txt`**: Contains the current step number (0, 1, 2, 3, 4, or X)
2. **Workflows**: Each workflow listens for specific events and advances the step
3. **`skills/action-update-step@v2`**: GitHub Action that updates the README content based on current step

### Workflow Triggers

| Workflow | Trigger Event | Condition |
|----------|--------------|-----------|
| 0-welcome | Push to `main` | Step is 0, repo is not template |
| 1-create-a-branch | Branch creation | Step is 1, branch is `my-first-branch` |
| 2-commit-a-file | Push to `my-first-branch` | Step is 2 |
| 3-open-a-pull-request | PR opened/reopened | Step is 3, head branch is `my-first-branch` |
| 4-merge-your-pull-request | Push to `main` | Step is 4 |

### Expected Branch Name

The course expects learners to create a branch named **`my-first-branch`**. This is hardcoded in workflow conditions.

## Development Guidelines

### For Course Maintainers

1. **Editing Step Content**: Modify files in `.github/steps/` to update instructions
2. **Updating Images**: Replace files in `images/` directory (keep same filenames or update references)
3. **Workflow Changes**: Ensure the `skills/action-update-step@v2` action is compatible with any changes

### Dependabot Configuration

- Package ecosystem: `github-actions`
- Update interval: Monthly
- Only monitors workflow action versions

### License

MIT License - Copyright GitHub, Inc.

## File Conventions

- **Markdown files**: Use GitHub-flavored markdown with HTML where needed
- **Images**: PNG format, stored in `/images/` directory
- **Step markers**: Use emoji sparingly (`:wave:`, `:tada:`, `:sparkles:`, etc.)
- **Author notes**: Enclosed in `<!-- -->` HTML comments at top of step files

## Important Notes for AI Assistants

1. **This is a template repository**: It's designed to be copied, not modified directly for learning
2. **README is dynamic**: Content changes based on `-step.txt` value - don't treat it as static
3. **Workflow dependencies**: Each step's workflow depends on the step counter matching
4. **Branch naming matters**: `my-first-branch` is required - don't suggest alternative names
5. **No build system**: This is pure documentation/workflow - no compilation or test commands
6. **Images are instructional**: Screenshots show GitHub UI elements for learner reference

## Common Tasks

### Updating Step Instructions

1. Edit the corresponding `.github/steps/N-*.md` file
2. Maintain the existing structure (author notes, headers, keyboard activities)
3. Keep image references pointing to `/images/` directory

### Adding a New Step

1. Create new step markdown in `.github/steps/`
2. Create corresponding workflow in `.github/workflows/`
3. Update previous workflow's `to_step` value
4. Update `skills/action-update-step` parameters

### Updating Dependencies

- GitHub Actions are updated via Dependabot (monthly)
- Primary dependencies: `actions/checkout@v4`, `skills/action-update-step@v2`
