# linux-minimal

Minimal Hyprland desktop setup for **Arch Linux** and **Fedora**, with Noctalia, UWSM, greetd, and a curated set of Wayland applications.

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

Both installers require internet access, a normal user account with `sudo` access, and this repository cloned locally. Run the relevant script from the repository root. These scripts target fresh installations, do not back up existing configuration, and may overwrite matching files.

### Arch Linux

1. Install Arch using **Archinstall** with the **Minimal** profile.
2. Configure a normal user and working network access.
3. Select the system components you want Archinstall to configure. This setup assumes NetworkManager, Bluetooth (BlueZ), PipeWire, power management, UFW, a kernel, firmware, a bootloader, zram, and NTP are configured during installation.
4. After booting into the installed system, clone this repository and run:

```bash
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./arch.sh
```

The script handles the desktop setup and installs `base-devel` and `git` as needed for its AUR bootstrap. It configures UFW rules but does not enable UFW; enablement is expected to be handled by the Archinstall setup.

#### Example Archinstall configuration

This is the author's configuration as an example, not a requirement to copy every setting.

| Archinstall option | Example value |
|---|---|
| Profile | Minimal |
| Network | NetworkManager (default backend) |
| Kernel | `linux` |
| Bootloader | systemd-boot |
| Timezone | `Asia/Kolkata` |
| NTP | Enabled |
| Pacman | Color enabled |
| zram | Enabled, `zstd` |
| Bluetooth | Enabled |
| Audio | PipeWire |
| Power management | `power-profiles-daemon` |
| Firewall | UFW |
| Authentication | Root password set; one regular user configured |
| Disk layout | Archinstall default layout on the selected target drive |

### Fedora

1. Boot the **Fedora Everything netinstall ISO**.
2. During installation, select **only the networking options**; leave the desktop and other software selection to the script.
3. Create a normal user with `sudo` access and ensure the installed system has working internet access.
4. Clone this repository and run:

```bash
git clone https://github.com/xulqarnaen/linux-minimal.git
cd linux-minimal
sudo bash ./fedora.sh
```

The Fedora script uses DNF and configures the additional repositories and packages it needs, including UFW.

## What the scripts configure

- Install the required packages and repositories.
- Set up Hyprland, Wayland portals, audio, Bluetooth, power management, greetd, Noctalia Greeter, and UWSM as appropriate for the distribution.
- Deploy `.config/` and `.local/` into the target user's home.
- Update XDG user directories and deploy `Wallpapers/` to the user's Pictures directory (normally `~/Pictures/Wallpapers/`).
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

- Read the relevant script before running it; it can install/remove packages, enable services, and change system configuration.
- The scripts are intended for fresh installations, not migration or repair of an existing desktop.
- Fork the repository to customize package lists, scripts, and dotfiles.

## License

See the repository's license file.
