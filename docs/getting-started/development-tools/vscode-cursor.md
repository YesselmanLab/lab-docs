# VS Code and Cursor Guide

VS Code (Visual Studio Code) and Cursor are powerful code editors with excellent Python support, debugging capabilities, and extensive customization options. Cursor is a fork of VS Code with built-in AI features.

---

## What are VS Code and Cursor?

### VS Code

VS Code is a free, open-source code editor developed by Microsoft. It features:
- **IntelliSense**: Smart code completion
- **Debugging**: Built-in debugger
- **Git Integration**: Version control built-in
- **Extensions**: Huge ecosystem of extensions
- **Terminal**: Integrated terminal
- **Multi-language**: Support for many programming languages

### Cursor

Cursor is a VS Code fork with AI capabilities:
- **All VS Code features**: Everything VS Code can do
- **AI Chat**: Built-in AI assistant (`Cmd+L`)
- **AI Completions**: Context-aware code suggestions
- **AI Edit**: AI-powered code editing (`Cmd+K`)
- **AI Composer**: Multi-file editing with AI

---

## Installation

### VS Code Installation

```bash
# Install via Homebrew
brew install --cask visual-studio-code

# Or download from: https://code.visualstudio.com/
```

### Cursor Installation

```bash
# Install via Homebrew
brew install --cask cursor

# Or download from: https://cursor.sh/
```

### Command Line Access

After installation, enable command line access:

**VS Code:**
1. Open VS Code
2. `Cmd+Shift+P` → "Shell Command: Install 'code' command in PATH"

**Cursor:**
1. Open Cursor
2. `Cmd+Shift+P` → "Shell Command: Install 'cursor' command in PATH"

Now you can use:
```bash
code .          # Open current directory in VS Code
cursor .        # Open current directory in Cursor
```

---

## Essential Extensions

### Python Development

Install these extensions for Python development:

1. **Python** (by Microsoft)
   - Python language support
   - IntelliSense, linting, debugging

2. **Pylance** (by Microsoft)
   - Fast Python language server
   - Type checking, auto-imports

3. **Python Debugger** (by Microsoft)
   - Debugging support for Python

4. **Jupyter** (by Microsoft)
   - Jupyter notebook support
   - Run cells, view outputs

### Code Quality

5. **Black Formatter** (by Microsoft)
   - Code formatting with Black

6. **Pylint** (by Microsoft)
   - Linting with Pylint

7. **Ruff** (by Astral Software)
   - Fast Python linter and formatter

### Git Integration

8. **GitLens** (by GitKraken)
   - Enhanced Git capabilities
   - Blame annotations, commit history

### Other Useful Extensions

9. **Error Lens** (by Alexander)
   - Inline error highlighting

10. **Path Intellisense** (by Christian Kohler)
    - Autocomplete file paths

11. **Bracket Pair Colorizer** (or built-in)
    - Color matching brackets

12. **Material Icon Theme** (by Philipp Kief)
    - File and folder icons

### Installing Extensions

```bash
# Via Command Palette
Cmd+Shift+P → "Extensions: Install Extensions"

# Via Command Line (VS Code)
code --install-extension ms-python.python

# Via Command Line (Cursor)
cursor --install-extension ms-python.python
```

---

## Python Configuration

### Select Python Interpreter

1. `Cmd+Shift+P` → "Python: Select Interpreter"
2. Choose your conda environment: `~/miniconda3/envs/lab-env/bin/python`

Or create `.vscode/settings.json` in your project:

```json
{
    "python.defaultInterpreterPath": "~/miniconda3/envs/lab-env/bin/python"
}
```

### Workspace Settings

Create `.vscode/settings.json` in your project root:

```json
{
    "python.defaultInterpreterPath": "~/miniconda3/envs/lab-env/bin/python",
    "python.formatting.provider": "black",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.ruffEnabled": true,
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    },
    "files.exclude": {
        "**/__pycache__": true,
        "**/*.pyc": true,
        "**/.pytest_cache": true
    },
    "python.analysis.typeCheckingMode": "basic",
    "python.analysis.autoImportCompletions": true
}
```

### User Settings

Access via `Cmd+,` or `Cmd+Shift+P` → "Preferences: Open User Settings (JSON)"

```json
{
    "editor.fontSize": 14,
    "editor.fontFamily": "Menlo, Monaco, 'Courier New', monospace",
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "editor.rulers": [80, 120],
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 1000,
    "editor.minimap.enabled": true,
    "workbench.colorTheme": "Default Dark+",
    "terminal.integrated.fontSize": 12
}
```

---

## Working with Jupyter Notebooks

### Open Notebook

1. Open `.ipynb` file
2. VS Code/Cursor will prompt to select kernel
3. Choose your conda environment

### Run Cells

- **Run cell**: `Shift+Enter`
- **Run cell and move to next**: `Shift+Enter`
- **Run cell and insert below**: `Option+Enter`
- **Run all cells**: `Cmd+Shift+P` → "Notebook: Run All"

### Install Jupyter Extension

The Jupyter extension is usually installed with Python extension. If not:

```bash
code --install-extension ms-toolsai.jupyter
```

---

## Debugging

### Set Breakpoints

1. Click in the gutter (left of line numbers) to set breakpoint
2. Or press `F9` on a line

### Start Debugging

1. `F5` or click Debug icon in sidebar
2. Select "Python: Current File"
3. Or create `launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "justMyCode": true
        },
        {
            "name": "Python: Debug Tests",
            "type": "python",
            "request": "launch",
            "module": "pytest",
            "args": ["-v"],
            "console": "integratedTerminal"
        }
    ]
}
```

### Debug Controls

- **Continue**: `F5`
- **Step Over**: `F10`
- **Step Into**: `F11`
- **Step Out**: `Shift+F11`
- **Restart**: `Cmd+Shift+F5`
- **Stop**: `Shift+F5`

---

## Git Integration

### Basic Git Operations

VS Code/Cursor has built-in Git support:

- **View changes**: Click Source Control icon (or `Ctrl+Shift+G`)
- **Stage files**: Click `+` next to file
- **Commit**: Enter message and press `Cmd+Enter`
- **Push/Pull**: Click `...` menu

### GitLens Features

With GitLens extension:

- **Blame annotations**: See who wrote each line
- **File history**: View file's commit history
- **Compare**: Compare branches, commits, files
- **Commit graph**: Visualize commit history

---

## Terminal Integration

### Open Terminal

- **New terminal**: `` Ctrl+` `` (backtick)
- **Split terminal**: `Cmd+\`
- **Kill terminal**: Trash icon

### Terminal Settings

```json
{
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.fontFamily": "Menlo",
    "terminal.integrated.shell.osx": "/bin/zsh",
    "terminal.integrated.cursorBlinking": true
}
```

---

## Cursor-Specific Features

### AI Chat

- **Open chat**: `Cmd+L`
- **Ask questions**: Type your question
- **Insert code**: Click "Insert at cursor"
- **Explain code**: Select code, then ask in chat

### AI Completions

- **Automatic**: Cursor suggests code as you type
- **Accept**: `Tab` or `Cmd+→`
- **Dismiss**: `Esc`

### AI Edit

- **Select code**: Highlight code you want to edit
- **Open AI edit**: `Cmd+K`
- **Describe changes**: "Add error handling", "Refactor this function"
- **Apply**: Review and accept changes

### AI Composer

- **Open composer**: `Cmd+I`
- **Multi-file editing**: Describe changes across files
- **Generate code**: Create new files or modify existing ones

### Cursor Settings

```json
{
    "cursor.ai.enableAutoCompletions": true,
    "cursor.ai.enableInlineCompletions": true,
    "cursor.ai.model": "gpt-4",
    "cursor.ai.maxTokens": 2000
}
```

---

## Keyboard Shortcuts

### Essential Shortcuts

```
Cmd+P              Quick Open (files)
Cmd+Shift+P        Command Palette
Cmd+B              Toggle sidebar
Cmd+J              Toggle panel
Ctrl+`             Toggle terminal
Cmd+\              Split editor
Cmd+W              Close tab
Cmd+K Cmd+W        Close all tabs

Cmd+/              Toggle line comment
Shift+Option+A     Toggle block comment
Cmd+D              Select next occurrence
Cmd+Shift+L        Select all occurrences

Cmd+F              Find
Cmd+Shift+F        Find in files
Cmd+H              Replace
Cmd+Shift+H        Replace in files

F5                 Start debugging
F9                 Toggle breakpoint
F10                Step over
F11                Step into
```

### Navigation

```
Cmd+P              Go to file
Cmd+Shift+O        Go to symbol in file
Ctrl+G             Go to line
Cmd+T              Go to symbol in workspace
Cmd+Shift+P        Command Palette
```

### Editing

```
Cmd+X              Cut line
Cmd+C              Copy line
Option+↑/↓         Move line up/down
Shift+Option+↑/↓   Copy line up/down
Cmd+Enter          Insert line below
Cmd+Shift+Enter    Insert line above
Cmd+]              Indent
Cmd+[              Outdent
```

---

## Project Setup

### Recommended Project Structure

```
my-project/
├── .vscode/
│   ├── settings.json
│   └── launch.json
├── src/
│   └── main.py
├── tests/
│   └── test_main.py
├── notebooks/
│   └── analysis.ipynb
├── .gitignore
├── requirements.txt
└── README.md
```

### Multi-root Workspaces

Open multiple folders:

1. `File → Add Folder to Workspace`
2. Save workspace: `File → Save Workspace As...`
3. Open workspace: `File → Open Workspace`

---

## Best Practices

### 1. Use Workspace Settings

Create `.vscode/settings.json` in each project for project-specific settings.

### 2. Configure Python Interpreter Per Project

Set Python interpreter in workspace settings, not globally.

### 3. Use Format on Save

Enable `editor.formatOnSave` to keep code consistently formatted.

### 4. Organize Extensions

- Install only what you need
- Disable unused extensions
- Keep extensions updated

### 5. Use Tasks

Create tasks for common operations (`.vscode/tasks.json`):

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Run Tests",
            "type": "shell",
            "command": "pytest",
            "group": "test"
        },
        {
            "label": "Format Code",
            "type": "shell",
            "command": "black .",
            "group": "build"
        }
    ]
}
```

Run tasks: `Cmd+Shift+P` → "Tasks: Run Task"

### 6. Use Snippets

Create custom code snippets:

1. `Cmd+Shift+P` → "Preferences: Configure User Snippets"
2. Select "Python"
3. Add your snippets

Example:
```json
{
    "Print to console": {
        "prefix": "print",
        "body": [
            "print(f\"$1: {$1}\")"
        ],
        "description": "Print with f-string"
    }
}
```

---

## Troubleshooting

### Issue: Python Interpreter Not Found

**Problem**: VS Code/Cursor can't find Python

**Solution**:
1. `Cmd+Shift+P` → "Python: Select Interpreter"
2. Manually enter path: `~/miniconda3/envs/lab-env/bin/python`
3. Or add to PATH in settings

### Issue: Extensions Not Working

**Problem**: Extension installed but not working

**Solution**:
1. Reload window: `Cmd+Shift+P` → "Developer: Reload Window"
2. Check extension output: View → Output → Select extension
3. Reinstall extension

### Issue: Formatting Not Working

**Problem**: Code not formatting on save

**Solution**:
```json
{
    "python.formatting.provider": "black",
    "editor.formatOnSave": true,
    "[python]": {
        "editor.defaultFormatter": "ms-python.black-formatter"
    }
}
```

### Issue: IntelliSense Not Working

**Problem**: No code completion or errors

**Solution**:
1. Select correct Python interpreter
2. `Cmd+Shift+P` → "Python: Restart Language Server"
3. Check Pylance is installed and enabled

### Issue: Terminal Not Opening

**Problem**: Terminal won't open

**Solution**:
1. Check shell path in settings
2. `` Ctrl+` `` to toggle terminal
3. `Cmd+Shift+P` → "Terminal: Create New Terminal"

---

## Quick Reference

### Essential Settings

```json
{
    "python.defaultInterpreterPath": "~/miniconda3/envs/lab-env/bin/python",
    "python.formatting.provider": "black",
    "editor.formatOnSave": true,
    "files.autoSave": "afterDelay"
}
```

### Essential Extensions

- Python (Microsoft)
- Pylance (Microsoft)
- Jupyter (Microsoft)
- Black Formatter (Microsoft)
- GitLens (GitKraken)

### Essential Shortcuts

```
Cmd+P              Quick Open
Cmd+Shift+P        Command Palette
Cmd+,              Settings
Ctrl+`             Terminal
F5                 Debug
Cmd+K Cmd+S        Keyboard Shortcuts
```

---

## Related Guides

- **[Python Development](../development-environment.md)** - Set up Python environment
- **[Conda Guide](conda.md)** - Manage Python environments
- **[Jupyter Guide](jupyter.md)** - Work with Jupyter notebooks
- **[Git Guide](git.md)** - Version control integration
- **[Development Tools Overview](index.md)** - All development tools guides

---

*Last updated: {{ git_revision_date_localized }}*

