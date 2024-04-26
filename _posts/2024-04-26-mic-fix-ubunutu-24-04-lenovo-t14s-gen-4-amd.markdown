---
layout: post
title:  "Internal Mic Fix for Lenovo T14s Gen 4 w/ AMD on Ubuntu 24.04"
date:   2024-04-26 00:00:00 -0800
tags: ubuntu linux lenovo amd ryzen 7840U t14s
---

I recently purchased a Lenovo T14s Gen 4 with the Amd Ryzen 7840u and loaded the brand new LTS version of Ubuntu on it, 24.04. To my dismay the internal microphone was not recognized at all in any of the sound settings. Finding a solution took a couple hours of reading logs and Googling so I'm putting that knowledge here to helpfully help anyone else in the same situation.

## The Issue
In the Ubuntu setting I was unable to find any recording devices. However, running the command: `lspci -knn | grep Audio` I was able to see three devices. Notably I saw:
```
c3:00.5 Multimedia controller [0480]: Advanced Micro Devices, Inc. [AMD] ACP/ACP3X/ACP6x Audio Coprocessor [1022:15e2] (rev 63)
	Subsystem: Lenovo ACP/ACP3X/ACP6x Audio Coprocessor [17aa:50d8]
```

This is the internal microphone for the laptop. 

## The Fix
Getting it working ended up being fairly trivial once I found the solution. Specifically [this post on the Archlinux Forums](https://bbs.archlinux.org/viewtopic.php?id=294307). The answer is to add a file to `/etc/modules-load.d/` in order to load the correct kernel modules for the internal mic. The exact command the author of the post gave (which worked great for me) is:
```
echo -e "snd-pci-ps\nsnd-soc-ps-mach" | sudo tee /etc/modules-load.d/sound.conf > /dev/null
```
After that I rebooted, and my mic is working great.
