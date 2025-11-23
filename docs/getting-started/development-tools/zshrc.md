# Zsh Configuration (.zshrc)

The `.zshrc` file is your shell's configuration file. Think of it as a settings file that runs automatically every time you open a new terminal window. It's where you can customize your terminal, set up shortcuts, and configure tools like Homebrew and conda.

---

## What is .zshrc?

**`.zshrc`** (pronounced "zee-ess-aitch-arr-see") is a hidden file in your home directory that contains configuration for the Z shell (zsh), which is the default shell on macOS.

### Why Do You Need It?

- **Customize your terminal**: Change how your prompt looks, add colors, etc.
- **Set up shortcuts**: Create aliases for long commands you use often
- **Initialize tools**: Automatically set up Homebrew, conda, and other tools
- **Save time**: Automatically configure your environment so you don't have to do it manually each time

### Where Is It?

The file is located at: `~/.zshrc` (which is the same as `/Users/your-username/.zshrc`)

The dot (`.`) at the beginning means it's a hidden file, so you won't see it in Finder by default.

---

## Do You Already Have One?

Let's check if you already have a `.zshrc` file:

```bash
# Check if .zshrc exists
ls -la ~/.zshrc
```

**If you see output**: You already have a `.zshrc` file! You can view it with:
```bash
cat ~/.zshrc
```

**If you see "No such file or directory"**: You don't have one yet, and that's fine! We'll create one.

---

## Creating Your First .zshrc File

### Step 1: Open Your Terminal

Open the Terminal app (found in Applications > Utilities, or press `Cmd+Space` and type "Terminal").

### Step 2: Create the File

You can create and edit the file using any text editor. Here are your options:

**Option A: Using VS Code or Cursor (Recommended)**
```bash
# If you have VS Code installed
code ~/.zshrc

# If you have Cursor installed
cursor ~/.zshrc
```

**Option B: Using TextEdit (macOS default)**
```bash
open -e ~/.zshrc
```

**Option C: Using nano (terminal editor)**
```bash
nano ~/.zshrc
```
(To save in nano: Press `Ctrl+O`, then `Enter`, then `Ctrl+X` to exit)

### Step 3: Add Basic Configuration

If you're starting from scratch, here's a minimal `.zshrc` to get you started. Each section is explained below:

```bash
# ~/.zshrc
# Your shell configuration file

# History settings - remember more commands
HISTFILE="$HOME/.zsh_history"    # Where to save your command history
HISTSIZE=10000                    # Remember 10,000 commands in memory
SAVEHIST=10000                    # Save 10,000 commands to file

# Share history between terminal windows
setopt SHARE_HISTORY              # Commands from one window appear in others

# Don't save duplicate commands
setopt HIST_IGNORE_DUPS           # If you run the same command twice, only save it once

# Useful aliases (shortcuts)
alias ll='ls -alF'                # Type "ll" to see files with details
alias la='ls -A'                  # Type "la" to see all files (including hidden)
alias ..='cd ..'                  # Type ".." to go up one directory
alias ...='cd ../..'              # Type "..." to go up two directories

# Python aliases
alias python='python3'            # Type "python" to run Python 3
alias pip='pip3'                  # Type "pip" to use pip3
```

**What each part does:**

1. **Comments** (`#` lines): These are just notes for you - the computer ignores them.

2. **History settings:**
   - `HISTFILE` - Where your command history is saved (usually `~/.zsh_history`)
   - `HISTSIZE` - How many commands to remember while your terminal is open
   - `SAVEHIST` - How many commands to save permanently (so you can see them after closing the terminal)

3. **setopt commands:**
   - `SHARE_HISTORY` - If you type a command in one terminal window, you can access it in another window
   - `HIST_IGNORE_DUPS` - Prevents your history from being cluttered with the same command repeated many times

4. **Aliases:**
   - `ll` - Shortcut for `ls -alF` (list files with full details)
   - `la` - Shortcut for `ls -A` (list all files including hidden ones)
   - `..` - Shortcut for `cd ..` (go up one directory)
   - `...` - Shortcut for `cd ../..` (go up two directories)
   - `python` - Shortcut for `python3` (run Python 3)
   - `pip` - Shortcut for `pip3` (use pip3)

**After adding this, try it out:**
```bash
# Reload your configuration
source ~/.zshrc

# Try the aliases
ll          # Should show files with details
..          # Should go up one directory
python --version  # Should show Python 3 version
```

### Step 4: Save and Apply

1. **Save the file** (in your editor, press `Cmd+S`)

2. **Reload your terminal configuration**:
```bash
source ~/.zshrc
```

Or simply **close and reopen your terminal** - it will automatically load the new configuration.

---

## Using a Complete Example Configuration

If you want a more comprehensive setup that includes configuration for Homebrew, conda, and other development tools, you can use an example `.zshrc` file.

### How to Get the Example File

**Option 1: Copy from the repository** (if you have the lab-docs repository):
```bash
# Navigate to the repository directory
cd /path/to/lab-docs

# Copy the example file to your home directory
cp docs/getting-started/development-tools/.zshrc.example ~/.zshrc
```

**Option 2: View and copy the file**:
```bash
# View the example file
cat docs/getting-started/development-tools/.zshrc.example

# Or open it in an editor
code docs/getting-started/development-tools/.zshrc.example
```

Then copy the contents and paste them into your `~/.zshrc` file.

### How to Use the Example File

1. **Backup your current .zshrc** (if you have one):
```bash
# If you have an existing .zshrc, back it up first
cp ~/.zshrc ~/.zshrc.backup
```

2. **Copy the example to your home directory** (see options above)

3. **Reload your configuration**:
```bash
source ~/.zshrc
```

!!! note "Note"
    The example file includes configuration for tools you might not have installed yet (like Oh My Zsh, Starship, or zoxide). That's okay - the configuration checks if these tools exist before trying to use them, so it won't cause errors if they're not installed.

---

## Understanding What Goes in .zshrc

This section explains all the different types of things you can put in your `.zshrc` file and what they do.

### 1. Comments

**What are comments?** Comments are notes for humans - the computer ignores them completely. They help you remember what your configuration does.

**How to write comments:** Start a line with `#`:
```bash
# This is a comment - it's just for reading
# The computer will completely ignore this line
```

**Why use comments?** They help you (and others) understand what your configuration does, especially if you come back to it months later.

### 2. Aliases (Shortcuts)

**What is an alias?** An alias is a shortcut - it lets you type a short command instead of a long one.

**How aliases work:**
```bash
alias ll='ls -alF'
```

This means: "When I type `ll`, run the command `ls -alF` instead."

**Real-world example:**
- **Without alias:** You type `ls -alF` every time you want to see detailed file listings
- **With alias:** You just type `ll` and it does the same thing

**Common aliases explained:**

```bash
# Navigation shortcuts
alias ..='cd ..'          # Type ".." to go up one directory
alias ...='cd ../..'      # Type "..." to go up two directories

# File listing shortcuts
alias ll='ls -alF'        # Type "ll" to see files with details
alias la='ls -A'          # Type "la" to see all files (including hidden)
alias l='ls -CF'          # Type "l" for a compact file list

# Python shortcuts
alias python='python3'    # Type "python" to run Python 3
alias pip='pip3'          # Type "pip" to use pip3

# Git shortcuts (if you use Git)
alias gs='git status'     # Type "gs" to check Git status
alias ga='git add'        # Type "ga" to add files to Git
alias gc='git commit -m'  # Type "gc" to commit changes
```

**How to create your own alias:**
1. Think of a command you type often
2. Decide on a short name for it
3. Add it to your `.zshrc`:
   ```bash
   alias shortname='long command here'
   ```
4. Reload: `source ~/.zshrc`

**Example:** If you often type `cd ~/Documents/Projects`, you could create:
```bash
alias proj='cd ~/Documents/Projects'
```
Then just type `proj` to go there!

### 3. Environment Variables

**What are environment variables?** Environment variables are settings that programs can read. They tell your computer how to behave.

**Common environment variables:**

**PATH** - This is the most important one! It tells your computer where to look for programs.

```bash
export PATH="$HOME/bin:$PATH"
```

**What does this mean?**
- `export` means "make this available to all programs"
- `PATH` is the variable name
- `"$HOME/bin:$PATH"` means "look in my bin folder first, then look in the existing PATH"

**Why does PATH matter?** When you type a command like `python` or `git`, your computer searches through all the directories in PATH to find that program. If the program isn't in PATH, you'll get "command not found" errors.

**Other useful environment variables:**

```bash
# Set your default text editor
export EDITOR='code'      # Use VS Code
# or
export EDITOR='cursor'    # Use Cursor
# or
export EDITOR='vim'       # Use vim

# Language settings (for proper character encoding)
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# Python settings
export PYTHONUNBUFFERED=1  # Show Python output immediately (useful for debugging)
```

**How to see your environment variables:**
```bash
# See all environment variables
env

# See a specific one
echo $PATH
echo $EDITOR
```

### 4. History Settings

**What is command history?** Your terminal remembers all the commands you've typed. You can press the up arrow to see previous commands.

**History settings control:**
- How many commands to remember
- Whether to share history between terminal windows
- Whether to save duplicate commands

**Common history settings explained:**

```bash
# Where to save the history file
HISTFILE="$HOME/.zsh_history"

# How many commands to remember in memory (while terminal is open)
HISTSIZE=10000

# How many commands to save to file (persists after closing terminal)
SAVEHIST=10000

# Share history between all terminal windows
setopt SHARE_HISTORY

# Don't save duplicate commands (if you run the same command twice, only save it once)
setopt HIST_IGNORE_DUPS
```

**Why configure history?** 
- **More history:** Remember more commands (default is often only 1000)
- **Share between windows:** If you type a command in one terminal, you can access it in another
- **Cleaner history:** Don't clutter your history with the same command repeated 50 times

### 5. setopt (Shell Options)

**What is setopt?** `setopt` turns on special features or behaviors in zsh.

**Common setopt options:**

```bash
# Share command history between all terminal windows
setopt SHARE_HISTORY

# Don't save duplicate commands in history
setopt HIST_IGNORE_DUPS

# Don't save commands that start with a space (useful for sensitive commands)
setopt HIST_IGNORE_SPACE

# Show the command before running it (when using history expansion)
setopt HIST_VERIFY
```

**How to see all options:**
```bash
# See all enabled options
setopt

# See all disabled options
unsetopt
```

### 6. Tool Initialization

**What is tool initialization?** This sets up tools (like Homebrew or conda) so they work automatically when you open a terminal.

**Why is this needed?** Some tools need to be "initialized" - they need to set up their environment before you can use them. Without initialization, you might get "command not found" errors even though the tool is installed.

**Example: Homebrew initialization**

```bash
# Initialize Homebrew (if installed)
if command -v brew &> /dev/null; then
  eval "$(/opt/homebrew/bin/brew shellenv)"
fi
```

**Breaking this down:**
- `if command -v brew &> /dev/null` - Check if `brew` command exists
- `then` - If it exists, do the next line
- `eval "$(/opt/homebrew/bin/brew shellenv)"` - Run Homebrew's setup command
- `fi` - End of the if statement

**Why the "if" check?** This is called "lazy loading" - it only tries to initialize Homebrew if it's actually installed. Without this check, you'd get errors every time you open a terminal if Homebrew isn't installed.

**Example: Conda initialization**

```bash
# Initialize conda (if installed)
if command -v conda &> /dev/null; then
  eval "$(conda shell.zsh hook)"
fi
```

This does the same thing for conda - checks if it exists, then initializes it if it does.

### 7. Conditional Statements (if/then/fi)

**What are conditionals?** They let your `.zshrc` check if something exists before trying to use it.

**Basic structure:**
```bash
if [ condition ]; then
  # do something
fi
```

**Common patterns:**

```bash
# Check if a command exists
if command -v somecommand &> /dev/null; then
  # Initialize the tool
  eval "$(somecommand init zsh)"
fi

# Check if a file exists
if [ -f "$HOME/.somefile" ]; then
  # Load the file
  source "$HOME/.somefile"
fi

# Check if a directory exists
if [ -d "$HOME/.somedir" ]; then
  # Do something with the directory
  export PATH="$HOME/.somedir/bin:$PATH"
fi
```

**Why use conditionals?** They prevent errors. If you try to initialize a tool that doesn't exist, you'll get error messages every time you open a terminal. Conditionals check first, so they only run if the tool is actually there.

### 8. Functions

**What are functions?** Functions are like aliases, but more powerful - they can do multiple things and accept arguments.

**Simple function example:**
```bash
# Create a function to go to a project directory
proj() {
  cd ~/Documents/Projects/$1
}
```

**How to use it:**
```bash
proj myproject    # Goes to ~/Documents/Projects/myproject
```

**More complex function example:**
```bash
# Create a function to make a directory and go into it
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

**How to use it:**
```bash
mkcd newfolder    # Creates "newfolder" and goes into it
```

**Functions vs aliases:**
- **Aliases:** Simple replacements (type A, run B)
- **Functions:** Can do multiple commands, accept arguments, use logic

### Summary: What Each Thing Does

| Type | Purpose | Example |
|------|---------|---------|
| **Comment** | Notes for humans | `# This is a comment` |
| **Alias** | Shortcut for a command | `alias ll='ls -alF'` |
| **Environment Variable** | Settings for programs | `export PATH="$HOME/bin:$PATH"` |
| **History Setting** | Control command history | `HISTSIZE=10000` |
| **setopt** | Enable shell features | `setopt SHARE_HISTORY` |
| **Tool Initialization** | Set up tools automatically | `eval "$(brew shellenv)"` |
| **Conditional** | Check before doing something | `if command -v brew; then ... fi` |
| **Function** | Custom command with logic | `proj() { cd ~/Projects/$1; }` |

---

## Common Customizations

Here are some common things you might want to add to your `.zshrc` file.

### Adding Your Own Aliases

**What are aliases again?** Shortcuts that let you type a short command instead of a long one.

**Navigation shortcuts** - Make it easier to move around directories:
```bash
alias ..='cd ..'          # Type ".." to go up one directory (parent folder)
alias ...='cd ../..'      # Type "..." to go up two directories
alias ....='cd ../../..'  # Type "...." to go up three directories
```

**How to use:** Instead of typing `cd ..`, just type `..`

**File listing shortcuts** - Make it easier to see files:
```bash
alias ll='ls -alF'        # Type "ll" to see files with details (size, date, permissions)
alias la='ls -A'          # Type "la" to see all files, including hidden ones (starting with .)
alias l='ls -CF'          # Type "l" for a compact, colorized file list
```

**What do these commands do?**
- `ls` = list files
- `-a` = show all files (including hidden)
- `-l` = long format (show details)
- `-F` = add symbols to show file types (/ for directories, * for executables)
- `-C` = column format

**Git shortcuts** - If you use Git, these save a lot of typing:
```bash
alias gs='git status'           # Type "gs" to see what files have changed
alias ga='git add'               # Type "ga filename" to add a file
alias gc='git commit -m'         # Type "gc 'message'" to commit changes
alias gp='git push'              # Type "gp" to push your changes
alias gl='git log'               # Type "gl" to see commit history
```

**How to use Git aliases:**
```bash
# Instead of typing:
git status

# Just type:
gs

# Instead of typing:
git commit -m "Fixed bug"

# Just type:
gc "Fixed bug"
```

### Adding Directories to PATH

**What is PATH again?** The list of directories where your computer looks for programs.

**Why add directories to PATH?** If you install programs in custom locations (not the standard system locations), you need to tell your computer where to find them.

**How to add directories:**
```bash
# Add a custom bin directory to PATH
export PATH="$HOME/bin:$PATH"
```

**Breaking this down:**
- `$HOME/bin` = your personal bin directory (where you might put custom scripts)
- `:$PATH` = keep the existing PATH, just add your directory to the front
- The order matters! Directories at the front are searched first

**Multiple directories:**
```bash
# Add multiple directories
export PATH="$HOME/bin:$PATH"
export PATH="$HOME/.local/bin:$PATH"
```

**Or add them all at once:**
```bash
export PATH="$HOME/bin:$HOME/.local/bin:$PATH"
```

**How to check your PATH:**
```bash
# See all directories in PATH (separated by colons)
echo $PATH

# See them on separate lines (easier to read)
echo $PATH | tr ':' '\n'
```

### Setting Environment Variables

**What are environment variables again?** Settings that programs can read to know how to behave.

**Set your default editor:**
```bash
# Use VS Code as your default editor
export EDITOR='code'

# Or use Cursor
export EDITOR='cursor'

# Or use vim (if you're comfortable with it)
export EDITOR='vim'
```

**Why set EDITOR?** Some programs (like Git) need to know which editor to use. When you run `git commit` without a message, it opens your default editor.

**Python settings:**
```bash
# Show Python output immediately (don't wait for buffer to fill)
export PYTHONUNBUFFERED=1
```

**What does this do?** Normally, Python waits to show output until it has a certain amount. This makes it show output immediately, which is helpful when debugging.

**Language/encoding settings:**
```bash
# Set language and character encoding
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

**Why set these?** Ensures your terminal handles special characters correctly (like accents, emojis, or characters from other languages).

### Creating Custom Functions

**What are functions again?** Custom commands that can do multiple things and accept arguments.

**Example: Make a directory and go into it:**
```bash
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

**How to use:**
```bash
mkcd newproject    # Creates "newproject" directory and goes into it
```

**Breaking it down:**
- `mkcd` = the function name (you choose this)
- `"$1"` = the first argument (what you type after the function name)
- `mkdir -p` = create directory (and parent directories if needed)
- `&&` = "and then"
- `cd "$1"` = change into that directory

**Example: Quick project navigation:**
```bash
proj() {
  cd ~/Documents/Projects/$1
}
```

**How to use:**
```bash
proj myproject    # Goes to ~/Documents/Projects/myproject
```

**Example: Find and open a file:**
```bash
# Find a file and open it in your editor
findopen() {
  find . -name "$1" -exec code {} \;
}
```

**How to use:**
```bash
findopen README.md    # Finds README.md and opens it in VS Code
```

---

## Editing Your .zshrc

### How to Edit

```bash
# Open in VS Code
code ~/.zshrc

# Open in Cursor
cursor ~/.zshrc

# Open in TextEdit
open -e ~/.zshrc

# Open in nano (terminal editor)
nano ~/.zshrc
```

### After Making Changes

Always reload your configuration after editing:

```bash
source ~/.zshrc
```

Or close and reopen your terminal.

---

## Troubleshooting

### Problem: Changes Don't Appear

**Solution**: You need to reload the configuration:
```bash
source ~/.zshrc
```

### Problem: Terminal Shows Errors

**Solution**: Check for syntax errors:
```bash
# Check for errors without applying
zsh -n ~/.zshrc
```

If there are errors, check the line numbers mentioned in the error message.

### Problem: Command Not Found

**Solution**: Make sure the tool is installed and the PATH is set correctly in your `.zshrc`:
```bash
# Check if the command exists
which command-name

# Check your PATH
echo $PATH
```

### Problem: Terminal Starts Slowly

**Solution**: This might happen if you're loading too many tools. The example configuration uses "lazy loading" (only loads tools if they exist) to prevent this.

---

## Quick Reference

```bash
# View your .zshrc
cat ~/.zshrc

# Edit your .zshrc
code ~/.zshrc        # VS Code
cursor ~/.zshrc      # Cursor
nano ~/.zshrc        # nano

# Reload .zshrc
source ~/.zshrc

# Check for errors
zsh -n ~/.zshrc

# Backup before making changes
cp ~/.zshrc ~/.zshrc.backup

# Restore from backup
cp ~/.zshrc.backup ~/.zshrc
```

---

## Next Steps

Now that you have a `.zshrc` file set up:

1. **Customize it**: Add your own aliases and settings
2. **Install tools**: Set up [Homebrew](homebrew.md) and [Conda](conda.md) - they'll work better with a proper `.zshrc`
3. **Learn more**: Check out the [Command Line Guide](../command-line-guide.md) to learn terminal basics

---

## Related Guides

- **[Homebrew Guide](homebrew.md)** - Installing development tools
- **[Conda Guide](conda.md)** - Python environment management
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Development Environment Setup](../development-environment.md)** - Complete macOS setup guide
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

