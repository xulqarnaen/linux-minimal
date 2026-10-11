# linux-minimal

Minimal Hyprland desktop setup for **Arch Linux** and **Fedora**, with Noctalia, and a curated set of Wayland applications. The target installed footprint is **under 5 GiB** and **around 700MiB** RAM usage on idle.

## Components

| Area | Software |
|---|---|
| Desktop | Hyprland, Noctalia, UWSM |
| Login | greetd, Noctalia Greeter |
| Shell and terminal | Fish, Foot, Starship |
| Browser and files | Brave Origin, Nautilus |
| Editor and media | Neovim, mpv, imv, Evince |
| Capture and clipboard | GPU Screen Recorder, wl-clip-persist |
| Font | JetBrains Mono Nerd Font |
| Firewall | UFW |

## Prerequisites

Both installers require internet access, a normal user account with `sudo` access, and Git to clone this repository.

⚠️ **Fresh installs only.** The scripts do not back up existing configuration and may overwrite matching files.

## Installation

### Arch Linux

⚠️The script assumes NetworkManager, BlueZ, PipeWire, power management, and UFW are already setup during archinstall.

1. Install Arch using **Archinstall** with the **Minimal** profile with options above configured.
2. Boot into the installed system and run the script:

```bash
sudo pacman -S --needed git
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./arch.sh
```

The script configures UFW rules for LocalSend on `53317/tcp` and `53317/udp`. 


### Fedora

1. Boot the **Fedora Everything netinstall ISO**.
2. During installation, select **only the networking options**.
3. Boot into the installed system and run:

```bash
sudo dnf install -y git
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./fedora.sh
```

The Fedora script enables **three COPR repositories**:

- **`lionheartp/Hyprland`** — provides the Hyprland-related packages used by this setup, including the Noctalia/Hyprland package source.
- **`leloubil/wl-clip-persist`** — provides `wl-clip-persist`, which keeps Wayland clipboard contents available after the source application exits.
- **`atim/starship`** — provides the Starship shell prompt.

It also adds the **official Brave Origin RPM repository** to install `brave-origin`. RPM Fusion Free and Nonfree repositories are installed for multimedia packages, including `libavcodec-freeworld`. 

## What the scripts configure

- Install required packages and repositories.
- Set up Hyprland, Wayland portals, audio, Bluetooth, power management, greetd, Noctalia Greeter, and UWSM as appropriate for each distribution.
- Theme almost the entire system with Noctalia.
- Deploy `.config/` and `.local/` into the target user's home, and `Wallpapers/` into the user's Pictures directory.
- Set application defaults and install JetBrains Mono Nerd Font system-wide.

## Common keybindings

| Keybinding | Action |
|---|---|
| `Super + Space` | Open launcher |
| `Super + Enter` | Open terminal |
| `Super + Q` | Close focused window |
| `Super + E` | Open file manager |
| `Super + B` | Open browser |
| `Alt + Tab` | Cycle windows |
| `Super + Arrow keys` | Focus window in that direction |
| `Super + 1–0` | Switch to workspace 1–10 |
| `Super + Shift + 1–0` | Move window to workspace 1–10 |
| `Super + F` | Maximize focused window |
| `Super + Shift + F` | Fullscreen focused window |
| `Super + S` | Toggle scratchpad |
| `Print` | Screenshot a region |
| `Shift + Print` | Screenshot full screen |
| `Super + Alt + Space` | Open control center |
| `Super + Ctrl + V` | Open clipboard panel |
| `Super + Escape` | Open session menu |
| `Super + Ctrl + L` | Lock session |

## Repository layout

```text
linux-minimal/
├── .config/       # Desktop and application configuration
├── .local/bin/    # User scripts for webapp setups
├── Wallpapers/    # Deployed to the user's Pictures directory
├── arch.sh        # Arch Linux setup script
├── fedora.sh      # Fedora Linux setup script
└── README.md
```

## Notes

- Review the relevant script before running it; it can install/remove packages, enable services, and change system configuration.
- The scripts are not intended for migrating or repairing an existing desktop.
- Fork the repository to customize package lists, scripts, and dotfiles.

## License

See the repository's license file.
