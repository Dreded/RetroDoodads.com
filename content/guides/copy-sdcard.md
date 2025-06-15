---
title: "Cloning an SD Card"
date: 2025-06-14
descripion: "Learn how to clone an SD card to a new one using simple tools on Windows, macOS, and Linux."
tags: ["guides", "sd card", "backup"]
---

Copying an SD card is a great way to back up or duplicate your setup. Here’s how to do it.

## 🧰 What You’ll Need

- A computer with an SD card reader
- Two SD cards (source and destination)
- A utility like:
  - **Windows**: [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
  - **macOS/Linux**: The `dd` command (built-in)

---

## 🪟 Windows Instructions

1. Download and open **Win32 Disk Imager**.
2. Insert your **source SD card**.
3. Choose the device letter and click **Read** to create an image file.
4. Remove the source and insert your **target SD card**.
5. Select the same image file and click **Write**.

> ⚠️ This will erase the target card completely.

---

## 🍎 macOS/Linux Instructions (using `dd`)

1. Insert the **source SD card**, open Terminal, and run:

    ```bash
    diskutil list
    ```

2. Find the source card (e.g. `/dev/disk2`) and clone it:

    ```bash
    sudo dd if=/dev/rdisk2 of=~/sdcard_backup.img bs=1m
    ```

3. Swap in the **target SD card** and write the image:

    ```bash
    sudo dd if=~/sdcard_backup.img of=/dev/rdisk3 bs=1m
    ```

> Replace `/dev/rdiskX` with your actual device paths!

---

## ✅ Done!

You’ve now copied your SD card. If it boots and works, go treat yourself to a cookie.
