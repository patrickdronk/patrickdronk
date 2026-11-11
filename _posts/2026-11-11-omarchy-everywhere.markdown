---
layout: post
title: "Omarchy Everywhere"
date: 2026-11-11 22:00:00 +0100
categories: engineering tooling
excerpt: "I got hyped about Omarchy, but I work on a Mac and my PC runs Windows. So I rebuilt its way of working on both."
---

<figure>
  <a href="{{ '/assets/images/omarchy-everywhere-desktop-4k.webp' | relative_url }}">
    <img src="{{ '/assets/images/omarchy-everywhere-desktop.webp' | relative_url }}" width="1920" height="1080" alt="A dark desktop with three tiled windows under a thin status bar: Neovim on the left, fastfetch reporting Arch Linux at the top right and btop below it. The focused window has a mint-green border.">
  </a>
  <figcaption>Windows 11. The terminals run Arch Linux through WSL2, and komorebi tiles the windows. Click for the full 4K version.</figcaption>
</figure>

That's my Windows PC. The story of how it got there starts with Linux.

<br>

## Hyped

[Omarchy](https://omarchy.org/) is DHH's opinionated Arch Linux distro, and it got me hyped for two reasons. It's fast. Every window tiles itself, apps and workspaces are one keystroke away, and the mouse mostly stays where it is. And it looks good. Pick a theme and the terminal, the editor and the status bar all change with it.

One problem. I work on a MacBook, and my desktop PC is where I play League of Legends, which doesn't run on Linux.

So switching wasn't an option. Copying how it works was.

<br>

## What I Actually Wanted

Take Linux out of Omarchy and a short list is left:

- One modifier key for everything. Mine is called Hyper and sits on the right Command key. `Hyper+H/J/K/L` moves between windows, `Hyper+Enter` opens a terminal, `Hyper+B` the browser.
- Tiling. Every window finds its own place.
- One command for the looks. `theme hackerman` recolors the terminal, the editor, the bar and the window borders in one go.
- A searchable cheatsheet of every shortcut, on `Hyper+/`.

I added one thing of my own, because I kept getting lost in ten numbered workspaces. Every app got a fixed home. Terminal and IDE on 1, browser on 2, chat on 3, music on 9. I don't have to remember the numbers, because each app's own key takes me there.

<br>

## Same Keys, Different Tools

The Mac came first. I started in April and settled on today's tools in June. This week the PC followed.

| | Mac | Windows |
|---|---|---|
| Tiling | yabai | komorebi |
| Shortcuts | skhd, Hammerspoon | one AutoHotkey script |
| Hyper key | Karabiner | the keyboard itself |
| Status bar | sketchybar | komorebi-bar |
| Launcher | Raycast | Raycast |
| Terminal | Ghostty | WezTerm, into Arch Linux on WSL2 |

The shell, tmux and Neovim aren't in that table because nothing differs there. Both machines read the same config files from the same repo.

The keyboard does much of the work. One Keychron serves both machines, with a separate layer for Windows. On that layer the key under my left thumb sends Control, so my Cmd+C and Cmd+V habits keep working, and Hyper is F24, a key that exists but that nothing uses. One AutoHotkey script listens for it and tells komorebi what to do.

<figure>
  <a href="{{ '/assets/images/omarchy-everywhere-cheatsheet.webp' | relative_url }}">
    <img src="{{ '/assets/images/omarchy-everywhere-cheatsheet.webp' | relative_url }}" width="1484" height="948" loading="lazy" alt="A dark window listing shortcuts in two columns, such as 'Focus window left' next to 'Hyper+H' and 'Close window' next to 'Hyper+Q'. Behind it, the tiled terminals.">
  </a>
  <figcaption>Hyper+/ on Windows. The Hyper binds in this list come from the same table as the hotkeys, so the two can&rsquo;t drift apart.</figcaption>
</figure>

<br>

## Two Days

The Windows side took two days, and I typed very little of it. Together with Claude Code I wrote down what had to feel identical and what was off limits. No driver may sit between the keyboard and the game, because League's anti-cheat is picky and I like my account. After that, Claude Code did the building on the PC. My part was the part only a person can do. I remapped the keyboard, pressed the keys and said whether it felt right.

It's not finished. Windows only knows one theme so far, and its bar is plainer than the one on the Mac. But the keys are the same on every machine now, and that was the point.

---

*This post was written with the help of AI, but the experiences and thoughts are my own.*
