# Oh My Zsh

Oh My Zsh is a framework for managing your zsh configuration. Think of it as a collection of themes, plugins, and helpful features that make your terminal more powerful and easier to use.

---

## What is Oh My Zsh?

**Oh My Zsh** is a popular, open-source framework that helps you customize your terminal. It provides:

- **Themes**: Pre-made designs that change how your terminal prompt looks
- **Plugins**: Add-ons that add new features and shortcuts
- **Helper functions**: Built-in tools that make common tasks easier

### Why Use Oh My Zsh?

- **Make your terminal prettier**: Choose from hundreds of themes
- **Add useful features**: Get shortcuts and tools for Git, Python, Docker, and more
- **Save time**: Common tasks become faster with built-in aliases
- **Easy to customize**: Simple configuration, no need to write everything from scratch

### Do You Need It?

**You might want Oh My Zsh if:**
- You want a nicer-looking terminal prompt
- You use Git frequently (Oh My Zsh has great Git shortcuts)
- You want helpful features without writing your own configuration
- You like having lots of customization options

**You might skip it if:**
- You prefer a minimal setup
- You want full control over every detail
- You're using a different prompt tool (like Starship)

---

## Installation

### Step 1: Check if You Already Have It

```bash
# Check if Oh My Zsh is installed
ls -la ~/.oh-my-zsh
```

**If you see a directory**: You already have Oh My Zsh installed!

**If you see "No such file or directory"**: You need to install it.

### Step 2: Install Oh My Zsh

Open your terminal and run:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

This command:
1. Downloads the Oh My Zsh installer
2. Runs it automatically
3. Sets up Oh My Zsh in your home directory

**What happens during installation:**
- It creates a `~/.oh-my-zsh` directory
- It backs up your existing `.zshrc` to `.zshrc.pre-oh-my-zsh`
- It creates a new `.zshrc` file with Oh My Zsh configuration

### Step 3: Restart Your Terminal

After installation, close and reopen your terminal, or run:

```bash
source ~/.zshrc
```

You should see your terminal prompt change (it will look different from before).

---

## Understanding Oh My Zsh Structure

### Where Everything Is Located

Oh My Zsh installs to `~/.oh-my-zsh` (which is `/Users/your-username/.oh-my-zsh`).

**Important directories:**
- `~/.oh-my-zsh/themes/` - All available themes
- `~/.oh-my-zsh/plugins/` - All available plugins
- `~/.oh-my-zsh/custom/` - Your custom themes and plugins
- `~/.zshrc` - Your configuration file (this is what you edit)

### How Oh My Zsh Works

Oh My Zsh works by modifying your `.zshrc` file. When you install it, it adds code to your `.zshrc` that:
1. Sets up the Oh My Zsh framework
2. Loads your chosen theme
3. Loads your chosen plugins
4. Provides helper functions

You configure Oh My Zsh by editing your `.zshrc` file.

---

## Configuring Oh My Zsh

### Where to Configure

All Oh My Zsh configuration is in your `~/.zshrc` file. After installation, it will look something like this:

```bash
# Path to your oh-my-zsh installation
export ZSH="$HOME/.oh-my-zsh"

# Theme name
ZSH_THEME="robbyrussell"

# Plugins
plugins=(git)

# Load Oh My Zsh
source $ZSH/oh-my-zsh.sh
```

### How to Edit Your Configuration

```bash
# Open in VS Code
code ~/.zshrc

# Open in Cursor
cursor ~/.zshrc

# Open in TextEdit
open -e ~/.zshrc

# Open in nano
nano ~/.zshrc
```

**After making changes**, always reload:
```bash
source ~/.zshrc
```

---

## Themes

### What Are Themes?

**Themes** change how your terminal prompt looks. The prompt is the text that appears before your cursor, like:

```
username@computer:~/Documents $
```

A theme can change:
- Colors
- What information is shown (username, directory, Git branch, etc.)
- Layout and formatting

### How to Change Your Theme

1. **Open your `.zshrc` file:**
   ```bash
   code ~/.zshrc
   ```

2. **Find the line that says `ZSH_THEME=`**

3. **Change the theme name:**
   ```bash
   ZSH_THEME="robbyrussell"  # Change "robbyrussell" to your preferred theme
   ```

4. **Reload your configuration:**
   ```bash
   source ~/.zshrc
   ```

### Popular Themes

Here are some popular themes to try:

**Simple and Clean:**
- `robbyrussell` - Default theme, simple and clean
- `af-magic` - Colorful but not overwhelming
- `bureau` - Minimal with useful info

**Feature-Rich:**
- `agnoster` - Shows Git branch, directory path, and more
- `powerlevel10k` - Very customizable, fast, and feature-rich
- `spaceship` - Modern, shows lots of useful information

**How to try a theme:**
1. Edit `~/.zshrc`
2. Change `ZSH_THEME="robbyrussell"` to `ZSH_THEME="agnoster"`
3. Run `source ~/.zshrc`
4. See how it looks!

### Disabling a Theme

If you want to use a different prompt tool (like Starship) instead:

```bash
ZSH_THEME=""  # Set to empty string to disable Oh My Zsh themes
```

---

## Plugins

### What Are Plugins?

**Plugins** are add-ons that add features to your terminal. They can:
- Add new commands
- Create shortcuts (aliases)
- Add autocomplete suggestions
- Provide helpful functions

### How to Enable Plugins

1. **Open your `.zshrc` file:**
   ```bash
   code ~/.zshrc
   ```

2. **Find the line that says `plugins=(...)`**

3. **Add plugin names inside the parentheses:**
   ```bash
   plugins=(git python docker)
   ```

4. **Reload your configuration:**
   ```bash
   source ~/.zshrc
   ```

### Popular Plugins

Here are some useful plugins to get started:

**Git Plugin** (usually enabled by default)
- Adds Git shortcuts like `gst` (git status), `ga` (git add), `gcmsg` (git commit -m)
- Shows Git branch in your prompt (if your theme supports it)
- Adds helpful Git aliases

**How to enable:**
```bash
plugins=(git)
```

**macOS Plugin**
- Adds macOS-specific shortcuts
- Helpful aliases for common macOS tasks

**How to enable:**
```bash
plugins=(git macos)
```

**Python Plugin**
- Adds Python-related aliases
- Helpful shortcuts for Python development

**How to enable:**
```bash
plugins=(git python)
```

**Docker Plugin**
- Adds Docker shortcuts
- Autocomplete for Docker commands

**How to enable:**
```bash
plugins=(git docker docker-compose)
```

**Other Useful Plugins:**
- `colored-man-pages` - Makes manual pages colorful and easier to read
- `command-not-found` - Suggests correct commands if you mistype
- `extract` - Extract any archive with just `extract filename`
- `z` - Jump to frequently used directories (type `z project` to go to a project folder)
- `zsh-autosuggestions` - Suggests commands as you type (needs separate installation)
- `zsh-syntax-highlighting` - Highlights commands as you type (needs separate installation)

**Example with multiple plugins:**
```bash
plugins=(
  git
  macos
  python
  docker
  docker-compose
  colored-man-pages
  command-not-found
  extract
  z
)
```

### What Each Plugin Does

**Git Plugin:**
- `gst` = `git status`
- `ga` = `git add`
- `gcmsg "message"` = `git commit -m "message"`
- `gp` = `git push`
- `gl` = `git pull`
- Shows current Git branch in prompt (if theme supports it)

**macOS Plugin:**
- `cdf` = cd to frontmost window of Finder
- `quick-look` = Quick look a file
- `man-preview` = Open man page in Preview app

**Python Plugin:**
- `py` = `python`
- `pyw` = `pythonw`
- `py2` = `python2`
- `py3` = `python3`

**Docker Plugin:**
- `dbl` = `docker build`
- `dcin` = `docker inspect`
- `dcls` = `docker ps`
- `dexec` = `docker exec`

**Extract Plugin:**
- Just type `extract filename.zip` or `extract filename.tar.gz`
- Automatically extracts any archive type

**Z Plugin:**
- Type `z project` to jump to a directory with "project" in the name
- Learns your frequently visited directories
- Much faster than typing full paths

---

## Common Configuration

### Complete Example Configuration

Here's a complete example `.zshrc` with Oh My Zsh:

```bash
# Path to your oh-my-zsh installation
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load
ZSH_THEME="robbyrussell"

# Which plugins would you like to load?
plugins=(
  git
  macos
  python
  docker
  docker-compose
  colored-man-pages
  command-not-found
  extract
  z
)

# Load Oh My Zsh
source $ZSH/oh-my-zsh.sh

# Your custom aliases (add your own here)
alias ll='ls -alF'
alias la='ls -A'
alias ..='cd ..'
```

### Understanding the Configuration

**`export ZSH="$HOME/.oh-my-zsh"`**
- Tells Oh My Zsh where it's installed
- Usually you don't need to change this

**`ZSH_THEME="robbyrussell"`**
- Sets which theme to use
- Change this to try different themes
- Set to `""` to disable themes

**`plugins=(...)`**
- List of plugins to load
- Add plugin names separated by spaces or new lines
- Order doesn't matter

**`source $ZSH/oh-my-zsh.sh`**
- This line loads Oh My Zsh
- Must be after theme and plugins configuration
- Don't remove this line!

---

## Advanced: Custom Themes and Plugins

### Custom Themes

You can create your own theme or install third-party themes:

1. **Create a custom theme directory:**
   ```bash
   mkdir -p ~/.oh-my-zsh/custom/themes
   ```

2. **Create your theme file:**
   ```bash
   code ~/.oh-my-zsh/custom/themes/my-theme.zsh-theme
   ```

3. **Set your theme:**
   ```bash
   ZSH_THEME="my-theme"
   ```

### Custom Plugins

You can create your own plugins:

1. **Create a custom plugin directory:**
   ```bash
   mkdir -p ~/.oh-my-zsh/custom/plugins
   ```

2. **Create your plugin:**
   ```bash
   mkdir -p ~/.oh-my-zsh/custom/plugins/my-plugin
   code ~/.oh-my-zsh/custom/plugins/my-plugin/my-plugin.plugin.zsh
   ```

3. **Add your plugin:**
   ```bash
   plugins=(git my-plugin)
   ```

### Installing Third-Party Plugins

Some popular plugins need separate installation:

**zsh-autosuggestions** (suggests commands as you type):
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Then add to plugins:
```bash
plugins=(git zsh-autosuggestions)
```

**zsh-syntax-highlighting** (highlights commands):
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Then add to plugins:
```bash
plugins=(git zsh-syntax-highlighting)
```

---

## Troubleshooting

### Problem: Oh My Zsh Not Loading

**Symptoms:** Terminal looks the same, no Oh My Zsh features

**Solution:**
```bash
# Check if Oh My Zsh is installed
ls -la ~/.oh-my-zsh

# Check your .zshrc
cat ~/.zshrc | grep oh-my-zsh

# Reload configuration
source ~/.zshrc
```

### Problem: Theme Not Changing

**Symptoms:** Changed theme name but nothing happened

**Solution:**
1. Check the theme name is correct (case-sensitive)
2. Make sure you reloaded: `source ~/.zshrc`
3. Check if theme file exists: `ls ~/.oh-my-zsh/themes/ | grep theme-name`

### Problem: Plugin Not Working

**Symptoms:** Added plugin but features don't appear

**Solution:**
1. Check plugin name is correct
2. Make sure you reloaded: `source ~/.zshrc`
3. Check if plugin exists: `ls ~/.oh-my-zsh/plugins/ | grep plugin-name`
4. Some plugins need additional setup (check plugin documentation)

### Problem: Terminal Starts Slowly

**Symptoms:** Terminal takes a long time to open

**Solution:**
- Remove unused plugins
- Some themes are slower than others (try a simpler theme)
- Consider using a faster prompt tool like Starship

### Problem: Conflicts with Other Tools

**Symptoms:** Errors or features not working

**Solution:**
- If using Starship, set `ZSH_THEME=""` to disable Oh My Zsh themes
- Some plugins conflict with each other - try disabling plugins one by one
- Check your `.zshrc` for conflicting configurations

---

## Uninstalling Oh My Zsh

If you want to remove Oh My Zsh:

```bash
# Uninstall Oh My Zsh
uninstall_oh_my_zsh

# Or manually:
rm -rf ~/.oh-my-zsh
rm ~/.zshrc
mv ~/.zshrc.pre-oh-my-zsh ~/.zshrc
```

This will restore your original `.zshrc` backup.

---

## Oh My Zsh vs. Other Tools

### Oh My Zsh vs. Starship

**Oh My Zsh:**
- More plugins and community features
- Themes are part of the framework
- Can be slower with many plugins
- More configuration options

**Starship:**
- Faster startup time
- More customizable prompt
- Works with any shell
- Simpler configuration

**Can you use both?** Yes! Use Oh My Zsh for plugins and set `ZSH_THEME=""` to use Starship for the prompt.

### Oh My Zsh vs. Plain .zshrc

**Oh My Zsh:**
- Pre-made themes and plugins
- Easier to get started
- Less control over details
- Larger configuration

**Plain .zshrc:**
- Full control
- Smaller and faster
- You write everything yourself
- More work to set up

---

## Quick Reference

### Common Commands

```bash
# Edit Oh My Zsh configuration
code ~/.zshrc

# Reload configuration
source ~/.zshrc

# List available themes
ls ~/.oh-my-zsh/themes

# List available plugins
ls ~/.oh-my-zsh/plugins

# Update Oh My Zsh
omz update

# Check Oh My Zsh version
omz version
```

### Common Git Shortcuts (from Git Plugin)

```bash
gst    # git status
ga     # git add
gaa    # git add --all
gcmsg  # git commit -m
gp     # git push
gl     # git pull
gco    # git checkout
gcb    # git checkout -b (create new branch)
gcm    # git checkout main
```

### Configuration Checklist

- [ ] Oh My Zsh installed
- [ ] Theme selected
- [ ] Plugins added
- [ ] Configuration reloaded
- [ ] Custom aliases added (optional)

---

## Next Steps

Now that you have Oh My Zsh set up:

1. **Try different themes**: Experiment to find one you like
2. **Add more plugins**: Explore the available plugins
3. **Customize further**: Add your own aliases and functions
4. **Learn the shortcuts**: Use the Git plugin shortcuts to speed up your workflow

---

## Related Guides

- **[Zsh Configuration (.zshrc)](zshrc.md)** - Learn about .zshrc configuration
- **[Homebrew Guide](homebrew.md)** - Installing development tools
- **[Conda Guide](conda.md)** - Python environment management
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

