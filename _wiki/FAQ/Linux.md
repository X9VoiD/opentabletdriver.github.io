---
title: "Linux FAQ"
hide_from_auto_list: true
---

**It is recommended that you check [General FAQ]({% link _wiki/FAQ/General.md %})
first before continuing.**

Also check out [Linux App Specific FAQ]({% link _wiki/FAQ/LinuxAppSpecific.md %}) for app-specific instructions.

### Troubleshooting {#troubleshooting}

#### Common Problems

If your tablet is connected properly and is supported, but is still not detected, [check logs]({% link _wiki/Documentation/Logs.md %}) for any errors or warnings. If you find any, try finding for a match and its accompanying solution below:

##### UCLogic kernel module is loaded {#hid_uclogic}

_Symptoms_

```
Another tablet driver found: UC Logic
```

```
ArgumentOutOfRangeException: Value range is [0, 15]. (Parameter 'value)
```

[_Solution_]({% link _wiki/Documentation/UdevRules.md %})

##### Insufficient permissions {#udev}

_Symptoms_

```
Not permitted to open HID class device at /dev/hidrawX
```

[_Solution_]({% link _wiki/Documentation/UdevRules.md %})

#### Tablet-specific Troubleshooting

##### Wacom CTL-x100

It is possible for Wacom CTL-x100 tablets to boot in Android mode (the mode they use when interfacing with android devices like phones) instead of PC mode in some rare cases. To fix this, press
the outer 2 express keys for 3-4 seconds until the LEDs change brightness. This toggles the tablet's operating mode
between PC (high LED brightness) and Android mode (low LED brightness).

> If you are sure your tablet is in PC mode, proceed [here](#troubleshooting).

---

### Tablet is detected but not working?

#### Fresh Install {#fail-virtual-device}

If this is a fresh install and you have not configured your tablet yet, [check logs]({% link _wiki/Documentation/Logs.md %}) for any errors or warnings. If you find any, try finding for a match and its accompanying solution below:

##### Missing uinput device

_Symptoms_

```
Failed to initialize virtual tablet. (error code ENODEV)
```

_Solution_

Reboot your computer.

##### Missing uinput device support

_Symptoms_

```
Failed to initialize virtual tablet. (error code ENOENT)
```

_Solution_

Make sure that your kernel has uinput support. If you are using a custom kernel or builds kernel from source, make sure that you have enabled `CONFIG_INPUT_UINPUT` in your kernel configuration. Refer to your distro's documentation regarding kernel configuration.

##### Missing uinput device permissions

_Symptoms_

```
Failed to initialize virtual tablet. (error code EACCES)
```

[_Solution_]({% link _wiki/Documentation/UdevRules.md %})

#### Non-fresh Install

Try disabling your filters one-by-one and see if input finally works.

#### It doesn't work in a specific application

Visit our wiki page for app-specific instructions [here]({% link _wiki/FAQ/LinuxAppSpecific.md %}).

---

### My cursor is going crazy! It teleports everywhere!

See [here]({% link _wiki/FAQ/General.md %}#emi-interference).

---

### Tablet is working but there is no pressure {#artist-mode}

Pressure support is available by changing the output mode of OpenTabletDriver to Artist Mode:

- Change output mode (at the bottom left of OpenTabletDriver) to Artist Mode.
- Remove Tip Binding in the Pen Settings panel by opening advanced binding editor (press '...' next to the binding), then press "Clear".
- Save your settings and then try drawing in an application that supports pressure.

You will also need to use artist mode mouse bindings in the advanced binding editor instead of regular mouse buttons. Regular mouse buttons are _not_ supported in artist mode.

---

### The daemon does not start on boot

#### systemd {#systemd-autostart}

Make sure that you have enabled the systemd service:

```bash
systemctl user enable opentabletdriver.service --now
```

If this does not work, this means that the desktop environment is not configured correctly to integrate with systemd. In such case, refer to your desktop environment's documentation on how to autostart processes on login. The command to execute on login is:

```bash
otd-daemon
```

#### Other init systems

OpenTabletDriver offers no official support for other init systems. Refer to your init system's documentation on how to autostart processes on login. The command to execute on login is:

```bash
otd-daemon
```

> This command should be run as user, not root.

---

### The cursor feels slow on Artist Mode {#libinput-smoothing}

Using artist mode will result in some minor smoothing due to libinput's tablet handling.

To disable this smoothing, add the contents below to `/etc/libinput/local-overrides.quirks`:

```ini
[OpenTabletDriver Virtual Tablet]
MatchName=OpenTabletDriver*
AttrTabletSmoothing=0
```

You should restart the OpenTabletDriver daemon after updating this file.

---

### Still have problems? {#discord}

If you are still encountering problems with OpenTabletDriver, it will be easier to help you over in our [Discord]({{ site.discord_invite_url }}) server. We will guide you in doing certain debugging steps and will give you different instructions to help resolve your problem.
