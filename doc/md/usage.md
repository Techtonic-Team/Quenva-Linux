# Usage

Head to the **[Ubuntu wiki](https://wiki.ubuntu.com)** and **[Quenva Linux Documentation](README.md)** for information on how to use your system, notably:

 - [Package management](https://help.ubuntu.com/community/InstallingSoftware) (installing/removing/upgrading software)
 - [Software Center](https://help.ubuntu.com/community/UbuntuSoftwareCenter)
 - [Wayland Environment](https://wiki.ubuntu.com/Wayland)

See the package lists in the sidebar for useful links about installed software.


## Maintenance & security

 * Only install software from trusted sources:
   - Official package repositories
   - Flatpak applications from Flathub
   - Distrobox containers
 * Backup your data periodically to an external storage using [Back In Time](https://backintime.readthedocs.io/en/latest/quick-start.html)
 * Only enter your administrator password to perform necessary system administration tasks
 * Use strong (long) passwords/phrases, do not reuse passwords for different services (use the [KeepassXC](https://keepassxc.org/) password manager), use secure network protocols (HTTPS, ...), use disk encryption
 * Security updates will be applied automatically through the Ubuntu update system
 * Keep your hardware in good condition


## Keyboard shortcuts

_Note: The `Super` key is also known as the Windows key._

- `Super + Space`: Applications menu
- `Super + I`: Web browser
- `Super + E`: File manager
- `Super + F`: Search files
- `Super + S`: Mute/unmute volume
- `Super + T`: Terminal
- `Super + R`: Run command
- `Super + L`: Lock session
- `Super + Q`: Shutdown/suspend/restart/logout...
- `Super + M`: E-mail client
- `Super + P`: Display settings
- `Super + Pause`: Settings manager
- `Ctrl + Alt + Delete`: Task manager
- `Alt + Mouse wheel`: Zoom
- `Win + Left`: Tile window left
- `Win + Right`: Tile window right
- `Win + Up`: Tile window top right
- `Win + Down`: Tile window bottom right


## See also

These projects can help you run Free and Open Source software on other devices.

- [LineageOS](https://lineageos.org/) - A Free and Open Source operating system for mobile devices, based on Android.
- [F-Droid](https://f-droid.org/) - A catalogue of Free and Open Source Software applications for the Android platform.
- [xsrv](https://xsrv.readthedocs.io/en/latest/) - Install, manage and run self-hosted network services and applications on your own server(s).


## Issues

* [TODO.md](TODO.md)
* [Gitlab issue tracker](https://gitlab.com/nodiscc/debian-live-config/-/issues)
* [Debian bug tracker (BTS)](https://wiki.debian.org/BTS)

# Using Quenva Linux

## Desktop Environment

Quenva Linux uses KDE Plasma, a modern and customizable desktop environment:

- **System Settings**: Configure every aspect of your system
- **Discover**: Install and manage software
- **KRunner**: Press Alt+Space to quickly launch applications and search
- **Activities**: Organize your work in different contexts
- **Widgets**: Add functionality to your desktop and panels

## Software Management

### Using Discover

1. Open Discover from the application menu
2. Browse categories or search for software
3. Click Install/Remove to manage applications
4. Keep your system updated through the Updates tab

### Using the Terminal

```bash
# Update package list
sudo apt update

# Upgrade installed packages
sudo apt upgrade

# Install new software
sudo apt install package-name

# Remove software
sudo apt remove package-name
```

## System Customization

### Appearance
- **System Settings** → **Appearance**
  - Choose themes, colors, and icons
  - Configure fonts and effects
  - Set up window decorations

### Desktop Layout
- Right-click panel → **Edit Panel**
- Add widgets with right-click → **Add Widgets**
- Configure multiple virtual desktops

### Keyboard and Mouse
- Configure shortcuts in **System Settings** → **Shortcuts**
- Set up mouse gestures and behavior

## File Management

- **Dolphin**: Main file manager
  - F4 to open terminal panel
  - Split views with F3
  - Configure view options

## Security and Updates

- Updates are managed through Discover
- Firewall configuration via plasma-firewall
- AppArmor profiles for enhanced security
- Regular backups with Kup

## Network Configuration

- Use plasma-nm for network management
- Configure VPN connections
- Bluetooth management with Bluedevil

## Getting Help

- Access built-in help with Alt+F2, type "help"
- Visit [Quenva Linux Documentation](https://docs.quenva.org)
- KDE Plasma documentation at [KDE UserBase](https://userbase.kde.org)
