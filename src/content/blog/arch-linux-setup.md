---
title: "The Arch Linux Minimalist Setup"
description: "Why I spend more time configuring my window manager than actually working. Exploring Hyprland, Waybar, and the pursuit of the perfect dotfile."
pubDate: 2026-03-22
tags: ["arch", "code"]
---

# Arch Linux Setup

I finally did it. I nuked my install and started from scratch. This time, I’m sticking to the minimalist philosophy.

## Hyprland vs Sway

I chose Hyprland for the eye candy. The animations are just too smooth to pass up.

```bash
# My current hyprland config
exec-once = waybar & hyprpaper
```

## The Dotfiles

Everything is tracked in my git repo. Configuration is code.

- WM: Hyprland
- Terminal: Alacritty
- Shell: Zsh / Starship
- Editor: Neovim (obviously)

Happy hacking.
