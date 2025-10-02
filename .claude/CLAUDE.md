# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Nushell configuration repository containing modular scripts for development workflows, DevOps tools, and system automation. The repository uses a manifest-based system (__.toml) to manage and sync modules to separate GitHub repositories under the fj0r organization.

## Core Technologies

- **Nushell**: Primary shell language for all scripts and configuration
- **Git**: Version control and workflow automation with custom hooks
- **Container Tools**: Docker, Podman, Nerdctl support via unified scripts
- **Kubernetes**: kubectl wrapper with enhanced completions and shortcuts

## Repository Architecture

### Configuration Files
- **config.nu**: Main Nushell configuration, sources `scripts/main/mod.nu`
- **env.nu**: Environment setup with prompt configuration
- **__.nu**: Repository-specific commands (module sync, git hooks, testing)
- **__.toml**: Manifest defining module sources, destinations, and publication settings

### Module System
The repository follows a modular structure where each subdirectory in `scripts/` represents a standalone module that can be synced to its own GitHub repository:

- `scripts/[module]/` - Module implementation files
- `scripts/[module]/mod.nu` - Module entry point
- `scripts/[module]/README.md` - Module documentation
- `scripts/main/` - Core configuration loaded by config.nu

### Key Modules
- **git**: Git workflow commands (gs, gl, gb, gp, ga, gc, gd, gm, gr, gcp, grmt, gbs, git-sync)
- **project**: Directory-based commands, git hooks, environment parsing
- **docker/kubernetes**: Container and K8s management with unified interfaces
- **scratch**: Scratch pad and code execution utilities
- **llm/ai**: AI integration commands
- **argx**: Argument parsing utilities
- **power**: Powerline-style prompt
- **cwdhist**: Command history tracking by directory
- **history-utils**: Command history analysis and visualization
- **ssh**: SSH connection management

## Common Commands

### Development Workflow
```bash
# Test in container
nu -c 'use __; test in container'

# Generate README from manifest
nu -c 'use __; gen README'

# Update TODO files for tracked modules
nu -c 'use __; update todo'

# Rename completion functions to new style
nu -c 'use __; rename-cmpl-func <file> --dry-run'
```

### Module Management
```bash
# Sync modules to separate repositories (runs on pre-push hook)
nu -c 'use __; dump nu_scripts'

# Sync specific modules
nu -c 'use __; dump nu_scripts git docker'

# Reverse sync (pull from repos back to this repo)
nu -c 'use __; dump nu_scripts --reverse'
```

### Git Workflow
The repository implements custom git hooks via the `git-hooks` function:
- **pre-commit**: Auto-generates README.md from manifest
- **pre-push**: Syncs modules to separate GitHub repositories

Git commands use intuitive shortcuts:
- `gs` - status/stash
- `gl` - log/show
- `gb` - branch operations
- `gp` - pull/push/fetch
- `ga` - add/rm/restore
- `gc` - commit
- `gd` - diff
- `gm` - merge
- `gr` - rebase

## Code Standards

### Nushell Conventions
- Completion functions use `cmpl-` prefix (e.g., `cmpl-mod`)
- Export public functions with `export def`
- Use `const` for file-scoped constants
- Destructure parameters in function signatures
- Prefer pipelines over intermediate variables

### Module Structure
Each module should have:
1. `mod.nu` - Main module file with exported functions
2. `README.md` - Documentation (auto-linked in root README)
3. Optional subdirectories for complex modules

### Naming Conventions
- Functions: kebab-case (e.g., `git-sync`, `test in container`)
- Files: lowercase with hyphens or underscores
- Completion functions: `cmpl-<context>` prefix
- Environment variables: UPPERCASE with underscores

## Manifest Configuration

The `__.toml` manifest controls module publishing:

```toml
[[manifest]]
from = "git"           # Directory in scripts/
to = "git"             # Published repo name (becomes git.nu)
rank = 2               # Sort order in README
title = "Git"          # Display title in README
disable = false        # Skip publishing if true
```

## Architecture Notes

### Module Synchronization System
The `git-sync` function in `__.nu` handles bidirectional sync between this monorepo and individual module repositories. It:
1. Uses rsync to copy files from `scripts/<from>` to `dest/<to>`
2. Initializes git repos with specified remotes
3. Executes post-sync hooks to move README files
4. Automatically commits and pushes changes

### Dynamic Loading
The main configuration supports dynamic loading:
- `~/.env.nu` - Loaded before main config if it exists
- `~/.nu` - Loaded after main config for user customizations

### Completion System
Completions use closure-based completion functions with the `cmpl-` prefix. These integrate with Nushell's native completion system and support fuzzy matching.

### Container Abstraction
Container commands abstract over Docker/Podman/Nerdctl using `$env.CNTRCTL` to select the runtime, enabling portable scripts across different container engines.
