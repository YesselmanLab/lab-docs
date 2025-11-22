# Installation Guide

This guide will help you set up your environment for working in the lab.

!!! tip "New to macOS Development?"
    If you're setting up a development environment on macOS for the first time, see the [Development Environment Setup Guide](development-environment.md) for detailed instructions on installing Homebrew, conda, pip, and configuring IDEs like VS Code or Cursor.

## Prerequisites

Before you begin, ensure you have:

- Python 3.8 or higher
- pip (Python package manager)
- Git
- [Add other prerequisites specific to your lab]

## Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/lab-repo.git
cd lab-repo
```

## Step 2: Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

## Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

## Step 4: Configuration

[Add lab-specific configuration steps]

## Verification

To verify your installation:

```bash
# Add verification commands
python --version
```

## Troubleshooting

### Common Issues

**Issue**: Python version not found
- **Solution**: Ensure Python 3.8+ is installed and in your PATH

**Issue**: pip not found
- **Solution**: Install pip or use `python -m pip` instead

[Add more troubleshooting tips as needed]

## Related Guides

- **[Development Environment Setup](development-environment.md)** - Complete macOS setup with Homebrew, conda, and IDEs
- **[Command Line Guide](command-line-guide.md)** - Learn terminal commands if you're new to the command line
- **[Quick Start Guide](quick-start.md)** - Next steps after installation
- **[Lab Guide / FAQ](faq.md)** - Lab rules and policies

## Next Steps

Once installation is complete, proceed to the [Quick Start Guide](quick-start.md).

