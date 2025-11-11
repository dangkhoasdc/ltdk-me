---
layout: "post.njk"
title: "Why Ubuntu on Windows?"
date: 2018-04-28
tags:
    - misc
---

>[!caution]
> This article was written in 2017. Some information may be outdated.
> Nowadays, WSL2 is available with better performance and full Linux kernel support.

For programming purposes, I prefer Linux to Windows. However, Windows is
really good at entertainment and office work. Besides, Microsoft Office is the
best office suite I have ever experienced, and OneNote is one of my favorite
note-taking software. Not to mention my beloved Blizzard games such as Diablo,
Starcraft and other video games.

A solution to integrate Windows and Linux in one machine is
to install dual-boot. However, I am tired of switching between 2 OSs.
In addition, we have to configure the systems so that it can easily transfer
files between 2 different partition formats.

Another workaround is to run Windows or Linux on a virtual machine.
Since I usually play video games, I could not use Windows as a client.
Running Linux virtually seems promising. Unfortunately, my laptop is not strong
enough to run the virtual machine smoothly.

Finally, M$ comes up with a new feature in Windows 10 named
['Windows Subsystem for Linux'](http://wsl-guide.org/en/latest/). Surprisingly,
it works flawlessly except for several minor issues.

# Settings

1. Turn Windows Subsystem On: find `Windows features` and
select `Windows Subsystem for Linux`, wait for the installation and
restart.
2. Open Windows Store and install Ubuntu.
I also saw OpenSuse on the store.
Hopefully, there will be more distros adapted in the future,
especially Arch Linux/Manjaro which is my favorite.

3. After working around with Ubuntu and Tmux in `cmder`, I have found out
that [wsltty](https://github.com/mintty/wsltty) is the best tool to avoid
fonts broken, key arrow issues. Besides, it runs faster
than `cmder` although `cmder` has many useful features.

Here is the result:

![](https://static.notion-static.com/67ecfe6abf0242199ffec19dd227a000/Untitled)

There are several tips:

- Change the cursor to block.
- Turn off the mouse support feature in vim (`:set mouse=`) in order to copy
text from Windows to vim.
- Copy from vim to Windows applications:
    1. Install xsel/xclip on Ubuntu.
    2. Install [Xming](https://sourceforge.net/projects/xming/)
    3. Set `export DISPLAY=:0` in the bashrc or zshrc

# Installing ArchLinux on WSL

After several months waiting for a better solution, finally I found [ArchWSL](https://github.com/yuk7/ArchWSL)
which is easy to install and full of configuration. In addition, it turns out
that `wsltty` is not a tool I really want since there are still some issues with
Unicode font and delay. Now I am using `xfce4-terminal` with the help from
Xming.

With a few steps we are able to run xfce4-terminal directly from Windows:

1. [Set Xming to run on startup](https://tunecomp.net/add-program-to-startup-windows-10/).
2. Use the following command in Run to execute `xfce4-terminal`:

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -windowstyle hidden -Command "iex \"path\to\arch.exe run DISPLAY=:0 xfce4-terminal\""
```

# Windows Defender

It is so annoying that I have to turn it off. Somehow, the program always scans
the Linux folder. Eventually, everything in Subsystem runs so slow. A better
workaround is to add the Linux folder to the exclusion list of Windows Defender.
