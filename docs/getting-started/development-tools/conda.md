# Conda Guide
updated 11/23/2025 by JDY

Conda is a tool that makes handling your Python (and other language) environments much easier, especially if you're new to programming or scientific computing. It helps you install packages and set up isolated environments—a bit like giving every project its own clean workspace. This means you don't have to worry about one project messing up the packages in another, and you can easily install tricky libraries used in data science.

---

## What is Conda, and Why should you use it?

Conda is an open-source program for managing packages and environments on Windows, macOS, and Linux. For beginners, it's useful because it simplifies many common headaches in Python:

- **Install packages and dependencies automatically**: You don’t have to track down and install everything by hand.
- **Create isolated environments**: Each project gets its own space, so you can try things without breaking other projects.
- **Switch between different Python versions easily**: If you need an older or newer Python for a specific project, it’s no problem.
- **Install binary packages (not just Python)**: Many data science libraries rely on system-level tools—conda handles them for you.
- **Works with pip and other package managers**: You can use your favorite tools together.

**In short:** Conda makes life easier for beginners by taking care of most of the tricky setup so you can focus on learning, coding, and running your projects.

---

## Installation



### Install Miniconda via Homebrew

You can also install Miniconda using Homebrew, which is often easier than downloading the installer manually:

```bash
# Install Miniconda (Apple Silicon or Intel)
brew install --cask miniconda

# After installation, add conda to your PATH:
# This command sets up conda for your shell (zsh shown here)
echo 'export PATH="/opt/homebrew/Caskroom/miniconda/base/bin:$PATH"' >> ~/.zshrc

# Initialize conda in your shell
conda init zsh   # or bash, fish, etc.

# Restart your terminal or source your shell rc file:
source ~/.zshrc

```

> **Tip:** For more about `zsh` and your configuration file (`.zshrc`), see:
> - [Oh My Zsh](https://ohmyz.sh/) (for managing your `zsh` shell)
> - [What is .zshrc?](https://linuxize.com/post/zshrc-file/) (explains the `.zshrc` file)

> **Note:** On Intel Macs, your path may be `/usr/local/Caskroom/miniconda/base/bin` rather than `/opt/homebrew/Caskroom/miniconda/base/bin`.

For more details, see the [Homebrew Miniconda cask documentation](https://formulae.brew.sh/cask/miniconda).

### Install Miniconda via Manual Download

Miniconda is a minimal installer that includes conda, Python, and a few essential packages:

```bash
# Download Miniconda for macOS (Apple Silicon)
cd ~/Downloads
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh

# Download Miniconda for macOS (Intel)
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh

# Run installer
bash Miniconda3-latest-MacOSX-arm64.sh  # or x86_64.sh for Intel

# Follow prompts:
# - Press Enter to review license
# - Type 'yes' to accept
# - Press Enter to confirm installation location
# - Type 'yes' to initialize conda
```

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

---

## Basic Usage

### Creating Environments

```bash
# Create environment with Python 3.10
conda create -n myenv python=3.10

# Create environment with specific packages
conda create -n myenv python=3.10 numpy pandas matplotlib

# Create environment from file
conda env create -f environment.yml
```

### Activating and Deactivating

```bash
# Activate environment
conda activate myenv

# Deactivate environment
conda deactivate

# Activate base environment
conda activate base
```

### Installing Packages

```bash
# Install a package
conda install numpy

# Install multiple packages
conda install numpy pandas matplotlib

# Install from specific channel
conda install -c conda-forge package-name

# Install specific version
conda install numpy=1.24.0
```

### Listing and Searching

```bash
# List all environments
conda env list
# or
conda info --envs

# List packages in current environment
conda list

# List packages in specific environment
conda list -n myenv

# Search for packages
conda search numpy

# Search in specific channel
conda search -c conda-forge package-name
```

### Removing Environments and Packages

```bash
# Remove a package
conda remove numpy

# Remove environment
conda env remove -n myenv

# Remove all unused packages
conda clean --all
```

---

## Best Practices

### 1. Use Environments for Each Project

**Always create a separate environment for each project:**

```bash
# Good: Project-specific environment
conda create -n project1 python=3.10
conda activate project1
conda install project-dependencies

# Bad: Installing everything in base
conda install everything
```

### 2. Use Environment Files

Create `environment.yml` files for reproducible environments:

```yaml
name: my-project
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - python=3.10
  - numpy>=1.20.0
  - pandas>=1.3.0
  - matplotlib>=3.4.0
  - pip
  - pip:
    - some-pip-only-package
```

**Usage:**
```bash
# Create from file
conda env create -f environment.yml

# Update existing environment
conda env update -f environment.yml --prune

# Export current environment
conda env export > environment.yml

# Export without build numbers (more portable)
conda env export --no-builds > environment.yml
```

### 3. Use Channels Wisely

Channels are repositories where conda looks for packages:

```bash
# Add channels (order matters - first checked first)
conda config --add channels conda-forge
conda config --add channels bioconda

# List channels
conda config --show channels

# Install from specific channel
conda install -c conda-forge package-name

# Set channel priority
conda config --set channel_priority strict
```

**Recommended channel order:**
1. `conda-forge` - Community-maintained packages
2. `bioconda` - Bioinformatics packages
3. `defaults` - Anaconda's default channel

### 4. Keep Base Environment Clean

**Don't install packages in base environment:**

```bash
# Good: Create new environment
conda create -n myproject python=3.10
conda activate myproject

# Bad: Installing in base
conda activate base
conda install packages  # Don't do this!
```

### 5. Use Mamba for Faster Installs

Mamba is a faster drop-in replacement for conda:

```bash
# Install mamba
conda install mamba -n base -c conda-forge

# Use mamba instead of conda
mamba create -n myenv python=3.10
mamba install numpy pandas
mamba env update -f environment.yml
```

### 6. Regular Maintenance

```bash
# Update conda
conda update conda

# Update all packages in environment
conda update --all

# Clean cache and unused packages
conda clean --all

# Remove unused environments
conda env remove -n old-env
```

---

## Working with pip

### When to Use pip vs conda

**Use conda for:**
- ✅ Packages available in conda (numpy, pandas, scipy, etc.)
- ✅ Packages with C/C++ dependencies
- ✅ System-level dependencies

**Use pip for:**
- ✅ Packages only available on PyPI
- ✅ Development versions
- ✅ Packages not in conda channels

### Best Practice: Install conda packages first, then pip

```bash
# Create environment
conda create -n myenv python=3.10

# Install conda packages first
conda install numpy pandas matplotlib

# Then install pip-only packages
pip install some-pip-only-package
```

### Including pip packages in environment.yml

```yaml
name: my-project
dependencies:
  - python=3.10
  - numpy
  - pip
  - pip:
    - package-only-on-pypi
    - another-pip-package
```

---

## Common Workflows

### Workflow 1: New Project Setup

```bash
# 1. Create environment
conda create -n myproject python=3.10

# 2. Activate
conda activate myproject

# 3. Install packages
conda install numpy pandas matplotlib jupyter

# 4. Install pip-only packages
pip install some-package

# 5. Export environment
conda env export > environment.yml

# 6. Add to git
git add environment.yml
```

### Workflow 2: Sharing Environment

```bash
# Export environment
conda env export --no-builds > environment.yml

# Share file with team

# Others can recreate:
conda env create -f environment.yml
conda activate myproject
```

### Workflow 3: Updating Environment

```bash
# Update specific package
conda update numpy

# Update all packages
conda update --all

# Update from environment file
conda env update -f environment.yml --prune
```

### Workflow 4: Multiple Python Versions

```bash
# Create environments with different Python versions
conda create -n py39 python=3.9
conda create -n py310 python=3.10
conda create -n py311 python=3.11

# Switch between them
conda activate py39
# work with Python 3.9

conda activate py310
# work with Python 3.10
```

---

## Advanced Usage

### Cloning Environments

```bash
# Clone an environment
conda create --name newenv --clone oldenv

# Useful for testing updates
conda create --name test-update --clone production
conda activate test-update
conda update --all
```

### Managing Channels

```bash
# Show channel configuration
conda config --show channels

# Add channel
conda config --add channels conda-forge

# Remove channel
conda config --remove channels channel-name

# Set channel priority
conda config --set channel_priority strict  # Prefer higher priority
conda config --set channel_priority flexible  # Try all channels
```

### Environment Variables

```bash
# Set environment variable in environment
conda env config vars set MY_VAR=value -n myenv

# List environment variables
conda env config vars list -n myenv

# Unset variable
conda env config vars unset MY_VAR -n myenv
```

### Installing from Git

```bash
# Install package from git
pip install git+https://github.com/user/repo.git

# Install editable (development mode)
pip install -e git+https://github.com/user/repo.git#egg=package
```

---

## Troubleshooting

### Issue: Environment Not Activating

**Problem**: `conda activate` doesn't work

**Solution**:
```bash
# Initialize conda
conda init zsh  # or bash

# Restart terminal or source
source ~/.zshrc
```

### Issue: Package Not Found

**Problem**: `PackagesNotFoundError`

**Solution**:
```bash
# Search for package
conda search package-name

# Try different channels
conda install -c conda-forge package-name
conda install -c bioconda package-name

# Use pip if not in conda
pip install package-name
```

### Issue: Dependency Conflicts

**Problem**: Conflicting package versions

**Solution**:
```bash
# Let conda solve dependencies
conda install package-name --solver=libmamba

# Or use mamba (faster solver)
mamba install package-name

# Create fresh environment
conda create -n fresh python=3.10 package-name
```

### Issue: Slow Installation

**Problem**: Conda is slow

**Solution**:
```bash
# Use mamba (much faster)
conda install mamba -n base -c conda-forge
mamba install packages

# Use conda-forge channel (often faster)
conda install -c conda-forge package-name
```

### Issue: Environment Takes Too Much Space

**Problem**: Environments are large

**Solution**:
```bash
# Clean unused packages
conda clean --all

# Remove old environments
conda env remove -n old-env

# Use miniconda instead of anaconda
```

---

## Conda vs Other Tools

### Conda vs pip

| Feature | Conda | pip |
|---------|-------|-----|
| Python packages | ✅ | ✅ |
| Non-Python dependencies | ✅ | ❌ |
| Environment management | ✅ | ⚠️ (venv) |
| Binary packages | ✅ | ⚠️ (wheels) |
| Dependency solving | ✅ | ⚠️ (basic) |

### Conda vs venv

| Feature | Conda | venv |
|---------|-------|------|
| Multiple Python versions | ✅ | ❌ |
| Non-Python packages | ✅ | ❌ |
| Cross-platform | ✅ | ✅ |
| Lightweight | ⚠️ | ✅ |

**Best Practice**: Use conda for scientific computing, use venv for simple Python projects.

---

## Quick Reference

```bash
# Environments
conda create -n envname python=3.10
conda activate envname
conda deactivate
conda env list
conda env remove -n envname

# Packages
conda install package
conda install -c conda-forge package
conda list
conda search package
conda update package
conda remove package

# Environment files
conda env export > environment.yml
conda env create -f environment.yml
conda env update -f environment.yml

# Maintenance
conda update conda
conda update --all
conda clean --all
```

---

## Related Guides

- **[Homebrew Guide](homebrew.md)** - System package management
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Development Environment Setup](../development-environment.md)** - Complete macOS setup guide
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

