# linux-minimal

Minimal Hyprland desktop setup for **Arch Linux** and **Fedora**, with Noctalia, UWSM, greetd, and a curated set of Wayland applications. The target installed footprint is **under 5 GiB**.

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

1. Install Arch using **Archinstall** with the **Minimal** profile.
2. Configure the system components listed below during Archinstall.
3. Boot into the installed system, then install Git, clone the repository, and run the script:

```bash
sudo pacman -S --needed git
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./arch.sh
```

The script configures UFW rules to allow LocalSend ports `53317/tcp` and `53317/udp`; firewall enablement is expected to be handled by Archinstall.

#### Example Archinstall configuration

Use this as a reference, not a configuration that must be copied exactly.

| Archinstall option | Example value |
|---|---|
| Profile | Minimal |
| Network | NetworkManager (default backend) |
| Kernel | `linux` |
| Bootloader | systemd-boot |
| Timezone | Your local timezone |
| NTP | Enabled |
| Pacman | Color enabled |
| zram | Enabled, `zstd` |
| Bluetooth | Enabled |
| Audio | PipeWire |
| Power management | `power-profiles-daemon` |
| Firewall | UFW |
| Authentication | Root password set; one regular user configured |
| Disk layout | Archinstall default layout on the selected target drive |

This setup assumes NetworkManager, BlueZ, PipeWire, power management, UFW, a kernel, firmware, a bootloader, zram, and NTP are configured during Archinstall.

### Fedora

1. Boot the **Fedora Everything netinstall ISO**.
2. During installation, select **only the networking options**.
3. Create a normal user with `sudo` access and ensure the system has internet access.
4. Install Git if needed, then clone the repository and run:

```bash
sudo dnf install -y git
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./fedora.sh
```

The Fedora script uses DNF and configures the additional repositories and packages it needs.

## What the scripts configure

- Install required packages and repositories.
- Set up Hyprland, Wayland portals, audio, Bluetooth, power management, greetd, Noctalia Greeter, and UWSM as appropriate for each distribution.
- Deploy `.config/` and `.local/` into the target user's home.
- Update XDG user directories and deploy `Wallpapers/` to the configured Pictures directory (normally `~/Pictures/Wallpapers/`).
- Set application defaults and install JetBrains Mono Nerd Font system-wide.

## Repository layout

```text
linux-minimal/
├── .config/       # Desktop and application configuration
├── .local/bin/    # User scripts and utilities
├── Wallpapers/    # Deployed to the user's Pictures directory
├── arch.sh
├── fedora.sh
└── README.md
```

## Notes

- Review the relevant script before running it; it can install/remove packages, enable services, and change system configuration.
- The scripts are not intended for migrating or repairing an existing desktop.
- Fork the repository to customize package lists, scripts, and dotfiles.

## License

See the repository's license file.
