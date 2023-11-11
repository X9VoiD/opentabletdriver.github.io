---
title: Windows Installation Guide
---

### Dependencies {#dependencies}

1. Install the [.NET 6 Desktop Runtime x64]({% link _sections/Framework.md %})

If you were previously using the standalone installer/updater (before v0.6), it is highly suggested that you switch
to the new method for installing OpenTabletDriver below.

---

### Installation {#installation}

If you are upgrading from an older version of OpenTabletDriver, it is important that you do not
install it on top of the old version and instead clean up the old directory or install it to its own
directory.

1. Download the [latest release]({{ site.otd_release_url }}/OpenTabletDriver.win-x64.zip). <small class="text-muted">(OpenTabletDriver.win-x64.zip)</small>
2. Extract the downloaded file into a folder of its own.\\
> Replace `<username>` with your username in the example below.
```
C:\Users\<username>\OpenTabletDriver
```
3. Run `OpenTabletDriver.UX.Wpf.exe` in the extracted directory.\\
> You can create a shortcut to this file, just make sure that the working directory points
to the extracted directory.

---

### Installation of WinUSB {#winusb}
Some tablets require Zadig's WinUSB installed on a device interface to interact with the tablet correctly. To figure out if your
tablet requires WinUSB, and if it does, which interface to install it on, carefully check the notes on [the supported list of tablets here]({% link _sections/Tablets.md %}).

**<u>Only install WinUSB if it is explicitly listed for your tablet. Most tablets do not require WinUSB.</u>**

1. If your tablet **does** require WinUSB download it from [here](https://github.com/pbatard/libwdi/releases/download/v1.5.0/zadig-2.8.exe).
2. Start Zadig.
3. Go to `Options > show all devices`.
4. Find your tablet with the correct interface number on the device list.
5. Click `Replace Driver.`

---

### Post-Installation {#post-install}
Take a look at the [FAQ]({% link _wiki/FAQ/Windows.md %}) if you encounter any problems.
