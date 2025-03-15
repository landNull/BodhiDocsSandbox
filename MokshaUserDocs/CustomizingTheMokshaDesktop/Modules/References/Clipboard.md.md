---
title: Clipboard
summary: 
status: Reference
---
# Clipboard
This is a clipboard module we created for the Bodhi Linux's e17 fork, Moksha. Despite being developed for Moksha, it should work on any e17 Desktop _meeting the requirements below_.

Clipboard currently is a simple, basic features clipboard manager. It maintains a history of text copied to the clipboard from which you can choose with a bare minimum of configuration options. Our main ambition, aside from learning EFL and enlightenment module programming, was to make it light on system resources with no additional dependencies, integrate in a natural way with the e17/Moksha desktops and be a usable alternative to other clipboard managers (Parcellite, CopyQ, glipper etc.).

# Main Features

[](https://github.com/Obsidian-StudiosInc/clipboard#main-features)

[![](https://camo.githubusercontent.com/e766d15605b1ef753b93a5f23c5a4c4de75dd6211bf7a281cea4875f5e9a1c1f/687474703a2f2f692e696d6775722e636f6d2f303036735a78422e706e67)](http://i.imgur.com/006sZxB.png)

- Text only clipboard management. Sorry no image support.
- Stores a clipboard history of customizable length.
- Clipboard contents are preserved even when you close applications
- Uses either or both Primary or Clipboard clipboards.
- Synchronize clipboards.
- Several View options to display items the way you like.
- Global hotkeys with configurable e17/Moksha key bindings.
- Functions with or without a gadget added to the desktop or a shelf.
- Does not need or use a system tray.