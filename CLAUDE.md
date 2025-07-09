# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Wezterm-Auto is a macOS automation script for managing multiple projects in wezterm terminal with nvim. The script takes a fuzzy project path argument and either:
1. Switches focus to an existing wezterm window if the project is already open
2. Creates a new wezterm window, renames it based on the project path, navigates to the project directory, opens nvim, and switches focus to the new window

## Architecture

This is a simple automation project that consists of:
- A main script (to be implemented) that handles project fuzzy matching and wezterm automation
- Documentation directory (`wezterm-cli-docs/`) containing comprehensive wezterm CLI command references

## Key wezterm CLI Commands

The project relies heavily on wezterm CLI commands for automation:

- `wezterm cli list` - Lists all windows, tabs, and panes with their IDs, workspaces, titles, and working directories
- `wezterm cli spawn` - Creates new tabs/windows with optional parameters:
  - `--new-window` - Creates a new window instead of a tab
  - `--cwd CWD` - Sets the working directory
  - `--workspace WORKSPACE` - Sets the workspace name
- `wezterm cli set-window-title TITLE` - Sets the window title
- `wezterm cli activate-pane --pane-id ID` - Switches focus to a specific pane

## Development Notes

- Target platform: macOS only
- No build system or package manager detected - this appears to be a simple script-based project
- The main implementation script has not been created yet
- All wezterm CLI documentation is available in the `wezterm-cli-docs/` directory for reference

## Project Structure

```
wezterm-auto/
├── README.md                 # Project description (in Chinese)
└── wezterm-cli-docs/        # Complete wezterm CLI documentation
    ├── cli/                 # CLI subcommand documentation
    │   ├── spawn.md        # Window/tab creation
    │   ├── list.md         # Listing windows/tabs/panes
    │   ├── set-window-title.md  # Window title management
    │   └── ...             # Other CLI commands
    └── ...                 # Other wezterm features
```

## Implementation Strategy

The main script should:
1. Use `wezterm cli list` to check existing windows and their working directories
2. Implement fuzzy matching to find projects already open in wezterm
3. Use macOS-specific focus switching if project is found
4. Use `wezterm cli spawn --new-window --cwd <path>` to create new windows for unopened projects
5. Use `wezterm cli set-window-title` to rename windows based on project paths
6. Execute `nvim .` in the new window's working directory