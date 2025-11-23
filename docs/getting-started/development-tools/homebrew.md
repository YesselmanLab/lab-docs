# Homebrew Guide

Homebrew is the missing package manager for macOS (and Linux). It makes it easy to install and manage software that Apple (or your Linux system) doesn't include.

---

## What is Homebrew?

Homebrew installs packages to their own directory and then symlinks their files into `/opt/homebrew` (Apple Silicon) or `/usr/local` (Intel). This means you can install packages without needing `sudo` and without interfering with system files.

---

## Installation

### macOS Installation

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the on-screen instructions. After installation, you may need to add Homebrew to your PATH:

#### For Apple Silicon Macs (M1/M2/M3)

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/opt/homebrew/bin/brew shellenv)"
```

#### For Intel Macs

```bash
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zshrc
eval "$(/usr/local/bin/brew shellenv)"
```

### Verify Installation

```bash
brew --version
brew doctor
```

---

## Basic Usage

### Installing Packages

```bash
# Install a package
brew install git

# Install multiple packages at once
brew install git python node

# Install a cask (GUI application)
brew install --cask visual-studio-code
```

### Updating Homebrew

```bash
# Update Homebrew itself
brew update

# Update all installed packages
brew upgrade

# Update a specific package
brew upgrade git

# See what would be updated (without updating)
brew outdated
```

### Searching for Packages

```bash
# Search for packages
brew search python

# Search for casks (GUI apps)
brew search --casks code
```

### Listing Installed Packages

```bash
# List all installed packages
brew list

# List only top-level packages (not dependencies)
brew leaves

# Show package information
brew info git
```

### Uninstalling Packages

```bash
# Uninstall a package
brew uninstall git

# Uninstall and remove dependencies
brew uninstall --force git

# Remove all unused dependencies
brew autoremove
```

---

## Best Practices

### 1. Keep Homebrew Updated

Regularly update Homebrew and your packages:

```bash
# Weekly maintenance routine
brew update
brew upgrade
brew cleanup
```

You can automate this with a cron job or just remember to run it weekly.

### 2. Use Brewfiles for Reproducible Setups

Create a `Brewfile` to document and share your setup:

```bash
# Generate Brewfile from current installations
brew bundle dump

# Install from Brewfile
brew bundle install

# Check if Brewfile is satisfied
brew bundle check
```

Example `Brewfile`:

```
# Homebrew packages
brew "git"
brew "python"
brew "node"
brew "tree"
brew "htop"
brew "wget"

# Homebrew casks (GUI apps)
cask "visual-studio-code"
cask "cursor"
cask "google-chrome"
```

### 3. Organize with Taps

Taps are additional repositories of Homebrew formulae:

```bash
# Add a tap
brew tap homebrew/cask-versions

# List installed taps
brew tap

# Remove a tap
brew untap homebrew/cask-versions
```

### 4. Use Services for Background Processes

Homebrew can manage system services:

```bash
# Install a service
brew install postgresql

# Start a service
brew services start postgresql

# Stop a service
brew services stop postgresql

# List all services
brew services list

# Restart a service
brew services restart postgresql
```

### 5. Clean Up Regularly

```bash
# Remove old versions and cache
brew cleanup

# See what would be cleaned
brew cleanup -n

# Clean up specific package
brew cleanup git
```

### 6. Fix Common Issues

```bash
# Check for common issues
brew doctor

# Fix permissions issues
sudo chown -R $(whoami) /opt/homebrew  # Apple Silicon
# or
sudo chown -R $(whoami) /usr/local      # Intel

# Reinstall a broken package
brew reinstall git
```

---

## Essential Packages for Development

### Version Control

```bash
brew install git
brew install git-lfs  # Git Large File Storage
```

### Programming Languages

```bash
# Python (though conda is often better for Python)
brew install python

# Node.js
brew install node

# Go
brew install go

# Rust
brew install rust
```

### Development Tools

```bash
# Terminal utilities
brew install tree          # Directory tree visualization
brew install htop          # Process monitor
brew install wget          # File downloading
brew install jq             # JSON processor
brew install bat            # Better cat
brew install fd             # Better find
brew install ripgrep        # Better grep
brew install fzf            # Fuzzy finder
brew install exa             # Better ls
brew install tldr            # Simplified man pages
```

### Text Editors and IDEs

```bash
# VS Code
brew install --cask visual-studio-code

# Cursor
brew install --cask cursor

# Vim (enhanced)
brew install vim

# Neovim
brew install neovim
```

### Database Tools

```bash
# PostgreSQL
brew install postgresql

# MySQL
brew install mysql

# Redis
brew install redis
```

---

## Advanced Usage

### Installing Specific Versions

```bash
# Search for versions
brew search python@

# Install specific version
brew install python@3.11

# Switch between versions
brew unlink python@3.10
brew link python@3.11
```

### Creating Custom Formulae

For packages not in Homebrew, you can create custom formulae:

```bash
# Create a local tap
brew tap-new username/tap-name

# Create a formula
brew create https://example.com/package.tar.gz
```

### Pinning Packages

Prevent packages from being upgraded:

```bash
# Pin a package
brew pin git

# Unpin a package
brew unpin git

# List pinned packages
brew list --pinned
```

### Using Homebrew in Scripts

```bash
#!/bin/bash
# Check if package is installed
if ! brew list git &>/dev/null; then
    brew install git
fi
```

---

## Troubleshooting

### Issue: Command Not Found

**Problem**: `brew: command not found`

**Solution**:
```bash
# Add to PATH (Apple Silicon)
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
source ~/.zshrc

# Or (Intel)
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zshrc
source ~/.zshrc
```

### Issue: Permission Denied

**Problem**: Permission errors when installing

**Solution**:
```bash
# Fix ownership (Apple Silicon)
sudo chown -R $(whoami) /opt/homebrew

# Fix ownership (Intel)
sudo chown -R $(whoami) /usr/local
```

### Issue: Outdated Formulae

**Problem**: Package not found or outdated

**Solution**:
```bash
# Update Homebrew
brew update

# Update specific tap
brew update --force
```

### Issue: Broken Installation

**Problem**: Package installed but not working

**Solution**:
```bash
# Reinstall
brew reinstall package-name

# Or uninstall and reinstall
brew uninstall package-name
brew install package-name
```

### Issue: Conflicting Versions

**Problem**: Multiple versions of same package

**Solution**:
```bash
# List all versions
brew list --versions python

# Switch versions
brew unlink python@3.10
brew link python@3.11
```

---

## When to Use Homebrew vs Other Package Managers

### Use Homebrew For:
- ✅ System-level tools (git, wget, tree, etc.)
- ✅ GUI applications (VS Code, browsers, etc.)
- ✅ Development tools not language-specific
- ✅ System services (PostgreSQL, Redis, etc.)

### Don't Use Homebrew For:
- ❌ Python packages (use pip/conda instead)
- ❌ Node.js packages (use npm/yarn instead)
- ❌ Language-specific packages (use language package managers)

### Best Practice:
Use Homebrew for **system tools** and **applications**, but use language-specific package managers (pip, npm, etc.) for **libraries and frameworks**.

---

## Quick Reference

```bash
# Installation
brew install package
brew install --cask app-name

# Updates
brew update
brew upgrade
brew outdated

# Information
brew list
brew info package
brew search term

# Maintenance
brew cleanup
brew doctor
brew autoremove

# Services
brew services list
brew services start service-name

# Brewfiles
brew bundle dump
brew bundle install
```

---

## Related Guides

- **[Conda Guide](conda.md)** - Python package and environment management
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Development Environment Setup](../development-environment.md)** - Complete macOS setup guide
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

