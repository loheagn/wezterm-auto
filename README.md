# Wezterm-Auto

A macOS automation tool for quickly switching and managing multiple projects in WezTerm.

*Read this in other languages: [中文](README.zh.md)*

## Motivation

As developers, we frequently need to switch between different projects. The traditional approach involves manually opening terminals, navigating to project directories, starting editors, etc. This process is tedious and repetitive. Wezterm-Auto aims to simplify this workflow by enabling you to:

- Intelligently detect if a project is already open in WezTerm
- If already open, directly switch to the corresponding tab
- If not open, automatically create a new session and launch nvim
- Support fuzzy search to quickly locate project directories

## Features

### 🔍 Smart Project Detection
- Automatically detects if a project is already open in WezTerm
- Precise path matching to avoid false matches

### 🚀 Quick Project Switching
- If project is open: directly activate the corresponding tab and switch focus
- If project is not open: automatically create a new tab/window and launch nvim

### 🔎 Fuzzy Search Support
- Supports exact match, prefix match, and contains match
- Intelligently searches for projects in the HOME directory
- Priority: exact match > prefix match > contains match

### 🖥️ Smart Window Management
- If WezTerm is not running: automatically start and display in fullscreen
- If WezTerm is running: create a new tab in the existing window
- Automatically set window and tab titles

## Installation & Usage

### Installation
```bash
# Clone the project
git clone <repository-url> ~/wezterm-auto
cd ~/wezterm-auto

# Create symbolic link to ~/bin (ensure ~/bin is in PATH)
ln -sf "$(pwd)/wezterm-auto" ~/bin/wezterm-auto
```

### Usage
```bash
# Use full path
wezterm-auto ~/projects/my-app

# Use relative path
wezterm-auto ./my-project

# Use fuzzy matching (search in HOME directory)
wezterm-auto my-app    # Will find ~/my-app or ~/my-application
wezterm-auto blog      # Will find ~/blog or ~/my-blog
```

### Fuzzy Matching Rules
1. **Exact Match**: Prioritize directories with exact name match
2. **Prefix Match**: Find directories starting with the input
3. **Contains Match**: Find directories containing the input string

For example, when inputting `blog`:
- If `~/blog` exists, it will be selected first
- If not, but `~/blog-site` exists, it will be selected
- Finally, consider contains matches like `~/my-blog`

## How It Works

### Core Workflow
1. **Path Resolution**: Use fuzzy matching algorithm to resolve user input project path
2. **Session Detection**: Check if project is already open via `wezterm cli list`
3. **Smart Switching**: Choose to activate existing session or create new session based on detection results
4. **Focus Management**: Use AppleScript to switch application focus and window state

### Technical Implementation
- **WezTerm CLI**: Use `wezterm cli` commands to manage windows, tabs, and panes
- **jq**: Parse JSON format window information
- **AppleScript**: Implement macOS window focus switching and fullscreen functionality
- **Bash**: Main script logic and system calls

## System Requirements

- macOS system
- WezTerm terminal
- jq (JSON processing tool)
- Neovim

## Project Structure

```
wezterm-auto/
├── wezterm-auto           # Main script file
├── README.md              # Project documentation (English)
├── README.zh.md           # Project documentation (Chinese)
├── CLAUDE.md              # Development guide
└── wezterm-cli-docs/      # WezTerm CLI documentation reference
    └── cli/               # Various CLI command documentation
```

## Contributing

Issues and Pull Requests are welcome to improve this project.