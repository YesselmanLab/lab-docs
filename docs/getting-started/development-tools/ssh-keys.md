# SSH Keys Guide

SSH (Secure Shell) keys provide a secure way to authenticate to remote servers without entering passwords. They're essential for accessing clusters, GitHub, GitLab, and other remote services.

---

## What are SSH Keys?

SSH keys are a pair of cryptographic keys:
- **Private key**: Stored on your computer (keep secret!)
- **Public key**: Shared with remote servers (safe to share)

Benefits:
- **Passwordless authentication**: No need to type passwords
- **More secure**: Cryptographic keys are harder to crack
- **Convenient**: Once set up, seamless access
- **Required**: Many services (GitHub, clusters) require SSH keys

---

## Generate SSH Keys

### Basic Key Generation

```bash
# Generate SSH key pair
ssh-keygen -t ed25519 -C "your.email@example.com"

# For older systems (if ed25519 not supported)
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```

**During generation, you'll be asked:**
1. **File location**: Press Enter for default (`~/.ssh/id_ed25519`)
2. **Passphrase**: Enter a passphrase (recommended) or press Enter for none
3. **Confirm passphrase**: Re-enter if you set one

### Key Files Created

```bash
# Private key (NEVER share this!)
~/.ssh/id_ed25519

# Public key (safe to share)
~/.ssh/id_ed25519.pub
```

### View Your Public Key

```bash
# Display public key
cat ~/.ssh/id_ed25519.pub

# Copy to clipboard (macOS)
pbcopy < ~/.ssh/id_ed25519.pub

# Copy to clipboard (Linux)
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
```

---

## Add SSH Key to SSH Agent

The SSH agent manages your keys and handles authentication.

### Start SSH Agent

```bash
# Start SSH agent
eval "$(ssh-agent -s)"

# Output: Agent pid 12345
```

### Add Key to Agent

```bash
# Add default key
ssh-add ~/.ssh/id_ed25519

# Add with passphrase prompt
ssh-add ~/.ssh/id_ed25519

# List loaded keys
ssh-add -l

# Remove key from agent
ssh-add -d ~/.ssh/id_ed25519
```

### Auto-start SSH Agent (macOS)

Add to `~/.zshrc`:

```bash
# SSH Agent
if [ -z "$SSH_AUTH_SOCK" ]; then
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519
fi
```

Or use keychain (macOS):

```bash
# Install keychain
brew install keychain

# Add to ~/.zshrc
eval $(keychain --eval --quiet id_ed25519)
```

---

## Add SSH Key to GitHub

### Method 1: Web Interface

1. **Copy your public key**:
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

2. **Go to GitHub**:
   - Settings → SSH and GPG keys
   - Click "New SSH key"

3. **Add key**:
   - Title: "MacBook Pro" (or descriptive name)
   - Key: Paste your public key
   - Click "Add SSH key"

### Method 2: GitHub CLI

```bash
# Install GitHub CLI
brew install gh

# Authenticate
gh auth login

# Add SSH key
gh ssh-key add ~/.ssh/id_ed25519.pub --title "MacBook Pro"
```

### Test GitHub Connection

```bash
# Test SSH connection
ssh -T git@github.com

# Should see:
# Hi username! You've successfully authenticated...
```

---

## Add SSH Key to GitLab

1. **Copy your public key**:
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

2. **Go to GitLab**:
   - Settings → SSH Keys
   - Paste your public key
   - Add title and expiration (optional)
   - Click "Add key"

### Test GitLab Connection

```bash
# Test SSH connection
ssh -T git@gitlab.com

# Should see:
# Welcome to GitLab, @username!
```

---

## SSH Config File

Create `~/.ssh/config` to manage multiple SSH connections:

```bash
# Create config file
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

### Example Config

```bash
# GitHub
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes

# GitLab
Host gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes

# HCC Cluster
Host hcc
    HostName login.crane.hcc.unl.edu
    User your-username
    IdentityFile ~/.ssh/id_ed25519
    ForwardAgent yes
    ServerAliveInterval 60

# Alias for shorter command
Host cluster
    HostName login.crane.hcc.unl.edu
    User your-username
    IdentityFile ~/.ssh/id_ed25519
```

### Using Config

```bash
# Instead of:
ssh username@login.crane.hcc.unl.edu

# Use:
ssh hcc
# or
ssh cluster
```

---

## Connect to Remote Servers

### Basic Connection

```bash
# Connect to server
ssh username@hostname

# Example
ssh jdoe@login.crane.hcc.unl.edu

# With config file
ssh hcc
```

### First Connection

On first connection, you'll see:

```
The authenticity of host 'hostname' can't be established.
RSA key fingerprint is ...
Are you sure you want to continue connecting (yes/no)?
```

Type `yes` to add host to known hosts.

### Copy Public Key to Server

#### Method 1: ssh-copy-id (Easiest)

```bash
# Copy key to server
ssh-copy-id username@hostname

# With config
ssh-copy-id hcc
```

#### Method 2: Manual

```bash
# On your local machine
cat ~/.ssh/id_ed25519.pub

# Copy the output, then on remote server:
mkdir -p ~/.ssh
chmod 700 ~/.ssh
echo "paste-public-key-here" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

#### Method 3: One-liner

```bash
# Copy key in one command
cat ~/.ssh/id_ed25519.pub | ssh username@hostname "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

### Test Connection

```bash
# Should connect without password
ssh username@hostname
```

---

## Multiple SSH Keys

If you need different keys for different services:

### Generate Additional Keys

```bash
# Generate key for work
ssh-keygen -t ed25519 -C "work@example.com" -f ~/.ssh/id_ed25519_work

# Generate key for personal
ssh-keygen -t ed25519 -C "personal@example.com" -f ~/.ssh/id_ed25519_personal
```

### Configure Multiple Keys

Edit `~/.ssh/config`:

```bash
# Work GitHub
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes

# Personal GitHub
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes
```

### Use Different Keys

```bash
# Clone with work key
git clone git@github-work:company/repo.git

# Clone with personal key
git clone git@github-personal:username/repo.git
```

---

## SSH Agent Forwarding

Forward your SSH agent to access GitHub/GitLab from remote servers:

### Enable Agent Forwarding

In `~/.ssh/config`:

```bash
Host remote-server
    HostName server.example.com
    User username
    ForwardAgent yes
```

### Use on Remote Server

```bash
# Connect to remote server
ssh remote-server

# On remote server, you can now use GitHub/GitLab
git clone git@github.com:username/repo.git
```

---

## Security Best Practices

### 1. Use Strong Passphrases

Always use a passphrase for your private key:

```bash
# Generate key with passphrase
ssh-keygen -t ed25519 -C "email@example.com"
# Enter strong passphrase when prompted
```

### 2. Protect Private Key

```bash
# Set correct permissions
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 700 ~/.ssh
```

### 3. Never Share Private Key

- **NEVER** share `~/.ssh/id_ed25519` (private key)
- **OK** to share `~/.ssh/id_ed25519.pub` (public key)

### 4. Use Different Keys for Different Services

Don't reuse the same key everywhere.

### 5. Rotate Keys Periodically

Generate new keys every 1-2 years:

```bash
# Generate new key
ssh-keygen -t ed25519 -C "email@example.com" -f ~/.ssh/id_ed25519_new

# Add to services
# Remove old key from services
```

### 6. Use Keychain (macOS)

Store passphrase securely:

```bash
brew install keychain

# Add to ~/.zshrc
eval $(keychain --eval --quiet id_ed25519)
```

---

## Troubleshooting

### Issue: Permission Denied

**Problem**: Can't connect, "Permission denied (publickey)"

**Solution**:
```bash
# Check key permissions
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# Check server permissions
ssh username@hostname
# On server:
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys

# Verify key is added
ssh-add -l
```

### Issue: SSH Agent Not Running

**Problem**: Key not found

**Solution**:
```bash
# Start SSH agent
eval "$(ssh-agent -s)"

# Add key
ssh-add ~/.ssh/id_ed25519
```

### Issue: Wrong Key Used

**Problem**: Using wrong key for service

**Solution**:
```bash
# Check which key is used
ssh -vT git@github.com

# Specify key explicitly
ssh -i ~/.ssh/id_ed25519_work git@github.com

# Or use SSH config
```

### Issue: Host Key Verification Failed

**Problem**: "Host key verification failed"

**Solution**:
```bash
# Remove old host key
ssh-keygen -R hostname

# Or edit ~/.ssh/known_hosts and remove the line
```

### Issue: Connection Timeout

**Problem**: Can't connect to server

**Solution**:
```bash
# Test connection
ssh -v username@hostname

# Check if server is reachable
ping hostname

# Check firewall/VPN
```

### Issue: GitHub/GitLab Still Asking for Password

**Problem**: Using HTTPS instead of SSH

**Solution**:
```bash
# Check remote URL
git remote -v

# Change to SSH
git remote set-url origin git@github.com:username/repo.git

# Or when cloning
git clone git@github.com:username/repo.git
```

---

## Quick Reference

### Generate Keys

```bash
# Generate key
ssh-keygen -t ed25519 -C "email@example.com"

# View public key
cat ~/.ssh/id_ed25519.pub

# Copy to clipboard
pbcopy < ~/.ssh/id_ed25519.pub
```

### SSH Agent

```bash
# Start agent
eval "$(ssh-agent -s)"

# Add key
ssh-add ~/.ssh/id_ed25519

# List keys
ssh-add -l
```

### Connect to Server

```bash
# Basic connection
ssh username@hostname

# With config
ssh alias-name

# Copy key to server
ssh-copy-id username@hostname
```

### Test Connections

```bash
# Test GitHub
ssh -T git@github.com

# Test GitLab
ssh -T git@gitlab.com

# Test server
ssh username@hostname
```

---

## Related Guides

- **[Git Guide](git.md)** - Use SSH keys with Git
- **[HCC Clusters Guide](hcc-cluster.md)** - Connect to computing clusters
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

