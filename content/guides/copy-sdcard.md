---
title: "Cloning an SD Card"
date: 2025-06-14
descripion: "Learn how to clone an SD card to a new one using simple tools on Windows, macOS, and Linux."
tags: ["guides", "sd card", "backup"]
---

Cloning an SD card is a great way to back up or duplicate your setup. You may want to clone the black label SDCard your system came with to a better quality SDCard. Here’s how to do it.

## Some caveats before we get started.
- ⚠️ This will erase the target card completely.
- ⚠️ These methods create a full 1:1 clone of your SD card — even if only 500MB is used, the resulting image will match the card's total size (e.g., 32GB for a 32GB card), but it includes hidden partitions.
- ⚠️ The restored image will match the original SD card’s size. Larger cards can be used, but extra space won’t be accessible unless manually expanded.
- ℹ️ For long-term storage, compress the image using your OS’s zip feature or a tool like 7-Zip, it’ll be much smaller than the raw image file.

![SDCard Properties](/images/guide/compressed_sd_size.png)

## 🧰 What You’ll Need

- A computer with an SD card reader
- Two SD cards (source and destination)
- A utility like:
  - **Windows**: [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
  - **macOS/Linux**: The `dd` command (built-in)

## 🪟 Windows Instructions

1. Download and open [**Win32 Disk Imager**](https://sourceforge.net/projects/win32diskimager/)
2. Insert your **source SD card**.
3. - Choose the device letter of your SDCard.
    - Click the little Folder Icon 📂 to choose where to save the Image. Name your image something like SDCardBackup.img
    - Click **Read** to create the image file. Depending on the size of your SDCard this will take a while for my 32GB SD Card it took 15min. (128GB=1h) ![Win32DiskImager](/images/guide/win32DiskImager.png)
4. Remove the source from your reader and insert your **target SD card**.
5. Select the same image file(already selected if you just did the read) and click **Write**.

> ⚠️ This will erase the target card completely.

## 🍎 macOS/Linux Instructions (using `dd`)

1. Insert the **source SD card**, open Terminal, and run:

    ```bash
    diskutil list
    ```

2. Find the source card (e.g. `/dev/disk2`) and clone it:

    ```bash
    sudo dd if=/dev/diskX of=~/sdcard_backup.img bs=1m
    ```

3. Swap in the **target SD card** and write the image:

    ```bash
    sudo dd if=~/sdcard_backup.img of=/dev/diskX bs=1m
    ```
> ⚠️ This will erase the target card completely.

> ⚠️ Replace `/dev/diskX` with your actual device paths!

---

## ✅ Done!

You’ve now copied your SD card. If it boots and works, go treat yourself to a cookie.
