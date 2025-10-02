# Nushell Configuration Library

## Overview
This is a comprehensive collection of Nushell scripts and configurations for enhancing command-line workflows. It includes utilities for AI integration, Git operations, Docker/Kubernetes management, project management, and various other productivity tools.

**Version**: Nushell 0.104.0  
**Last Updated**: October 2, 2025

## Project Purpose
This repository serves as a centralized configuration and script library for Nushell users, providing:
- AI/LLM integration for command-line workflows
- Git workflow automation and utilities
- Docker and Kubernetes management tools
- Scratch pad and todo management
- SSH configuration management
- Project-based command execution
- Powerline prompt customization
- Command history utilities

## Project Structure
- `config.nu` - Main Nushell configuration file
- `env.nu` - Environment variables and prompt configuration
- `scripts/` - Collection of modular Nushell scripts organized by functionality:
  - `llm/` - AI and LLM integration tools
  - `git/` - Git workflow utilities
  - `docker/` - Docker/container management
  - `kubernetes/` - Kubernetes utilities
  - `scratch/` - Scratch pad, todo, and code executor
  - `project/` - Project-based commands and git hooks
  - `power/` - Powerline prompt configuration
  - `ssh/` - SSH management utilities
  - And many more...

## How to Use in Replit
This project runs an interactive Nushell environment where you can:

1. **Interactive Shell**: The console provides a Nushell REPL where you can execute commands
2. **Load Scripts**: Scripts are automatically sourced from the `scripts/` directory
3. **Try Commands**: Explore the various utilities like:
   - AI commands: `ai-session`, `ai-do`, `ai-assistant`
   - Git commands: Various git workflow shortcuts
   - Scratch: `scratch-list`, `scratch-add`, `scratch-edit`
   - And many more documented in individual script README files

## Configuration Files
- `__.toml` - Manifest file defining script modules and their organization
- `__.nu` - Utility functions for managing and syncing the script collection
- `.replit` - Replit environment configuration

## Key Features
1. **AI Integration** (`scripts/llm/`): Use AI in Nushell for tasks like generating git commit messages, code summaries, and more
2. **Git Workflows** (`scripts/git/`): Streamlined git operations and workflow automation
3. **Container Management** (`scripts/docker/`, `scripts/kubernetes/`): Tools for managing Docker and Kubernetes
4. **Scratch System** (`scripts/scratch/`): Todo list, code executor, and counter
5. **Project Management** (`scripts/project/`): Directory-based commands and git hooks

## Recent Changes
- **October 2, 2025**: Initial Replit setup
  - Installed Nushell 0.104.0 via Nix
  - Configured interactive shell workflow
  - Documented project structure and usage

## User Preferences
- Environment: Replit with Nix package manager
- Shell: Nushell (interactive console)
- Output: Console-based TUI for shell interactions

## Architecture Notes
- Modular script organization using Nushell's module system
- Scripts can be used independently or composed together
- Configuration follows Nushell conventions (config.nu, env.nu)
- Manifest system (__.toml) for organizing and distributing scripts
