# 🔔 dunst-confirm

Confirmation alets with Dunst + keybinds. For the rest of who use WM setups and don't want to install all kinds of deps.

I use this script because I didn't like that swaynag forces you to click "Yes" instead of having a keyboard bind.

## ⚙️ Installation

### 1. Prerequisites

You must have the **Dunst notification daemon** installed and running on your system.

### 2. Make the Script Executable

Save the provided script content (see below) as a file named <code>dunst-confirm</code> (with no extension) and make it executable:

```
# Save the script content to dunst-confirm
# ...
chmod +x dunst-confirm
```

### 3. Install Globally

Move the executable script into your system's binary path, such as <code>/usr/local/bin</code> or <code>~/bin</code>, to make it accessible from any directory.

```
sudo mv dunst-confirm /usr/local/bin/
```

## 🚀 Basic Usage

The script requires two arguments: a message prompt and the command to execute if confirmed.

```
dunst-confirm "Are you sure you want to execute this command?" "echo 'You rock'"
```

### Example: Confirming System Shutdown

To create a notification asking if you want to power off the system:

```
dunst-confirm "System will POWEROFF!" "systemctl poweroff"
```

## ⌨️ Keybinding Setup (Recommended)

The script relies on <code>dunstify</code> to pause and wait for an action. To interact with the notification using your keyboard, you must bind two keys in your window manager's configuration file: one to **confirm** the action and one to **dismiss** the notification.

### Keybinding Logic

The script sends a notification with a specific action key (<code>confirm</code>) and then waits for the key name to be output by <code>dunstify</code>.

* **Confirm:** Your window manager keybind triggers `dunstctl action`, which executes the *default* action (`confirm`) on the **newest** notification. This signals the script to run the command.
* **Dismiss:** Your window manager keybind triggers `dunstctl close`, which closes the **newest** notification, causing the script to exit without running the command.

### Configuration Examples

Use your preferred window manager's configuration file (e.g., `~/.config/sway/config`, `~/.config/hypr/hyprland.conf`) to set up your keybinds. The examples use `Mod+Y` (Confirm) and `Mod+N` (Dismiss).

#### Sway / i3

In your `~/.config/sway/config` or `~/.config/i3/config`:

```
# Custom keybind for Dunst to Confirm the action
bindsym $mod+y exec dunstctl action

# Custom keybind for Dunst to Dismiss the notification
bindsym $mod+n exec dunstctl close
```

#### Hyprland

In your `~/.config/hypr/hyprland.conf`:

```
# Custom keybind for Dunst to Confirm the action
bind = $MOD, y, exec, dunstctl action

# Custom keybind for Dunst to Dismiss the notification
bind = $MOD, n, exec, dunstctl close
```
