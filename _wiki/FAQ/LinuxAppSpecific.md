---
title: Linux App-specific FAQ
---

### osu!stable

#### osu! is not detecting input from my tablet (Wayland)

Do not use `Absolute Mode` as your output mode. Use `Artist Mode` instead. Wine and XWayland currently has issues with parsing absolute mouse input.

Please do note that libinput adds smoothing on top of `Artist Mode` by default. See [here]({% link _wiki/FAQ/Linux.md %}#libinput-smoothing) for more information on how to remove the smoothing.

---

### osu!Lazer

#### My cursor is stuck (Wayland) {#osu-lazer-broken-input-wayland}

Make sure you set the `SDL_VIDEODRIVER` to `wayland`. Some examples:

```bash
env SDL_VIDEODRIVER=wayland ./osu.AppImage
```

```bash
env SDL_VIDEODRIVER=wayland osu-lazer
```
