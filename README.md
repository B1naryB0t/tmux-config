# Tmux Configuration for Debian Linux

A comprehensive tmux configuration with modern plugins, optimized for Debian-based systems.

## Features

- **Leader Key**: `Ctrl+Space` for all tmux commands
- **Window Navigation**: Numbers 1-9 (instead of default 0-9)
- **System Clipboard Integration**: Seamless copy/paste with X11 clipboard
- **Flexible Navigation**: Both arrow keys and vim keybindings for window/pane navigation
- **Full Mouse Support**: Click to select panes, drag to resize, scroll through history
- **Quick Config Reload**: `Leader+r` to reload configuration
- **Rose Pine Moon Theme**: Beautiful, consistent theming
- **Enhanced Functionality**: Multiple productivity plugins

## Included Plugins

- **tmux-harpoon**: Quick project switching and bookmarking
- **tmux-tea**: Session management with fuzzy finding
- **rose-pine/tmux**: Rose Pine Moon colorscheme
- **tmux-better-mouse-mode**: Enhanced mouse functionality
- **tmux-yank**: Improved copy/paste operations
- **tmux-logging**: Save complete pane history and screen captures
- **tmux-resurrect**: Save and restore tmux sessions
- **tmux-thumbs**: Copy/open text hints (similar to vimium)

## Installation

### Prerequisites

```bash
# Update package list
sudo apt update

# Install required packages
sudo apt install tmux git xclip

# For better clipboard integration (optional)
sudo apt install xsel
```

### Quick Installation

1. **Clone this repository:**

   ```bash
   git clone https://github.com/B1naryB0t/tmux-config ~/.config/tmux
   cd ~/.config/tmux
   ```

2. **Create symlink to tmux config:**

   ```bash
   ln -sf ~/.config/tmux/tmux.conf ~/.tmux.conf
   ```

3. **Install TPM (Tmux Plugin Manager):**

   ```bash
   git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
   ```

4. **Start tmux and install plugins:**
   ```bash
   tmux new-session
   ```
   Then press `Ctrl+Space + I` (capital i) to install all plugins.

### Manual Installation

1. **Copy the tmux.conf to your home directory:**

   ```bash
   cp tmux.conf ~/.tmux.conf
   ```

2. **Install TPM:**

   ```bash
   git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
   ```

3. **Reload tmux configuration:**

   ```bash
   tmux source-file ~/.tmux.conf
   ```

4. **Install plugins:**
   Press `Ctrl+Space + I` in tmux to install all plugins.

## Key Bindings

### Basic Commands

| Key Binding  | Action         |
| ------------ | -------------- |
| `Ctrl+Space` | Leader key     |
| `Leader + r` | Reload config  |
| `Leader + :` | Command prompt |

### Windows

| Key Binding    | Action                  |
| -------------- | ----------------------- |
| `Leader + c`   | New window              |
| `Leader + X`   | Kill window (no prompt) |
| `Leader + 1-9` | Switch to window 1-9    |
| `Leader + n`   | Next window             |
| `Leader + p`   | Previous window         |
| `Leader + →`   | Next window             |
| `Leader + ←`   | Previous window         |
| `Leader + l`   | Last window             |

### Panes

| Key Binding                   | Action                  |
| ----------------------------- | ----------------------- |
| `Leader + -` or `Leader + "`  | Horizontal split        |
| `Leader + \|` or `Leader + %` | Vertical split          |
| `Leader + x`                  | Kill pane (no prompt)   |
| `Leader + h/j/k/l`            | Navigate panes (vim)    |
| `Leader + ↑/↓/←/→`            | Navigate panes (arrows) |
| `Leader + Ctrl + h/j/k/l`     | Resize panes (vim)      |
| `Leader + Ctrl + ↑/↓/←/→`     | Resize panes (arrows)   |

### Copy Mode

| Key Binding  | Action                           |
| ------------ | -------------------------------- |
| `Leader + [` | Enter copy mode                  |
| `Leader + ]` | Paste                            |
| `v`          | Begin selection (in copy mode)   |
| `y`          | Copy to clipboard (in copy mode) |

### Plugin-Specific Bindings

#### Tmux Harpoon

| Key Binding  | Action              |
| ------------ | ------------------- |
| `Leader + a` | Mark file/project   |
| `Leader + e` | Toggle harpoon menu |

#### Tmux Tea

| Key Binding  | Action       |
| ------------ | ------------ |
| `Leader + T` | Session menu |

#### Tmux Thumbs

| Key Binding      | Action               |
| ---------------- | -------------------- |
| `Leader + Space` | Activate thumbs mode |

#### Tmux Logging

| Key Binding          | Action                |
| -------------------- | --------------------- |
| `Leader + Shift + p` | Toggle logging        |
| `Leader + Alt + p`   | Save complete history |
| `Leader + Alt + c`   | Clear history         |

#### Tmux Resurrect

| Key Binding        | Action          |
| ------------------ | --------------- |
| `Leader + Alt + s` | Save session    |
| `Leader + Alt + r` | Restore session |

## Configuration Details

### Mouse Support

- Full mouse support enabled
- Click to select panes and windows
- Drag borders to resize panes
- Scroll wheel for history navigation
- Right-click context menus

### Clipboard Integration

The configuration uses `xclip` for clipboard integration on Debian systems. If `xclip` is not available, it falls back to `xsel`. Install the preferred clipboard utility:

```bash
# Primary option (recommended)
sudo apt install xclip

# Alternative option
sudo apt install xsel
```

### Visual Settings

- Rose Pine Moon colorscheme
- 256 color support with true color
- Custom status bar with useful information
- Window and pane borders with clear indicators

## Troubleshooting

### Colors Not Displaying Correctly

Add this to your shell profile (`.bashrc`, `.zshrc`, etc.):

```bash
export TERM=screen-256color
```

### Clipboard Not Working

Ensure `xclip` is installed and X11 forwarding is working:

```bash
sudo apt install xclip
echo "test" | xclip -selection clipboard
xclip -selection clipboard -o  # Should output "test"
```

### Plugins Not Loading

1. Verify TPM is installed: `ls ~/.tmux/plugins/tpm`
2. Reload config: `Leader + r`
3. Install plugins: `Leader + I`
4. If issues persist, restart tmux completely: `tmux kill-server && tmux`

### Mouse Not Working

Ensure your terminal emulator supports mouse reporting. Most modern terminals (gnome-terminal, konsole, xterm, etc.) support this by default.

### Session Restore Issues

If tmux-resurrect isn't saving/restoring properly:

1. Check that the save directory exists: `ls ~/.local/share/tmux/resurrect/`
2. Verify you're using the correct key bindings: `Leader + Alt + s` (save) and `Leader + Alt + r` (restore)
3. Ensure you have proper permissions to write to the save directory

## Debian-Specific Notes

### Terminal Recommendations

For the best experience on Debian, use:

- **GNOME Terminal** (default on GNOME)
- **Konsole** (default on KDE)
- **xterm** (lightweight option)
- **Alacritty** (modern GPU-accelerated option)

### Performance Optimization

For better performance on older Debian systems:

```bash
# Add to ~/.tmux.conf for older systems
set -g status-interval 5  # Reduce status update frequency
set -g history-limit 5000 # Reduce history if memory is limited
```

## Customization

The configuration is designed to be easily customizable. Edit `tmux.conf` and modify:

- **Colors**: Change the Rose Pine theme or customize colors
- **Key bindings**: Add or modify key mappings
- **Status bar**: Customize the information displayed
- **Plugin settings**: Adjust plugin-specific configurations

After making changes, reload with `Leader + r`.

## Support

If you encounter any issues specific to Debian or need help with the configuration, check the plugin documentation or create an issue in this repository.
