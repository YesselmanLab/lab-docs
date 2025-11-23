# iTerm2 Guide

iTerm2 is a powerful terminal emulator for macOS that provides a superior alternative to the default Terminal app. It offers advanced features like split panes, search, autocomplete, and extensive customization options.

---

## What is iTerm2?

iTerm2 is a replacement for Terminal and the successor to iTerm. It's a terminal emulator that provides:
- **Split panes**: Work with multiple terminal sessions side-by-side
- **Search**: Find text in terminal output quickly
- **Autocomplete**: Intelligent command completion
- **Customization**: Extensive theming and configuration options
- **Hotkeys**: Powerful keyboard shortcuts for productivity
- **Session management**: Save and restore terminal sessions

---

## Installation

### Using Homebrew (Recommended)

```bash
# Install iTerm2
brew install --cask iterm2
```

### Manual Installation

1. Visit [iTerm2's official website](https://iterm2.com/)
2. Download the latest version
3. Extract and drag iTerm2 to your Applications folder
4. Launch iTerm2 from Applications

### First Launch Setup

On first launch, iTerm2 will ask if you want to:
- **Set iTerm2 as the default terminal**: Recommended for better experience
- **Install shell integration**: Enables advanced features like command history and status bar

---

## Basic Usage

### Opening iTerm2

```bash
# Open from command line
open -a iTerm

# Or use Spotlight (Cmd+Space) and type "iTerm2"
```

### Creating New Windows and Tabs

- **New Window**: `Cmd+N`
- **New Tab**: `Cmd+T`
- **Close Tab**: `Cmd+W`
- **Switch Tabs**: `Cmd+1`, `Cmd+2`, etc. or `Cmd+{` / `Cmd+}`

### Split Panes

One of iTerm2's most powerful features is split panes:

- **Split Vertically**: `Cmd+D`
- **Split Horizontally**: `Cmd+Shift+D`
- **Navigate Between Panes**: `Cmd+[` / `Cmd+]` or `Cmd+Option+Arrow Keys`
- **Close Pane**: `Cmd+W` (when pane is focused)
- **Maximize Pane**: `Cmd+Shift+Enter` (toggle)

---

## Essential Configuration

### Accessing Preferences

- **Preferences**: `Cmd+,` (or iTerm2 → Preferences)

### Recommended Settings

#### General Settings

1. **Preferences → General → Magic**
   - Enable "Enable Magic" for better shell integration
   - Enable "Enable Python API" if you use Python scripts

2. **Preferences → General → Selection**
   - Enable "Copy to pasteboard on selection" (auto-copy)
   - Enable "Applications in terminal may access clipboard"

#### Profiles

1. **Preferences → Profiles → General**
   - Set default working directory
   - Configure startup command if needed

2. **Preferences → Profiles → Colors**
   - Choose a color scheme (or import custom ones)
   - Popular schemes: Solarized Dark, Dracula, One Dark

3. **Preferences → Profiles → Text**
   - Set font size (recommended: 12-14pt)
   - Choose a font (popular: Monaco, Menlo, Fira Code, JetBrains Mono)
   - Enable ligatures if using a font that supports them

4. **Preferences → Profiles → Keys**
   - Configure keyboard shortcuts
   - Set up key mappings for common actions

#### Window Settings

1. **Preferences → Profiles → Window**
   - Configure transparency (optional)
   - Set window appearance
   - Configure margins and padding

---

## Advanced Features

### Search

- **Search**: `Cmd+F` opens search bar
- **Find Next**: `Cmd+G`
- **Find Previous**: `Cmd+Shift+G`
- **Search in all tabs**: Enable in search options

### Autocomplete

iTerm2 can autocomplete commands, file paths, and more:

- **Trigger**: `Cmd+;` or `Cmd+Shift+;`
- **Navigate suggestions**: Arrow keys
- **Select**: Enter

### Command History

With shell integration enabled:

- **View command history**: `Cmd+Shift+H`
- **Browse history**: Use arrow keys in history view
- **Re-run command**: Select and press Enter

### Status Bar

The status bar shows useful information at the top of each terminal:

1. **Preferences → Profiles → Session → Status bar enabled**
2. Configure components:
   - CPU usage
   - Memory usage
   - Git branch (if in a git repo)
   - Current directory
   - Time
   - Custom components

### Hotkey Window

Create a hotkey to show/hide iTerm2 from anywhere:

1. **Preferences → Keys → Hotkey**
2. Enable "Show/hide all windows with a system-wide hotkey"
3. Set your preferred hotkey (e.g., `Cmd+Option+I`)

### Shell Integration

Shell integration provides enhanced features:

```bash
# Install shell integration (if not done during first launch)
curl -L https://iterm2.com/shell_integration/zsh -o ~/.iterm2_shell_integration.zsh

# Add to ~/.zshrc
echo 'source ~/.iterm2_shell_integration.zsh' >> ~/.zshrc
source ~/.zshrc
```

Benefits:
- Command history tracking
- Status bar integration
- Better session management
- Improved autocomplete

---

## Productivity Tips

### 1. Use Profiles for Different Environments

Create profiles for different use cases:

- **Default**: Your everyday terminal
- **SSH**: Pre-configured for remote servers
- **Python**: Activate conda environment on startup
- **Project-specific**: Auto-cd to project directory

**Create a new profile:**
1. Preferences → Profiles → Other Actions → New Profile
2. Configure settings
3. Set as default or use via Profiles menu

### 2. Keyboard Shortcuts

Customize shortcuts in **Preferences → Keys → Key Bindings**:

Common useful shortcuts:
- `Cmd+Option+E`: Open new editor window
- `Cmd+Option+B`: Open new browser window
- `Cmd+Option+T`: New tab
- `Cmd+Option+Arrow`: Navigate panes

### 3. Use Triggers for Automation

Triggers can perform actions based on terminal output:

1. **Preferences → Profiles → Advanced → Triggers**
2. Add trigger:
   - **Regular Expression**: Pattern to match
   - **Action**: What to do (e.g., highlight, sound, notification)

Example: Highlight errors in red:
- Regex: `.*ERROR.*`
- Action: Highlight text (red background)

### 4. Session Restoration

iTerm2 can restore your sessions after restart:

1. **Preferences → General → Startup**
2. Enable "Restore window contents"
3. Sessions will be saved and restored automatically

### 5. Use tmux Integration

iTerm2 has built-in tmux integration:

1. **Preferences → General → Magic**
2. Enable "Enable tmux integration"
3. Use tmux normally - iTerm2 will provide native integration

---

## Color Schemes and Themes

### Installing Color Schemes

1. Visit [iTerm2 Color Schemes](https://iterm2colorschemes.com/)
2. Download a scheme
3. **Preferences → Profiles → Colors → Color Presets → Import**
4. Select the downloaded `.itermcolors` file
5. Choose from **Color Presets** dropdown

### Popular Color Schemes

- **Solarized Dark/Light**: Classic, easy on the eyes
- **Dracula**: Modern dark theme
- **One Dark**: Based on Atom editor theme
- **Nord**: Arctic, north-bluish color palette
- **Gruvbox**: Retro groove color scheme

### Creating Custom Themes

1. **Preferences → Profiles → Colors**
2. Customize each color element
3. **Color Presets → Save Current Color Preset**
4. Name and save your theme

---

## Integration with Other Tools

### Oh My Zsh

iTerm2 works seamlessly with Oh My Zsh:

```bash
# Install Oh My Zsh (if not already installed)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Popular themes that work well with iTerm2:
# - powerlevel10k
# - agnoster
# - spaceship
```

### Conda Environments

Display conda environment in status bar:

1. Install shell integration (see above)
2. Status bar will automatically show active conda environment
3. Or use Oh My Zsh conda plugin

### Git Integration

Status bar can show git branch and status:

1. Enable shell integration
2. Add "Git State" component to status bar
3. Shows branch name and status when in git repository

---

## Troubleshooting

### Issue: Colors Not Displaying Correctly

**Problem**: Terminal colors look wrong

**Solution**:
1. Check your color scheme in Preferences → Profiles → Colors
2. Ensure your shell's color settings match (e.g., `$TERM` variable)
3. Try a different color scheme

### Issue: Shell Integration Not Working

**Problem**: Command history or status bar not working

**Solution**:
```bash
# Reinstall shell integration
curl -L https://iterm2.com/shell_integration/zsh -o ~/.iterm2_shell_integration.zsh

# Ensure it's sourced in ~/.zshrc
echo 'source ~/.iterm2_shell_integration.zsh' >> ~/.zshrc
source ~/.zshrc
```

### Issue: Font Ligatures Not Working

**Problem**: Font ligatures (like `->` becoming `→`) not showing

**Solution**:
1. Use a font that supports ligatures (Fira Code, JetBrains Mono, etc.)
2. **Preferences → Profiles → Text**
3. Enable "Use ligatures" checkbox
4. Restart iTerm2

### Issue: Slow Performance

**Problem**: iTerm2 is slow or laggy

**Solution**:
1. **Preferences → Advanced → Performance**
2. Disable GPU acceleration if causing issues
3. Reduce transparency
4. Limit scrollback buffer size
5. Disable unused features

### Issue: Hotkey Not Working

**Problem**: Hotkey window doesn't appear

**Solution**:
1. Check if hotkey conflicts with system shortcuts
2. **Preferences → Keys → Hotkey**
3. Try a different hotkey combination
4. Ensure "Show/hide all windows" is enabled

---

## Best Practices

### 1. Regular Updates

Keep iTerm2 updated for bug fixes and new features:

```bash
# Check for updates
brew upgrade --cask iterm2

# Or: iTerm2 → Check for Updates
```

### 2. Backup Your Configuration

iTerm2 stores preferences in:
- `~/Library/Preferences/com.googlecode.iterm2.plist`

Backup this file to restore settings:

```bash
# Backup
cp ~/Library/Preferences/com.googlecode.iterm2.plist ~/iterm2-backup.plist

# Restore
cp ~/iterm2-backup.plist ~/Library/Preferences/com.googlecode.iterm2.plist
```

### 3. Use Profiles for Organization

Create profiles for:
- Different projects
- SSH connections
- Different environments (dev, staging, prod)
- Different shells (zsh, bash, fish)

### 4. Customize Keyboard Shortcuts

Tailor shortcuts to your workflow:
- Map common actions to easy-to-reach keys
- Use consistent shortcuts across applications
- Document your custom shortcuts

### 5. Leverage Split Panes

Use split panes for:
- Running multiple commands simultaneously
- Monitoring logs while working
- Comparing outputs side-by-side
- Running servers and clients together

---

## Quick Reference

### Essential Keyboard Shortcuts

```
Cmd+N          New window
Cmd+T          New tab
Cmd+W          Close tab/pane
Cmd+D          Split vertically
Cmd+Shift+D    Split horizontally
Cmd+[ / Cmd+]  Navigate between panes
Cmd+Shift+Enter  Maximize pane (toggle)
Cmd+,          Preferences
Cmd+F          Search
Cmd+G          Find next
Cmd+;          Autocomplete
Cmd+Shift+H    Command history
```

### Configuration Files

```
Preferences:   ~/Library/Preferences/com.googlecode.iterm2.plist
Profiles:      Stored in preferences plist
Color Schemes: ~/Library/Application Support/iTerm2/DynamicProfiles/
```

---

## Related Guides

- **[Oh My Zsh Guide](oh-my-zsh.md)** - Enhance your shell with themes and plugins
- **[Zsh Configuration Guide](zshrc.md)** - Configure your shell environment
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics
- **[Development Environment Setup](../development-environment.md)** - Complete macOS setup guide

---

*Last updated: {{ git_revision_date_localized }}*

