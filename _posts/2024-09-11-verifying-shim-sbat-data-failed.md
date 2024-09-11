---
layout: post
title: Verifying shim SBAT data failed
date: 2024-09-11 10:11 +0200
categories: [UEFI, GRUB, Security, Firmware]
tags: [GRUB, firmware, secure boot, SBAT]
description: "After a windwos update, i had problems to boot my system. Before my GRUB strated, i got the error message 'Verifying shim SBAT data failed'."
---
# Introduction
After a Windows update, I had problems to boot my system. Before my GRUB started, I got the error message 'Verifying shim SBAT data failed'.
The only thing I could do was to boot into the BIOS. So I did some research with my smartphone and found a solution.

## Solution
The solution was to disable secure boot in the BIOS. After that, I could boot into ubuntu, where I deleted via terminal teh SBAT policy.
```bash
sudo mokutil --set-sbat-policy delete
```
After that, I could enable secure boot again and everything worked fine.

## Sidenote
Be careful when you disable secure boot. It is a security feature that protects your system from malware. If you disable it, you should be sure that your system is secure.

### End Thoughts
Maybe Dual booting is not the best idea. For another time i wouldn't do it again. But it is a good way to learn more about GRUB, the system itself and how it works.
