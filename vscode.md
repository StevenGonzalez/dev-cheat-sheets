# VS Code Cheat Sheet

## Table of Contents
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Command Palette](#command-palette)
- [File Management](#file-management)
- [Editing](#editing)
- [Navigation](#navigation)
- [Multi-cursor Editing](#multi-cursor-editing)
- [Search and Replace](#search-and-replace)
- [Code Folding](#code-folding)
- [IntelliSense](#intellisense)
- [Debugging](#debugging)
- [Extensions](#extensions)
- [Settings](#settings)
- [Themes](#themes)
- [Integrated Terminal](#integrated-terminal)
- [Git Integration](#git-integration)
- [Best Practices](#best-practices)

## Keyboard Shortcuts

### General
| Windows/Linux | Mac | Action |
|---------------|-----|--------|
| `Ctrl+Shift+P` | `Cmd+Shift+P` | Command Palette |
| `Ctrl+P` | `Cmd+P` | Quick Open (Go to File) |
| `Ctrl+Shift+N` | `Cmd+Shift+N` | New Window |
| `Ctrl+Shift+W` | `Cmd+Shift+W` | Close Window |
| `Ctrl+,` | `Cmd+,` | Open Settings |
| `Ctrl+K Ctrl+S` | `Cmd+K Cmd+S` | Keyboard Shortcuts |
| `Ctrl+`` | `Cmd+`` | Toggle Terminal |
| `F11` | `Cmd+Ctrl+F` | Toggle Fullscreen |

### File Operations
| Windows/Linux | Mac | Action |
|---------------|-----|--------|
| `Ctrl+N` | `Cmd+N` | New File |
| `Ctrl+O` | `Cmd+O` | Open File |
| `Ctrl+S` | `Cmd+S` | Save File |
| `Ctrl+Shift+S` | `Cmd+Shift+S` | Save As |
| `Ctrl+K S` | `Cmd+K S` | Save All |
| `Ctrl+W` | `Cmd+W` | Close File |
| `Ctrl+Shift+T` | `Cmd+Shift+T` | Reopen Closed Tab |
| `Ctrl+K Ctrl+W` | `Cmd+K Cmd+W` | Close All |

### Editing
| Windows/Linux | Mac | Action |
|---------------|-----|--------|
| `Ctrl+Z` | `Cmd+Z` | Undo |
| `Ctrl+Y` | `Cmd+Shift+Z` | Redo |
| `Ctrl+X` | `Cmd+X` | Cut Line |
| `Ctrl+C` | `Cmd+C` | Copy Line |
| `Ctrl+V` | `Cmd+V` | Paste |
| `Ctrl+Shift+K` | `Cmd+Shift+K` | Delete Line |
| `Alt+Up/Down` | `Option+Up/Down` | Move Line Up/Down |
| `Shift+Alt+Up/Down` | `Shift+Option+Up/Down` | Copy Line Up/Down |

### Selection
| Windows/Linux | Mac | Action |
|---------------|-----|--------|
| `Ctrl+A` | `Cmd+A` | Select All |
| `Ctrl+L` | `Cmd+L` | Select Current Line |
| `Ctrl+D` | `Cmd+D` | Select Word |
| `Ctrl+Shift+L` | `Cmd+Shift+L` | Select All Occurrences |
| `Ctrl+F2` | `Cmd+F2` | Select All Occurrences of Word |
| `Shift+Alt+Right` | `Shift+Option+Right` | Expand Selection |
| `Shift+Alt+Left` | `Shift+Option+Left` | Shrink Selection |

### Navigation
| Windows/Linux | Mac | Action |
|---------------|-----|--------|
| `Ctrl+G` | `Cmd+G` | Go to Line |
| `Ctrl+P` | `Cmd+P` | Go to File |
| `Ctrl+Shift+O` | `Cmd+Shift+O` | Go to Symbol |
| `Ctrl+T` | `Cmd+T` | Go to Symbol in Workspace |
| `F12` | `F12` | Go to Definition |
| `Alt+F12` | `Option+F12` | Peek Definition |
| `Shift+F12` | `Shift+F12` | Go to References |
| `Ctrl+Tab` | `Cmd+Tab` | Switch Between Tabs |

## Command Palette

The Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) is your gateway to all VS Code functionality:

### Essential Commands
```
> File: New File
> File: Open Folder
> File: Save All
> View: Toggle Terminal
> View: Toggle Sidebar
> Preferences: Open Settings
> Extensions: Install Extensions
> Git: Clone
> Terminal: Create New Terminal
> Format Document
> Transform to Uppercase
> Transform to Lowercase
> Sort Lines Ascending
> Developer: Reload Window
```

### Quick Tips
- Type `?` to see available commands
- Use `>` for commands
- Use `@` for symbols in current file
- Use `#` for symbols across workspace
- Type file names directly to open files

## File Management

### Explorer
- **Toggle Sidebar**: `Ctrl+B` / `Cmd+B`
- **Focus Explorer**: `Ctrl+Shift+E` / `Cmd+Shift+E`
- **New File**: Right-click in Explorer → New File
- **New Folder**: Right-click in Explorer → New Folder
- **Rename**: `F2` or right-click → Rename

### Quick Open
```bash
# Go to file
Ctrl+P / Cmd+P

# Go to line in current file
Ctrl+G / Cmd+G

# Go to symbol in current file
Ctrl+Shift+O / Cmd+Shift+O

# Go to symbol in workspace
Ctrl+T / Cmd+T
```

### Tabs and Groups
- **Split Editor**: `Ctrl+\` / `Cmd+\`
- **Focus Group**: `Ctrl+1/2/3` / `Cmd+1/2/3`
- **Move Tab to Group**: `Ctrl+Alt+Right/Left` / `Cmd+Option+Right/Left`
- **Close Tab**: `Ctrl+W` / `Cmd+W`
- **Close All Tabs**: `Ctrl+K Ctrl+W` / `Cmd+K Cmd+W`

## Editing

### Basic Text Manipulation
```bash
# Duplicate line
Shift+Alt+Down / Shift+Option+Down

# Move line up/down
Alt+Up/Down / Option+Up/Down

# Delete line
Ctrl+Shift+K / Cmd+Shift+K

# Insert line below
Ctrl+Enter / Cmd+Enter

# Insert line above
Ctrl+Shift+Enter / Cmd+Shift+Enter

# Join lines
Ctrl+J / Cmd+J
```

### Indentation
```bash
# Indent line
Ctrl+] / Cmd+]

# Outdent line
Ctrl+[ / Cmd+[

# Auto indent selection
Ctrl+K Ctrl+F / Cmd+K Cmd+F

# Format document
Shift+Alt+F / Shift+Option+F
```

### Comments
```bash
# Toggle line comment
Ctrl+/ / Cmd+/

# Toggle block comment
Shift+Alt+A / Shift+Option+A

# Add line comment
Ctrl+K Ctrl+C / Cmd+K Cmd+C

# Remove line comment
Ctrl+K Ctrl+U / Cmd+K Cmd+U
```

## Navigation

### Within File
```bash
# Go to beginning/end of line
Home/End

# Go to beginning/end of file
Ctrl+Home/End / Cmd+Home/End

# Go to matching bracket
Ctrl+Shift+\ / Cmd+Shift+\

# Go to definition
F12

# Peek definition
Alt+F12 / Option+F12

# Go back/forward
Alt+Left/Right / Ctrl+-/Ctrl+Shift+-
```

### Breadcrumbs
Enable breadcrumbs for better navigation:
```json
{
    "breadcrumbs.enabled": true
}
```

### Minimap
- **Toggle Minimap**: `View → Show Minimap`
- **Configure**: 
```json
{
    "editor.minimap.enabled": true,
    "editor.minimap.showSlider": "always"
}
```

## Multi-cursor Editing

### Creating Multiple Cursors
```bash
# Add cursor above/below
Ctrl+Alt+Up/Down / Cmd+Option+Up/Down

# Add cursor at mouse position
Alt+Click / Option+Click

# Select all occurrences of current word
Ctrl+Shift+L / Cmd+Shift+L

# Add next occurrence to selection
Ctrl+D / Cmd+D

# Skip current occurrence
Ctrl+K Ctrl+D / Cmd+K Cmd+D
```

### Multi-cursor Techniques
1. **Box Selection**: `Shift+Alt+Drag` / `Shift+Option+Drag`
2. **Column Selection**: `Ctrl+Shift+Alt+Arrow` / `Cmd+Shift+Option+Arrow`
3. **Find and Replace with Multiple Cursors**: Use `Ctrl+H` / `Cmd+H` with multiple selections

### Examples
```javascript
// Before: Select "name" and press Ctrl+D multiple times
const firstName = "John";
const lastName = "Doe";
const fullName = firstName + " " + lastName;

// After editing with multi-cursor:
const person_name = "John";
const person_surname = "Doe";
const person_fullname = person_name + " " + person_surname;
```

## Search and Replace

### Basic Search
```bash
# Find
Ctrl+F / Cmd+F

# Find next/previous
F3/Shift+F3 / Cmd+G/Cmd+Shift+G

# Find in selection
Alt+L / Option+L (in find widget)

# Case sensitive
Alt+C / Option+C (in find widget)

# Whole word
Alt+W / Option+W (in find widget)

# Regular expression
Alt+R / Option+R (in find widget)
```

### Replace
```bash
# Replace
Ctrl+H / Cmd+H

# Replace next
Ctrl+Shift+1 / Cmd+Shift+1

# Replace all
Ctrl+Alt+Enter / Cmd+Option+Enter
```

### Global Search
```bash
# Search across files
Ctrl+Shift+F / Cmd+Shift+F

# Replace across files
Ctrl+Shift+H / Cmd+Shift+H

# Search in specific files
Use include/exclude patterns:
*.js, !node_modules
```

### Regular Expression Examples
```regex
# Find email addresses
[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}

# Find phone numbers
\(\d{3}\)\s*\d{3}-\d{4}

# Find URLs
https?://[^\s]+

# Find HTML tags
<[^>]+>

# Capture groups for replacement
Find: (function)\s+(\w+)
Replace: const $2 = $1
```

## Code Folding

### Folding Commands
```bash
# Fold/unfold region
Ctrl+Shift+[ / Cmd+Shift+[
Ctrl+Shift+] / Cmd+Shift+]

# Fold all
Ctrl+K Ctrl+0 / Cmd+K Cmd+0

# Unfold all
Ctrl+K Ctrl+J / Cmd+K Cmd+J

# Fold level 1,2,3...
Ctrl+K Ctrl+1/2/3 / Cmd+K Cmd+1/2/3
```

### Custom Folding Regions
```javascript
// #region My Custom Region
function myFunction() {
    // Code here
}
// #endregion

/* #region CSS Custom Region */
.my-class {
    color: red;
}
/* #endregion */
```

## IntelliSense

### Triggering IntelliSense
```bash
# Trigger suggest
Ctrl+Space / Cmd+Space

# Trigger parameter hints
Ctrl+Shift+Space / Cmd+Shift+Space

# Quick fix
Ctrl+. / Cmd+.

# Show hover
Ctrl+K Ctrl+I / Cmd+K Cmd+I
```

### Code Actions
- **Auto Import**: Automatically import modules/packages
- **Organize Imports**: Remove unused and sort imports
- **Extract Method**: Extract selected code into a method
- **Generate Constructor**: Generate constructor from properties

### Snippets
Common snippets (type and press Tab):
```javascript
// JavaScript
log  → console.log()
func → function name() {}
iife → (function() {})()
try  → try-catch block
for  → for loop
if   → if statement

// HTML
!    → HTML5 boilerplate
div  → <div></div>
a    → <a href=""></a>
img  → <img src="" alt="">

// CSS
m10  → margin: 10px;
p20  → padding: 20px;
bc   → background-color:
```

## Debugging

### Setting Up Debugging
1. **Create launch.json**: `.vscode/launch.json`
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch Program",
            "type": "node",
            "request": "launch",
            "program": "${workspaceFolder}/app.js",
            "console": "integratedTerminal"
        }
    ]
}
```

### Debug Controls
```bash
# Start debugging
F5

# Start without debugging
Ctrl+F5 / Cmd+F5

# Stop debugging
Shift+F5

# Restart debugging
Ctrl+Shift+F5 / Cmd+Shift+F5

# Step over
F10

# Step into
F11

# Step out
Shift+F11

# Continue
F5
```

### Breakpoints
```bash
# Toggle breakpoint
F9

# Toggle conditional breakpoint
Right-click in gutter → Add Conditional Breakpoint

# Toggle logpoint
Right-click in gutter → Add Logpoint

# Enable/disable all breakpoints
Ctrl+Shift+F9 / Cmd+Shift+F9
```

### Debug Console
- Access via `View → Debug Console`
- Evaluate expressions during debugging
- Execute commands in the current context

## Extensions

### Essential Extensions
```bash
# Language Support
- Python
- JavaScript (ES6) code snippets
- C/C++
- Java Extension Pack
- Go
- Rust

# Productivity
- GitLens
- Bracket Pair Colorizer 2
- Auto Rename Tag
- Path Intellisense
- IntelliCode

# Themes
- Material Theme
- One Dark Pro
- Dracula Official

# Tools
- Live Server
- REST Client
- Docker
- Remote - SSH
- Prettier - Code formatter
```

### Managing Extensions
```bash
# Install extension
Ctrl+Shift+X / Cmd+Shift+X

# Enable/disable extension
Right-click extension → Enable/Disable

# Uninstall extension
Right-click extension → Uninstall

# Extension settings
Right-click extension → Extension Settings
```

### Recommended Extensions File
Create `.vscode/extensions.json`:
```json
{
    "recommendations": [
        "ms-python.python",
        "esbenp.prettier-vscode",
        "ms-vscode.vscode-json",
        "bradlc.vscode-tailwindcss",
        "ms-vscode.live-server"
    ]
}
```

## Settings

### Settings UI vs JSON
- **Settings UI**: `Ctrl+,` / `Cmd+,`
- **Settings JSON**: `Ctrl+Shift+P` → "Preferences: Open Settings (JSON)"

### Essential Settings
```json
{
    // Editor
    "editor.fontSize": 14,
    "editor.fontFamily": "'Fira Code', 'Courier New', monospace",
    "editor.fontLigatures": true,
    "editor.tabSize": 2,
    "editor.insertSpaces": true,
    "editor.wordWrap": "on",
    "editor.minimap.enabled": true,
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true,
    
    // Files
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 1000,
    "files.exclude": {
        "**/node_modules": true,
        "**/dist": true,
        "**/.DS_Store": true
    },
    
    // Terminal
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe",
    
    // Git
    "git.enableSmartCommit": true,
    "git.confirmSync": false,
    
    // Workbench
    "workbench.colorTheme": "One Dark Pro",
    "workbench.iconTheme": "material-icon-theme",
    "workbench.startupEditor": "newUntitledFile"
}
```

### Workspace Settings
Create `.vscode/settings.json` in your project:
```json
{
    "editor.tabSize": 4,
    "python.defaultInterpreterPath": "./venv/bin/python",
    "eslint.workingDirectories": ["./frontend"]
}
```

## Themes

### Popular Themes
- **One Dark Pro**: Dark theme with good syntax highlighting
- **Material Theme**: Google Material Design inspired
- **Dracula**: Dark theme with vibrant colors
- **Solarized**: Light and dark variants
- **Nord**: Arctic-inspired color palette

### Custom Theme Settings
```json
{
    "workbench.colorCustomizations": {
        "editor.background": "#1e1e1e",
        "editor.foreground": "#d4d4d4",
        "activityBar.background": "#2d2d30"
    },
    "editor.tokenColorCustomizations": {
        "comments": "#6A9955",
        "keywords": "#569cd6",
        "strings": "#ce9178"
    }
}
```

## Integrated Terminal

### Terminal Basics
```bash
# Toggle terminal
Ctrl+` / Cmd+`

# Create new terminal
Ctrl+Shift+` / Cmd+Shift+`

# Kill terminal
Click trash icon or Ctrl+C

# Split terminal
Ctrl+Shift+5 / Cmd+Shift+5

# Focus terminal/editor
Ctrl+` / Cmd+`
```

### Terminal Configuration
```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe",
    "terminal.integrated.shell.osx": "/bin/zsh",
    "terminal.integrated.shell.linux": "/bin/bash",
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.fontFamily": "Fira Code"
}
```

### Multiple Terminals
- Create multiple terminal instances
- Name terminals for easy identification
- Use different shells (bash, PowerShell, cmd)

## Git Integration

### Git Commands in VS Code
```bash
# Source Control panel
Ctrl+Shift+G / Cmd+Shift+G

# Stage changes
Click + next to file

# Unstage changes
Click - next to file

# Commit
Ctrl+Enter / Cmd+Enter (in commit message box)

# Push/Pull
Click ... in Source Control → Push/Pull

# View diff
Click file in Source Control panel
```

### Git Timeline
- View file history in Explorer
- See changes over time
- Compare versions

### GitLens Extension Features
- Blame annotations
- Code lens with git information
- Repository explorer
- File history
- Branch comparison

### Git Settings
```json
{
    "git.enableSmartCommit": true,
    "git.confirmSync": false,
    "git.autofetch": true,
    "diffEditor.ignoreTrimWhitespace": false
}
```

## Best Practices

### Workspace Organization
```
project/
├── .vscode/
│   ├── settings.json          # Project-specific settings
│   ├── launch.json           # Debug configurations
│   ├── tasks.json            # Build tasks
│   └── extensions.json       # Recommended extensions
├── src/
├── tests/
└── README.md
```

### Productivity Tips
1. **Learn Keyboard Shortcuts**: Focus on the most common ones
2. **Use Command Palette**: `Ctrl+Shift+P` / `Cmd+Shift+P` for everything
3. **Master Multi-cursor**: Speed up repetitive editing
4. **Customize Settings**: Tailor VS Code to your workflow
5. **Use Extensions Wisely**: Don't overload with unnecessary extensions

### Code Organization
- Use consistent indentation
- Enable format on save
- Use meaningful file names
- Organize code with regions/comments
- Keep related files in same folder

### Performance Tips
```json
{
    "files.watcherExclude": {
        "**/node_modules/**": true,
        "**/dist/**": true,
        "**/.git/**": true
    },
    "search.exclude": {
        "**/node_modules": true,
        "**/dist": true
    },
    "files.exclude": {
        "**/node_modules": true,
        "**/dist": true
    }
}
```

### Debugging Tips
- Use console.log strategically
- Set conditional breakpoints
- Use the Debug Console for quick evaluations
- Learn debugger-specific features for your language
- Use logpoints instead of console.log statements

---

*Remember: VS Code is highly customizable. Experiment with different settings, extensions, and workflows to find what works best for you.*