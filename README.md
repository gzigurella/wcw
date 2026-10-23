# Clipboard toast for Wayland

A small `wl-paste --watch` helper that displays a desktop notification when the
regular Wayland clipboard changes. Wayland itself does not provide this notification;
this repository contains the user-session helper that implements it. It never includes clipboard contents in the
notification or writes them to disk.

The watcher runs for the whole Wayland session, so it also reports clipboard
changes from applications other than Kitty. Rapid changes are coalesced by the
desktop notification server using a synchronous notification hint.

## Requirements

- A Wayland compositor implementing the wlroots data-control protocol (Hyprland
  supports it)
- `wl-clipboard` (`wl-paste`)
- `libnotify` (`notify-send`)
- `flock`

## Run manually

```sh
./bin/watch-clipboard
```

The watcher stays in the foreground. Stop it with Ctrl+C.

## Hyprland autostart

Add this inside your Hyprland startup hook:

```lua
hl.exec_cmd("/path/to/wcw/bin/watch-clipboard")
```

The runtime lock prevents duplicate watcher instances.
