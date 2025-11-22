# Command Line Guide

This guide will teach you how to use the command line (terminal) on macOS, from absolute basics to advanced techniques and useful tools.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Basic Commands](#basic-commands)
3. [File Operations](#file-operations)
4. [Text Processing](#text-processing)
5. [Advanced Techniques](#advanced-techniques)
6. [Cool Tools](#cool-tools)
7. [Tips and Tricks](#tips-and-tricks)

---

## Getting Started

### Opening the Terminal

On macOS, you can open Terminal in several ways:

1. **Spotlight Search**: Press `Cmd+Space`, type "Terminal", press Enter
2. **Applications**: Applications → Utilities → Terminal
3. **Finder**: Go → Utilities → Terminal

### Understanding the Prompt

When you open Terminal, you'll see something like:

```bash
username@computername ~ %
```

This is called the "prompt". It shows:
- Your username
- Your computer name
- Current directory (`~` means your home directory)
- Ready for your command (`%`)

### Your First Commands

Let's start with the most basic commands:

```bash
# See what directory you're in
pwd

# List files in current directory
ls

# Print text to screen
echo "Hello, World!"

# Clear the screen
clear
```

---

## Basic Commands

### Navigation

```bash
# Print Working Directory - see where you are
pwd

# List files and directories
ls

# List with details (long format)
ls -l

# List all files including hidden ones
ls -a

# List with human-readable file sizes
ls -lh

# Change directory
cd Documents

# Go to home directory
cd ~
# or just
cd

# Go up one directory
cd ..

# Go to root directory
cd /

# Go to previous directory
cd -
```

### Getting Help

```bash
# Get help for any command
man ls          # Manual page for ls
man cd          # Manual page for cd

# Quick help (if available)
ls --help

# Search manual pages
man -k search_term
```

### Viewing Files

```bash
# View entire file
cat filename.txt

# View file page by page
less filename.txt
# Press 'q' to quit, space for next page, 'b' for previous page

# View first 10 lines
head filename.txt

# View first 20 lines
head -n 20 filename.txt

# View last 10 lines
tail filename.txt

# View last 20 lines
tail -n 20 filename.txt

# Watch a file as it updates (great for logs)
tail -f logfile.txt
```

---

## File Operations

### Creating Files and Directories

```bash
# Create a new directory
mkdir my_folder

# Create nested directories
mkdir -p parent/child/grandchild

# Create an empty file
touch newfile.txt

# Create multiple files
touch file1.txt file2.txt file3.txt

# Create file with content using echo
echo "Hello World" > hello.txt

# Append to file
echo "New line" >> hello.txt
```

### Copying and Moving

```bash
# Copy a file
cp source.txt destination.txt

# Copy a directory (recursive)
cp -r source_dir destination_dir

# Move/rename a file
mv oldname.txt newname.txt

# Move file to different directory
mv file.txt ~/Documents/

# Move multiple files
mv file1.txt file2.txt ~/Documents/
```

### Deleting

```bash
# Delete a file
rm filename.txt

# Delete multiple files
rm file1.txt file2.txt file3.txt

# Delete directory (empty)
rmdir empty_folder

# Delete directory with contents (CAREFUL!)
rm -r folder_name

# Delete with confirmation
rm -i filename.txt

# Force delete (no confirmation - DANGEROUS!)
rm -f filename.txt
```

### Finding Files

```bash
# Find files by name
find . -name "*.txt"

# Find files in home directory
find ~ -name "*.py"

# Find directories
find . -type d -name "my_folder"

# Find files modified in last 7 days
find . -mtime -7

# Find files larger than 100MB
find . -size +100M
```

---

## Text Processing

### Searching in Files

```bash
# Search for text in a file
grep "search term" filename.txt

# Case-insensitive search
grep -i "search" filename.txt

# Search in multiple files
grep "search" *.txt

# Search recursively in directories
grep -r "search" .

# Show line numbers
grep -n "search" filename.txt

# Show context (3 lines before and after)
grep -C 3 "search" filename.txt

# Count matches
grep -c "search" filename.txt
```

### Editing Text

```bash
# Open file in nano (beginner-friendly editor)
nano filename.txt
# Ctrl+X to exit, Y to save, N to discard

# Open file in vim (advanced editor)
vim filename.txt
# Press 'i' to insert, 'Esc' then ':wq' to save and quit
# ':q!' to quit without saving

# Open file in VS Code from terminal
code filename.txt

# Open file in Cursor
cursor filename.txt
```

### Text Manipulation

```bash
# Count lines, words, characters
wc filename.txt

# Count lines only
wc -l filename.txt

# Count words only
wc -w filename.txt

# Sort lines alphabetically
sort filename.txt

# Sort numerically
sort -n numbers.txt

# Remove duplicate lines
sort filename.txt | uniq

# Show unique lines with count
sort filename.txt | uniq -c

# Extract specific columns (space-separated)
cut -d' ' -f1,3 filename.txt

# Replace text
sed 's/old/new/g' filename.txt

# Replace in file (modify file)
sed -i '' 's/old/new/g' filename.txt
```

---

## Advanced Techniques

### Pipes and Redirection

```bash
# Pipe output of one command to another
ls -l | grep ".txt"

# Count files in directory
ls | wc -l

# Save output to file
ls > file_list.txt

# Append output to file
echo "new line" >> file_list.txt

# Use output as input
cat file1.txt file2.txt > combined.txt

# Chain multiple commands
ls -l | grep ".txt" | wc -l
```

### Variables and Environment

```bash
# Set a variable
MY_VAR="Hello World"

# Use a variable
echo $MY_VAR

# List all environment variables
env

# View specific variable
echo $HOME
echo $PATH

# Add to PATH
export PATH="$PATH:/new/directory"
```

### Command Substitution

```bash
# Use output of command as input
echo "Today is $(date)"

# Store command output in variable
FILES=$(ls *.txt)
echo $FILES

# Count files matching pattern
FILE_COUNT=$(ls *.txt | wc -l)
echo "Found $FILE_COUNT text files"
```

### Loops

```bash
# For loop - process each file
for file in *.txt; do
    echo "Processing $file"
    wc -l "$file"
done

# For loop with numbers
for i in {1..10}; do
    echo "Number: $i"
done

# While loop
counter=1
while [ $counter -le 5 ]; do
    echo "Count: $counter"
    counter=$((counter + 1))
done
```

### Conditional Statements

```bash
# If statement
if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi

# Check if directory exists
if [ -d "my_folder" ]; then
    echo "Directory exists"
fi

# Check file permissions
if [ -r "file.txt" ]; then
    echo "File is readable"
fi
```

### Background Processes

```bash
# Run command in background
python long_script.py &

# See background jobs
jobs

# Bring job to foreground
fg %1

# Kill a background job
kill %1

# Run command and detach (nohup)
nohup python script.py &
```

### Aliases

```bash
# Create an alias
alias ll='ls -lh'

# Create alias for common command
alias ..='cd ..'
alias ...='cd ../..'

# List all aliases
alias

# Make alias permanent (add to ~/.zshrc)
echo 'alias ll="ls -lh"' >> ~/.zshrc
source ~/.zshrc
```

---

## Cool Tools

### Homebrew (Package Manager)

```bash
# Install Homebrew (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install packages
brew install tree
brew install htop
brew install wget
brew install jq

# Update Homebrew
brew update

# Upgrade packages
brew upgrade

# List installed packages
brew list

# Search for packages
brew search python
```

### Useful Homebrew Tools

#### tree - Directory Tree Visualization

```bash
# Install
brew install tree

# Show directory tree
tree

# Show tree with depth limit
tree -L 2

# Show only directories
tree -d

# Show hidden files
tree -a
```

#### htop - Process Monitor

```bash
# Install
brew install htop

# Run htop
htop

# Shows: CPU usage, memory, running processes
# Press 'q' to quit, 'F5' for tree view
```

#### jq - JSON Processor

```bash
# Install
brew install jq

# Pretty print JSON
cat data.json | jq .

# Extract specific field
cat data.json | jq '.name'

# Filter array
cat data.json | jq '.[] | select(.age > 30)'
```

#### bat - Better cat

```bash
# Install
brew install bat

# View file with syntax highlighting
bat filename.py

# Show line numbers
bat -n filename.py

# Show multiple files
bat file1.txt file2.txt
```

#### fd - Better find

```bash
# Install
brew install fd

# Find files (faster than find)
fd "\.py$"

# Find in specific directory
fd "test" src/

# Case-insensitive search
fd -i "python"
```

#### ripgrep (rg) - Better grep

```bash
# Install
brew install ripgrep

# Search (faster than grep)
rg "search term"

# Search in specific file types
rg "function" --type py

# Show context
rg "error" -C 3
```

#### fzf - Fuzzy Finder

```bash
# Install
brew install fzf

# Interactive file finder
fzf

# Search command history
# Press Ctrl+R in terminal

# Install useful key bindings
$(brew --prefix)/opt/fzf/install
```

#### tldr - Simplified Manual Pages

```bash
# Install
brew install tldr

# Get simplified help
tldr ls
tldr git
tldr python
```

#### exa - Better ls

```bash
# Install
brew install exa

# List files (with colors and icons)
exa

# Tree view
exa --tree

# Long format with git status
exa --long --git
```

### Git Commands

```bash
# Initialize repository
git init

# Check status
git status

# Add files
git add filename.txt
git add .  # Add all files

# Commit changes
git commit -m "Your message"

# View history
git log

# View changes
git diff

# Create branch
git branch new-feature

# Switch branch
git checkout new-feature

# Merge branch
git merge new-feature

# Clone repository
git clone https://github.com/user/repo.git
```

### Python-Specific Commands

```bash
# Run Python script
python script.py

# Run Python interactively
python

# Install package
pip install package_name

# Install from requirements
pip install -r requirements.txt

# List installed packages
pip list

# Create virtual environment
python -m venv venv

# Activate virtual environment
source venv/bin/activate

# Deactivate
deactivate
```

### Conda Commands

```bash
# Create environment
conda create -n myenv python=3.10

# Activate environment
conda activate myenv

# Install package
conda install numpy

# List environments
conda env list

# Deactivate
conda deactivate

# Export environment
conda env export > environment.yml
```

---

## Tips and Tricks

### Keyboard Shortcuts

```bash
# In Terminal:
Ctrl+A          # Move to beginning of line
Ctrl+E          # Move to end of line
Ctrl+U          # Delete to beginning of line
Ctrl+K          # Delete to end of line
Ctrl+W          # Delete previous word
Ctrl+L          # Clear screen (same as 'clear')
Ctrl+C          # Cancel current command
Ctrl+D          # Exit terminal
Ctrl+R          # Search command history
Tab             # Auto-complete
Tab Tab         # Show all completions
```

### Command History

```bash
# View command history
history

# Search history
history | grep "python"

# Run previous command
!!

# Run command from history by number
!42

# Run last command starting with 'python'
!python
```

### Tab Completion

```bash
# Type part of filename and press Tab
ls Doc[TAB]     # Completes to "Documents/"

# Press Tab twice to see all options
ls D[TAB][TAB]   # Shows all files starting with 'D'
```

### Wildcards

```bash
# Match any characters
ls *.txt        # All .txt files
ls file*        # All files starting with "file"

# Match single character
ls file?.txt    # file1.txt, file2.txt, etc.

# Match character range
ls file[1-5].txt

# Match specific characters
ls file[abc].txt
```

### Combining Commands

```bash
# Run command only if previous succeeds
command1 && command2

# Run command if previous fails
command1 || command2

# Run multiple commands sequentially
command1; command2; command3

# Run command in subshell
(cd /tmp && ls)
```

### Useful One-Liners

```bash
# Find largest files in directory
du -h . | sort -rh | head -10

# Count files by type
find . -name "*.py" | wc -l

# Find and delete old files
find . -name "*.log" -mtime +30 -delete

# Monitor file changes
watch -n 1 'ls -lht | head'

# Extract all URLs from file
grep -oP 'http[s]?://[^\s]+' file.txt

# Find duplicate files
find . -type f -exec md5 {} \; | sort | uniq -d -w 32

# Rename files in bulk
for file in *.txt; do mv "$file" "${file%.txt}.bak"; done

# Create backup of directory
tar -czf backup.tar.gz directory/

# Extract tar file
tar -xzf backup.tar.gz
```

### Customizing Your Terminal

#### Edit Your Shell Configuration

```bash
# Edit zsh configuration
nano ~/.zshrc

# Add useful aliases
alias ll='ls -lh'
alias la='ls -lah'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'

# Add to PATH
export PATH="$PATH:/custom/path"

# Reload configuration
source ~/.zshrc
```

#### Install Oh My Zsh (Enhanced Terminal)

```bash
# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Popular plugins to add to ~/.zshrc:
# plugins=(git python pip conda)
```

---

## Practice Exercises

### Beginner

1. Navigate to your Documents folder and list all files
2. Create a new folder called "test" and a file called "hello.txt" inside it
3. Write "Hello World" to the file
4. View the contents of the file
5. Copy the file to your home directory
6. Delete the test folder

### Intermediate

1. Find all Python files in your home directory
2. Count how many .txt files are in a directory
3. Search for a specific word in all text files
4. Create a backup of a directory using tar
5. List the 10 largest files in your home directory

### Advanced

1. Write a script that renames all files in a directory with a prefix
2. Find and delete all files older than 30 days
3. Create a script that monitors a log file and alerts on errors
4. Write a one-liner that finds duplicate files
5. Create an alias that shows your most used commands

---

## Related Guides

Continue with these Getting Started guides:

- **[Development Environment Setup](development-environment.md)** - Set up Homebrew, conda, and IDEs (uses command line)
- **[Installation Guide](installation.md)** - Install lab-specific software (uses command line)
- **[Lab Guide / FAQ](faq.md)** - Lab rules, policies, and expectations
- **[Quick Start Guide](quick-start.md)** - Get started with immediate tasks
- **[Getting Started Overview](overview.md)** - Return to the main getting started page

## Resources

- **Terminal Basics**: https://developer.apple.com/library/archive/documentation/OpenSource/Conceptual/Shell_Basics/
- **Bash Guide**: https://www.gnu.org/software/bash/manual/
- **Command Line Challenge**: https://cmdchallenge.com/
- **Explain Shell**: https://explainshell.com/ (explains any command)

---

*Last updated: {{ git_revision_date_localized }}*

