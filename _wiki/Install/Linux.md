---
title: Linux Installation Guide
---

### Ubuntu / Debian {#debian}
 1. Download the [latest release]({{ site.otd_release_url }}/OpenTabletDriver.deb) <small class="text-muted">(OpenTabletDriver.deb)</small>
 2. Run the following commands in a terminal

> This assumes that you are in the directory in which you downloaded OpenTabletDriver to.

```sh
# Update the package list
sudo apt update

# This will install the package, assuming you are in the correct directory
sudo apt install ./OpenTabletDriver.deb

# Reload the systemd user unit daemon
systemctl --user daemon-reload

# Enable and start the user service
systemctl --user enable opentabletdriver --now
```

If you have the Microsoft dotnet repository installed you will have to either make sure you are not using any packages from that repository or use everything dotnet based off that. Mixing packages from different repositories will cause libhostfxr issues. If you are experiencing these see these solutions from Microsoft [here](https://learn.microsoft.com/en-us/dotnet/core/install/linux-package-mixup#solutions) and remove the Microsoft repositories and packages.

---

### Arch Linux {#arch}
 1. Use an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers) to install the `opentabletdriver` AUR package.
 2. Run the following commands in a terminal

```sh
# Reload the systemd user unit daemon
systemctl --user daemon-reload
# Enable and start the user service
systemctl --user enable opentabletdriver --now
```

Alternatively, you can install `opentabletdriver` without an AUR helper.

#### Enabling the OpenTabletDriver service

- Run the following commands in a terminal to install and enable the OpenTabletDriver service.

```sh
# Downloads the pkgbuild from the AUR.
git clone https://aur.archlinux.org/opentabletdriver.git
# Changes into the correct directory and installs OpenTabletDriver
cd opentabletdriver && makepkg -si
# Clean up leftovers
cd ..
rm -rf opentabletdriver
# Reload the systemd user unit daemon
systemctl --user daemon-reload
# Enable and start the user service
systemctl --user enable opentabletdriver --now
```

---

### Gentoo {#gentoo}
1. Add Guru overlay\\
> This is only required if you don't already have the Guru overlay configured
```bash
# Enable guru repository
sudo eselect repository enable guru
sudo emerge --sync guru
```

2. Edit `/etc/portage/package.accept_keywords` and add this line
```
x11-drivers/OpenTabletDriver-bin ~amd64
```

3. Run the following command
```bash
# Install the OpenTabletDriver package
sudo emerge OpenTabletDriver-bin
```

---

### NixOS {#nixos}
1. Edit `/etc/nixos/configuration.nix` and add this in your configuration\\
> More configuration options can be found [here](https://search.nixos.org/options?query=opentabletdriver)
```nix
# Enable OpenTabletDriver
hardware.opentabletdriver.enable = true;
```

---

### Post-Installation {#post-install}
Take a look at the [FAQ]({% link _wiki/FAQ/Linux.md %}) if you encounter any problems.
