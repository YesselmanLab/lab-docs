# Setting Up a Development Environment on macOS

This guide will walk you through setting up a complete Python development environment on macOS using Homebrew, conda, and pip, along with configuring IDEs like VS Code or Cursor.

---

## Prerequisites

- macOS (any recent version)
- Administrator access (for installing Homebrew)
- Terminal access

---

## Step 1: Install Homebrew

Homebrew is a package manager for macOS that makes it easy to install development tools.

!!! tip "Detailed Homebrew Guide"
    For comprehensive Homebrew usage, best practices, and advanced techniques, see the [Homebrew Guide](development-tools/homebrew.md).

### Installation

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the on-screen instructions. After installation, you may need to add Homebrew to your PATH:

```bash
# For Apple Silicon Macs (M1/M2/M3)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/opt/homebrew/bin/brew shellenv)"

# For Intel Macs
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/usr/local/bin/brew shellenv)"
```

### Verify Installation

```bash
brew --version
```

### Update Homebrew

```bash
brew update
```

---

## Step 2: Install Python via Homebrew

While macOS comes with Python, it's better to install a fresh version via Homebrew:

```bash
# Install Python (latest version)
brew install python

# Verify installation
python3 --version
which python3
```

---

## Step 3: Install Miniconda (Recommended)

Miniconda is a minimal installer for conda. It's lighter than Anaconda and gives you full control.

!!! tip "Detailed Conda Guide"
    For comprehensive conda usage, best practices, environment management, and advanced techniques, see the [Conda Guide](development-tools/conda.md).

### Installation

```bash
# Download Miniconda installer for macOS
cd ~/Downloads
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh

# For Apple Silicon Macs, use:
# curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh

# Run the installer
bash Miniconda3-latest-MacOSX-x86_64.sh
```

Follow the prompts:
- Press Enter to review the license
- Type `yes` to accept
- Press Enter to confirm installation location
- Type `yes` to initialize conda

### Initialize Conda

After installation, restart your terminal or run:

```bash
source ~/.zshrc  # or ~/.bash_profile for bash
```

### Verify Installation

```bash
conda --version
conda info
```

### Update Conda

```bash
conda update conda
```

---

## Step 4: Set Up a Conda Environment

Create an isolated environment for your project:

```bash
# Create a new environment with Python 3.10
conda create -n lab-env python=3.10

# Activate the environment
conda activate lab-env

# Verify Python version
python --version
which python
```

### Managing Conda Environments

```bash
# List all environments
conda env list

# Deactivate current environment
conda deactivate

# Remove an environment (when you're done)
conda env remove -n lab-env
```

---

## Step 5: Install Packages with pip

Once your conda environment is active, use pip to install Python packages:

```bash
# Make sure you're in your conda environment
conda activate lab-env

# Upgrade pip first
pip install --upgrade pip

# Install packages
pip install numpy pandas matplotlib

# Install from requirements.txt
pip install -r requirements.txt

# Install in development mode (for local packages)
pip install -e .
```

### Virtual Environments (Alternative to Conda)

If you prefer using Python's built-in venv instead of conda:

```bash
# Create a virtual environment
python3 -m venv venv

# Activate it
source venv/bin/activate

# Install packages
pip install --upgrade pip
pip install numpy pandas matplotlib

# Deactivate
deactivate
```

---

## Step 6: Install Development Tools

### Git

```bash
# Install Git via Homebrew
brew install git

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Verify
git --version
```

### Additional Useful Tools

```bash
# Install useful development tools
brew install tree          # Directory tree visualization
brew install wget          # File downloading
brew install htop          # Process monitoring
brew install jq            # JSON processor
```

---

## Step 7: Set Up VS Code

### Installation

```bash
# Install VS Code via Homebrew
brew install --cask visual-studio-code

# Or download from: https://code.visualstudio.com/
```

### Essential Extensions

Install these extensions in VS Code:

1. **Python** (by Microsoft) - Python language support
2. **Pylance** (by Microsoft) - Fast Python language server
3. **Python Debugger** (by Microsoft) - Debugging support
4. **Jupyter** (by Microsoft) - Jupyter notebook support
5. **GitLens** - Enhanced Git capabilities
6. **Black Formatter** - Code formatting
7. **Pylint** - Linting support

### Configure VS Code for Python

1. Open VS Code
2. Press `Cmd+Shift+P` to open command palette
3. Type "Python: Select Interpreter"
4. Choose your conda environment: `~/miniconda3/envs/lab-env/bin/python`

### VS Code Settings

Create or edit `~/.vscode/settings.json`:

```json
{
    "python.defaultInterpreterPath": "~/miniconda3/envs/lab-env/bin/python",
    "python.formatting.provider": "black",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    },
    "files.exclude": {
        "**/__pycache__": true,
        "**/*.pyc": true
    }
}
```

### Working with Jupyter Notebooks in VS Code

1. Open a `.ipynb` file
2. VS Code will prompt you to select a kernel
3. Choose your conda environment: `Python 3.10.x ('lab-env': conda)`
4. You can now run cells with `Shift+Enter`

---

## Step 8: Set Up Cursor

Cursor is a VS Code fork with AI features. Setup is similar to VS Code.

### Installation

```bash
# Install Cursor via Homebrew
brew install --cask cursor

# Or download from: https://cursor.sh/
```

### Configure Cursor for Python

1. Open Cursor
2. Install the same extensions as VS Code (Python, Pylance, Jupyter, etc.)
3. Select your Python interpreter: `Cmd+Shift+P` → "Python: Select Interpreter"
4. Choose: `~/miniconda3/envs/lab-env/bin/python`

### Cursor-Specific Features

- **AI Chat**: `Cmd+L` to open AI chat
- **AI Completions**: Automatic code suggestions
- **AI Edit**: Select code and use `Cmd+K` for AI-powered edits

### Cursor Settings

Similar to VS Code, create settings in Cursor:

```json
{
    "python.defaultInterpreterPath": "~/miniconda3/envs/lab-env/bin/python",
    "python.formatting.provider": "black",
    "python.linting.enabled": true,
    "editor.formatOnSave": true
}
```

---

## Step 9: Configure Your Shell

### Zsh Configuration (Default on macOS)

Edit `~/.zshrc`:

```bash
# Add conda to PATH
export PATH="$HOME/miniconda3/bin:$PATH"

# Initialize conda
. "$HOME/miniconda3/etc/profile.d/conda.sh"

# Auto-activate conda environment (optional)
# conda activate lab-env

# Aliases for common commands
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'

# Python aliases
alias python='python3'
alias pip='pip3'
```

Reload your shell:

```bash
source ~/.zshrc
```

---

## Step 10: Project Setup Example

Here's how to set up a typical lab project:

```bash
# 1. Create project directory
mkdir my-lab-project
cd my-lab-project

# 2. Create conda environment
conda create -n my-project python=3.10
conda activate my-project

# 3. Create requirements.txt
cat > requirements.txt << EOF
numpy>=1.20.0
pandas>=1.3.0
matplotlib>=3.4.0
scipy>=1.7.0
jupyter
EOF

# 4. Install dependencies
pip install -r requirements.txt

# 5. Initialize Git
git init
echo "venv/" >> .gitignore
echo "__pycache__/" >> .gitignore
echo "*.pyc" >> .gitignore

# 6. Create project structure
mkdir src
mkdir notebooks
mkdir tests

# 7. Open in VS Code or Cursor
code .  # For VS Code
# or
cursor .  # For Cursor
```

---

## Common Workflows

### Daily Development Workflow

```bash
# 1. Activate your environment
conda activate lab-env

# 2. Navigate to project
cd ~/projects/my-project

# 3. Open in IDE
code .  # or cursor .

# 4. Work on your code...

# 5. Install new packages as needed
pip install new-package

# 6. Update requirements.txt
pip freeze > requirements.txt

# 7. Deactivate when done (optional)
conda deactivate
```

### Working with Jupyter Notebooks

```bash
# Activate environment
conda activate lab-env

# Install Jupyter if not already installed
pip install jupyter

# Launch Jupyter
jupyter notebook
# or
jupyter lab

# Or use VS Code/Cursor's built-in Jupyter support
```

### Managing Multiple Projects

```bash
# Create separate environments for each project
conda create -n project1 python=3.10
conda create -n project2 python=3.11

# Switch between projects
conda activate project1
# work on project1...

conda deactivate
conda activate project2
# work on project2...
```

---

## Troubleshooting

### Issue: Command Not Found

**Problem**: `conda: command not found`

**Solution**:
```bash
# Add conda to PATH
export PATH="$HOME/miniconda3/bin:$PATH"
source ~/.zshrc
```

### Issue: Wrong Python Version

**Problem**: VS Code/Cursor using wrong Python interpreter

**Solution**:
1. `Cmd+Shift+P` → "Python: Select Interpreter"
2. Choose the correct conda environment
3. Verify: `which python` should show your conda environment path

### Issue: Packages Not Found

**Problem**: Import errors even though package is installed

**Solution**:
```bash
# Verify you're in the correct environment
conda activate lab-env
which python
which pip

# Reinstall package
pip install --force-reinstall package-name

# Check if package is installed
pip list | grep package-name
```

### Issue: Homebrew Permission Errors

**Problem**: Permission denied when using Homebrew

**Solution**:
```bash
# Fix Homebrew permissions
sudo chown -R $(whoami) /opt/homebrew  # Apple Silicon
# or
sudo chown -R $(whoami) /usr/local  # Intel
```

### Issue: Conda Environment Not Activating

**Problem**: `conda activate` doesn't work

**Solution**:
```bash
# Initialize conda in your shell
conda init zsh  # or bash
source ~/.zshrc
```

---

## Best Practices

### 1. Always Use Virtual Environments

Never install packages globally. Always use conda environments or venv:

```bash
# Good
conda activate lab-env
pip install package

# Bad
pip install package  # without activating environment
```

### 2. Keep Requirements Files Updated

```bash
# Regularly update requirements.txt
pip freeze > requirements.txt

# Or use pip-tools for better dependency management
pip install pip-tools
pip-compile requirements.in
```

### 3. Use Environment Files

For conda, use `environment.yml`:

```yaml
name: lab-env
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - python=3.10
  - pip
  - pip:
    - numpy
    - pandas
    - matplotlib
```

Create environment:
```bash
conda env create -f environment.yml
```

### 4. Document Your Setup

Keep a `SETUP.md` or `README.md` in your project with:
- Required Python version
- How to create the environment
- How to install dependencies
- Any special configuration needed

### 5. Use Version Control

Always use Git for your projects:

```bash
# Initialize Git
git init

# Create .gitignore
echo "venv/" >> .gitignore
echo "__pycache__/" >> .gitignore
echo "*.pyc" >> .gitignore
echo ".vscode/" >> .gitignore  # Optional: exclude IDE settings
```

---

## Quick Reference

### Conda Commands

```bash
conda create -n env-name python=3.10    # Create environment
conda activate env-name                # Activate environment
conda deactivate                       # Deactivate
conda env list                         # List environments
conda env remove -n env-name           # Remove environment
conda install package-name             # Install package
conda list                             # List installed packages
conda update conda                     # Update conda
```

### pip Commands

```bash
pip install package-name               # Install package
pip install -r requirements.txt        # Install from file
pip uninstall package-name            # Uninstall package
pip list                               # List installed packages
pip freeze > requirements.txt          # Save package list
pip install --upgrade package-name     # Upgrade package
```

### Homebrew Commands

```bash
brew install package-name              # Install package
brew uninstall package-name           # Uninstall
brew update                            # Update Homebrew
brew upgrade                           # Upgrade packages
brew list                              # List installed packages
brew search term                       # Search for packages
```

---

## Related Guides

Continue with these Getting Started guides:

- **[Development Tools](development-tools/index.md)** - Detailed guides for [Homebrew](development-tools/homebrew.md) and [Conda](development-tools/conda.md)
- **[Command Line Guide](command-line-guide.md)** - Learn terminal commands (essential after setting up your environment)
- **[Installation Guide](installation.md)** - Install lab-specific software and dependencies
- **[Lab Guide / FAQ](faq.md)** - Lab rules, policies, and expectations
- **[Quick Start Guide](quick-start.md)** - Get started with immediate tasks
- **[Getting Started Overview](overview.md)** - Return to the main getting started page

## Additional Resources

- **Homebrew**: https://brew.sh/
- **Conda Documentation**: https://docs.conda.io/
- **VS Code Python Guide**: https://code.visualstudio.com/docs/languages/python
- **Cursor Documentation**: https://cursor.sh/docs
- **Python Virtual Environments**: https://docs.python.org/3/tutorial/venv.html

---

*Last updated: {{ git_revision_date_localized }}*

